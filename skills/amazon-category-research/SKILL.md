---
name: amazon-category-research
description: >
  对任何亚马逊畅销榜类目进行全面的深度研究。当用户提供类目URL时使用此skill，包括研究亚马逊产品类目、分析亚马逊畅销榜、
  调查亚马逊细分市场、为亚马逊销售进行市场调研，或提供亚马逊畅销榜/gp/bestsellers URL。也可在以下请求时触发：
  "调研这个亚马逊品类"、"分析这个Amazon类目"、"深度调研Amazon Best Sellers"、"分析亚马逊畅销榜"、
  "Amazon品类机会分析"，或任何研究/分析/调查亚马逊类目或畅销榜的请求。
---

# Amazon 类目深度研究

任何亚马逊畅销榜类目的端到端自主研究工作流。用户提供类目URL；skill收集数据、运行并行分析，并生成全面的中文报告包。

## 前置条件

- **Playwright MCP服务器** 必须可用（browser_navigate、browser_evaluate、browser_snapshot、browser_close）
- **Agent工具** 用于启动并行分析子代理
- 报告保存到 `{project_root}/reports/{category-slug}/`（例如 `reports/toys-and-games/`、`reports/building-toys/`）。
  在每次运行开始时创建子目录。

## 工作流程概览

skill分三个阶段运行：数据收集、并行分析、报告综合。使用TaskCreate/TaskUpdate追踪进度。

**重要**：所有文件输出（JSON数据、分析报告、综合报告）必须进入 `reports/` 下的类目特定子文件夹。从类目名称中提取人类可读的slug（例如 "Building & Construction Toys" → `building-toys`，"Toys & Games" → `toys-and-games`）。在保存任何文件之前创建目录。

---

## 第一阶段：数据收集

### 步骤1.1 — 解析用户输入

从用户消息中提取：
- **类目URL**（必填）— 亚马逊畅销榜URL，例如 `https://www.amazon.com/gp/bestsellers/toys-and-games/`
- **子类目**（可选）— 特定的子类目进行深度研究。如果省略，自动选择与主Top 30列表最相关的Top 5。
- **报告语言**（可选，默认：简体中文）

### 步骤1.2 — 抓取主类目 Top 30

使用 `mcp__playwright__browser_navigate` 导航到类目URL。等待页面完全加载。

使用 `mcp__playwright__browser_evaluate` 运行此提取脚本：

```javascript
() => {
  const lines = document.body.innerText.split('\n');
  const products = [];
  let current = null;
  for (let i = 0; i < lines.length; i++) {
    const match = lines[i].match(/^#(\d+)$/);
    if (match) {
      if (current && current.title) products.push(current);
      current = { rank: parseInt(match[1]) };
    } else if (current) {
      if (lines[i].includes('out of 5 stars')) current.stars = lines[i].trim();
      else if (lines[i].includes('offers from') || lines[i].match(/^\$[\d,.]+$/)) current.price = lines[i].trim();
      else if (lines[i].match(/^[\d,]+$/) && current.stars) current.reviews = lines[i].trim();
      else if (lines[i].trim().length > 15 &&
               !lines[i].includes('Movers') && !lines[i].includes('New Releases') &&
               !current.title) {
        current.title = lines[i].trim();
      }
    }
  }
  if (current && current.title) products.push(current);
  const nrIdx = products.findIndex(p => p.title && (p.title.includes('New Releases') || p.title.includes('Movers')));
  const result = nrIdx > 0 ? products.slice(0, nrIdx) : products.filter(p => p.title && p.title.length > 10);
  return result.slice(0, 30);
}
```

将结果保存到 `reports/{category-slug}/{category-slug}_top30.json`（使用人类可读的slug如 `building-toys`）。

### 步骤1.3 — 发现子类目

在同一页面上，使用 `mcp__playwright__browser_evaluate` 查找子类目导航链接：

```javascript
() => {
  const allLists = document.querySelectorAll('ul, ol');
  const subcats = [];
  allLists.forEach(list => {
    const items = list.querySelectorAll('li');
    const firstText = items[0]?.textContent?.trim() || '';
    if (firstText.includes('Action & Toy Figures') || firstText.includes('Arts & Crafts') || firstText.includes('Baby & Toddler') || firstText.includes('Building')) {
      list.querySelectorAll('a').forEach(a => {
        subcats.push({ name: a.textContent.trim(), url: a.href });
      });
    }
  });
  return subcats;
}
```

这会从左侧边栏返回完整的子类目链接列表。如果失败（返回空），尝试替代选择器：`a[href*="/zgbs/"]`，或从"任何部门"下拉菜单文本提取。

如果用户指定了子类目，按名称匹配。否则，使用以下逻辑自动选择 **5个子类目**：
1. 将每个Top 30产品映射到其最可能的子类目
2. 按在Top 30中出现频率对子类目排序
3. 选择前5名（排除主类目本身）
4. 如果少于5个出现，用相邻类目填充

### 步骤1.4 — 抓取每个子类目 Top 20

对于每个选定的子类目：
1. 使用 `mcp__playwright__browser_navigate` 导航到其URL
2. 运行与步骤1.2相同的提取脚本（但用 `.slice(0, 20)` 而不是30）
3. 保存到 `reports/{category-slug}/{subcategory_slug}_top20.json`

按顺序执行（Playwright使用单个浏览器标签）。最多定位5个子类目。

### 步骤1.5 — 关闭浏览器

所有抓取完成后运行 `mcp__playwright__browser_close`。

---

## 第二阶段：并行分析

使用 `run_in_background: true` 和 `subagent_type: "general-purpose"` 同时启动 **4个分析代理**。
每个代理接收完整的原始数据并将报告写入 `reports/`。

### 代理1 — 细分市场分析

文件：`reports/{category-slug}/{category-slug}_niche_analysis.md`

提示代理分析：
1. **产品类型分布** — 哪些类目主导Top 30，百分比细分
2. **价格带分析** — $0-7 / $7-15 / $15-30 / $30-50 / $50+ 分布和可行性
3. **星级评分模式** — 识别质量差距（高需求 + 低评分 = 机会）
4. **Top 5细分市场推荐** — 按：需求水平、竞争强度、利润潜力、入场难度排序
5. **供应链指导** — 采购地点（义乌、汕头、东莞等）、工厂类型、最小起订量预期
6. **风险评估** — 合规性、季节性、知识产权、竞争风险

### 代理2 — 竞品分析

文件：`reports/{category-slug}/{category-slug}_competitor_analysis.md`

提示代理分析：
1. **品牌格局** — 识别重复品牌、品牌集中度、中国卖家vs美国卖家比例
2. **产品策略** — SKU矩阵/变体玩法、捆绑、IP许可、定价策略
3. **评论壁垒** — 按价格层级估计新卖家竞争的评论阈值
4. **入场难度评级**（1-5星）用于每个主要子类目
5. **Top 3入场推荐** 包含目标价格、差异化角度和风险级别
6. **评论建立策略** — Vine计划、请求评论、社交播种时间线

### 代理3 — 关键词分析

文件：`reports/{category-slug}/{category-slug}_keyword_analysis.md`

提示代理分析：
1. **高频关键词** — 从所有产品标题提取，按频率排序，按子类目分组
2. **搜索意图分析** — 按年龄段（0-2、2-4、4-8、8-12）、按场景（生日、教育、旅行、节日）
3. **关键词策略** — 高量低竞争机会、每个子类目的标题公式、后端关键词模板（250字节）
4. **PPC关键词矩阵** — 针对前4个子类目：广泛/短语/精确匹配建议 + 负关键词
5. **季节性关键词日历** — 按月计划Q2（夏季）、Q3（返校）、Q4（节日）

### 代理4 — 利润分析

文件：`reports/{category-slug}/{category-slug}_profit_analysis.md`

提示代理分析：
1. **价格层级利润模型** — 每个价格带（$0-7、$7-15、$15-30、$30-50、$50+）：从阿里估计COGS、
   FBA费用（推荐费15%、配送费、仓储费）、净利率范围
2. **每个类目的单位经济学** — 针对前5个子类目：估计COGS、FBA费用、每单位净利润、利润率%
3. **FBA优化** — 包装尺寸层级降低策略、仓储技巧
4. **启动成本模型** — 最小可行启动预算（2个SKU x 500件）、广告预算建议
5. **盈亏平衡分析** — 覆盖固定成本所需的月度单位销量
6. **投资回报率排名** — 按估计投资回报率对子类目排序

**重要**：将实际抓取的数据（不是摘要）传递给每个代理。包含所有产品标题、价格、评分和评论数。代理需要真实数据才能产生有意义的分析。

---

## 第三阶段：报告综合

等待所有4个代理完成（你将收到任务通知）。然后启动一个最终综合代理
（`subagent_type: "general-purpose"`，这次是前台运行，因为我们需要结果）来生成综合报告。

### 最终报告

文件：`reports/{category-slug}/{category-slug}_comprehensive_report.md`

综合代理应：
1. 从 `reports/` 读取所有4份分析报告
2. 结合原始产品数据
3. 生成具有以下确切结构的综合报告：

```markdown
# 亚马逊美国站 {Category Name} 品类综合研究报告

## 目录
1. 执行摘要
2. 品类全景概览
3. 子品类深度分析 (Deep dive per subcategory)
4. 市场机会矩阵
5. 新卖家入场策略
6. 运营落地指南
7. 财务模型
8. 风险管控
9. 行动路线图
```

**必须包含的关键部分：**

- **执行摘要**：1页概览，包含Top 5机会表（细分市场、评分、利润、启动成本、回本周期）
- **品类格局**：Top 30产品类型分布表、按FBA费用比率的价格带分析
- **子类目深度研究**：每个抓取的子类目：市场特征、竞争格局、定价分析、主要参与者、入场难度评级（1-5星）
- **市场机会矩阵**：按4个维度（需求、竞争、利润、难度）对8-12个细分市场评级，分配S/A/B/C等级
- **入场策略**：3个阶段 — 验证期（1-2月）、扩展期（3-6月）、品牌建设期（6-12月）
- **运营手册**：Listing标题公式、关键词策略、PPC分阶段计划、评论建立、季节性日历
- **财务模型**：两个启动预算（精简版$3-5K、标准版$8-15K）、前3个产品的单位经济学、盈亏平衡分析、6个月损益预测
- **风险管理**：合规清单（适用的CPC/CPSIA/ASTM/FCC）、知识产权保护、季节性库存、竞争防御
- **行动路线图**：详细的30/60/90天计划及里程碑

---

## 输出总结

所有阶段完成后，向用户呈现：

1. 所有生成报告的汇总表及文件路径
2. 研究的Top 5关键发现
3. Top 3推荐行动项

## 错误处理

- 如果Playwright导航失败，重试一次，然后尝试 `mcp__web_reader__webReader` 作为备选
- 如果提取脚本返回空结果，页面结构可能不同 — 使用 `browser_snapshot` 检查页面结构并调整选择器
- 如果子类目发现失败，要求用户提供子类目URL
- 如果任何分析代理失败，重新生成该报告
