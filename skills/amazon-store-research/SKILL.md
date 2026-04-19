---
name: amazon-store-research
description: >
  对任何亚马逊卖家店铺进行全面的深度研究。当用户提供店铺URL时使用此skill，包括研究亚马逊店铺、分析卖家 storefront、
  调查亚马逊品牌、研究竞品店铺，或提供亚马逊店铺URL（amazon.com/stores/...）。也可在以下请求时触发：
  "调研这个亚马逊店铺"、"分析这个Amazon卖家"、"深度调研Amazon店铺"、"分析亚马逊品牌店铺"、
  "Amazon店铺调研"、"调研这个卖家"、"分析竞争对手店铺"，或任何研究/分析/调查亚马逊卖家店铺或品牌 storefront 的请求。
---

# Amazon 店铺深度研究

任何亚马逊卖家店铺的端到端自主研究工作流。用户提供店铺URL；skill从 storefront 收集数据、运行并行分析，并生成全面的中文报告包。

## 前置条件

- **Playwright MCP服务器** 必须可用（browser_navigate、browser_evaluate、browser_snapshot、browser_close）
- **Agent工具** 用于启动并行分析子代理
- 报告保存到 `{project_root}/reports/{store-slug}/`（例如 `reports/jmbricklayer/`）。
  在每次运行开始时创建子目录。

## 工作流程概览

skill分三个阶段运行：数据收集、并行分析、报告综合。使用TaskCreate/TaskUpdate追踪进度。

**重要**：所有文件输出（JSON数据、分析报告、综合报告）必须进入 `reports/` 下的店铺特定子文件夹。从店铺名称中提取人类可读的slug（例如 "JMBricklayer" → `jmbricklayer`）。在保存任何文件之前创建目录。

---

## 第一阶段：数据收集

### 步骤1.1 — 解析用户输入

从用户消息中提取：
- **店铺URL**（必填）— 亚马逊店铺URL，例如 `https://www.amazon.com/stores/JMBricklayer/page/3CACFA02-74C5-4F9D-81DB-0BF560B7BA47`
- **店铺名称** — 从URL或页面标题提取
- **报告语言**（可选，默认：简体中文）

### 步骤1.2 — 抓取店铺首页

使用 `mcp__playwright__browser_navigate` 导航到店铺URL。等待页面完全加载。

首先，使用 `mcp__playwright__browser_evaluate` 提取店铺导航结构：

```javascript
() => {
  const storeInfo = {};
  const navItems = Array.from(document.querySelectorAll('nav a, nav button'));
  storeInfo.navigation = navItems.map(item => ({
    text: item.textContent?.trim(),
    url: item.href || '',
    type: item.tagName === 'BUTTON' ? 'dropdown' : 'link'
  })).filter(item => item.text && item.text.length > 0 && item.text !== 'Back');

  const productLinks = Array.from(document.querySelectorAll('a[href*="/dp/"]'));
  storeInfo.productLinks = productLinks.map(a => ({
    asin: a.href.match(/\/dp\/([A-Z0-9]+)/)?.[1],
    text: a.textContent?.trim()?.substring(0, 200)
  }));

  const collectionLinks = Array.from(document.querySelectorAll('a[href*="/stores/page/"]'));
  storeInfo.collections = collectionLinks.map(a => ({
    text: a.textContent?.trim(),
    url: a.href,
    id: a.href.match(/page\/([A-F0-9-]+)/)?.[1]
  })).filter(c => c.text && c.text.length > 0);

  return storeInfo;
}
```

这揭示了：
- 店铺导航项（首页、畅销品、新品、合集、下拉菜单）
- 所有合集/类别页面URL
- 首页可见的产品链接

### 步骤1.3 — 从首页提取产品

使用 `mcp__playwright__browser_evaluate` 运行此产品提取脚本：

```javascript
() => {
  const products = [];
  const seen = new Set();
  const allLinks = Array.from(document.querySelectorAll('a[href*="/dp/"]'));

  allLinks.forEach(a => {
    const href = a.href;
    const asinMatch = href.match(/\/dp\/([A-Z0-9]+)/);
    if (!asinMatch) return;
    const asin = asinMatch[1];
    if (seen.has(asin)) return;

    const title = a.textContent?.trim();
    if (title && title.length > 20 && !title.includes('Amazon Business') && !title.includes('Reload Your')) {
      seen.add(asin);
      const container = a.closest('li') || a.parentElement?.parentElement?.parentElement || document.body;
      const containerText = container?.innerText || '';
      const priceMatch = containerText.match(/\$[\d,.]+/);
      const reviewMatch = containerText.match(/\(([\d,K]+)\)/);
      const ratingMatch = containerText.match(/([\d.]+) out of 5/);

      products.push({
        asin,
        title: title.substring(0, 200),
        price: priceMatch?.[0] || null,
        reviews: reviewMatch?.[1] || null,
        rating: ratingMatch?.[1] || null,
        url: href.split('?')[0]
      });
    }
  });
  return products;
}
```

### 步骤1.4 — 抓取关键店铺页面

使用步骤1.2发现的合集URL导航到每个关键页面。标准店铺页面包括：

1. **畅销品** — 查找文本为"Best Sellers"的导航项
2. **新品** — 查找文本为"New Releases"的导航项
3. **关于我们** — 查找文本为"About us"的导航项

对于每个页面，使用步骤1.3中的相同产品提取脚本。

### 步骤1.5 — 抓取合集/类别页面

导航到从导航中发现的每个主题合集页面。使用相同的产品提取脚本。

常见合集模式：
- "按主题购物"下拉菜单 → 包含主题类别
- "按难度"下拉菜单 → 包含难度级别
- 独立合集链接（场合等）

**重要**：识别导航中的下拉菜单。下拉项（由 `type: 'dropdown'` 或嵌套链接指示）包含实际的合集子页面。抓取每个子合集页面。

### 步骤1.6 — 关闭浏览器

所有抓取完成后运行 `mcp__playwright__browser_close`。

### 步骤1.7 — 保存原始数据

将所有抓取的数据整合到 `reports/{store-slug}/{store-slug}_store_data.json` 的单个JSON文件中，结构如下：

```json
{
  "storeInfo": {
    "brandName": "...",
    "storeUrl": "...",
    "storefrontId": "...",
    "scrapeDate": "...",
    "navigation": [...],
    "totalUniqueASINs": 0,
    "priceRange": "..."
  },
  "homePage": { "products": [...] },
  "bestSellers": { "products": [...] },
  "newReleases": { "products": [...] },
  "collections": {
    "Collection Name": { "productCount": 0, "products": [...] }
  }
}
```

跨所有页面去重ASIN并计算唯一产品数。

---

## 第二阶段：并行分析

使用 `run_in_background: true` 和 `subagent_type: "general-purpose"` 同时启动 **4个分析代理**。
每个代理接收完整的原始数据并将报告写入 `reports/{store-slug}/`。

### 代理1 — 产品组合分析

文件：`reports/{store-slug}/{store-slug}_portfolio_analysis.md`

提示代理分析：
1. **店铺概览** — 品牌定位、类目覆盖、ASIN总数、价格范围
2. **产品矩阵** — 跨合集/类目分布、跨类目重叠
3. **产品编号系统** — 识别产品代码/编号中的任何模式
4. **定价策略** — 价格带、每个合集的平均价格、定价层级
5. **评分与评论分析** — 每个合集的平均评分、评论分布、评论壁垒
6. **Top产品档案** — 按评论数排名的Top 10产品及特征
7. **新品发布节奏** — 产品推出速度、创新方向、近期主题
8. **SKU策略** — 产品线扩展、系列开发、尺寸/片数梯度

### 代理2 — 竞争定位分析

文件：`reports/{store-slug}/{store-slug}_competitive_analysis.md`

提示代理分析：
1. **竞争格局** — 品牌定位（例如LEGO替代品、细分玩家、中国出口品牌）
2. **SWOT分析** — 优势、劣势、机会、威胁及具体证据
3. **直接竞品对比** — vs主要品牌（LEGO及与类目相关的任何知名替代品牌）
4. **差异化策略** — 独特功能（LED灯、授权、主题、价格优势）
5. **目标客户细分** — 谁购买这些产品（收藏者、礼品买家、爱好者等）
6. **Listing策略** — 标题关键词模式、常见短语、优化观察
7. **评论质量分析** — 跨合集评分对比，识别弱/强合集

### 代理3 — 收入估算分析

文件：`reports/{store-slug}/{store-slug}_revenue_analysis.md`

提示代理分析：
1. **销售估算方法论** — 评论与销售比率、评论增速、日评论率
2. **Top 10产品月估算** — 月单位销量和收入（保守/中性/乐观）
3. **店铺月收入** — 分层模型（Top 10 + 第二层 + 第三层长尾），三种场景
4. **合集收入贡献** — 哪些合集驱动最多收入
5. **价格弹性分析** — 哪些价格带积累评论最快
6. **产品生命周期分析** — 按评论数将产品分类为生命周期阶段
7. **新产品表现** — 评估早期产品（低评论数）
8. **年度收入预测** — 月度 × 12 并考虑Q4季节性权重

### 代理4 — 增长策略分析

文件：`reports/{store-slug}/{store-slug}_growth_strategy.md`

提示代理分析：
1. **品牌发展评估** — 成熟度、市场验证、价格覆盖
2. **增长机会** — 哪些合集可扩展、服务不足的细分市场、新主题
3. **产品优化** — 修复低评分产品、填补价格空白、捆绑机会
4. **运营策略** — PPC关键词、评论建立、促销日历、库存
5. **竞争应对** — 如何针对大品牌和类似替代品定位
6. **市场扩展** — 国际市场、品牌网站、社交媒体
7. **风险评估** — 知识产权风险、质量问题、物流挑战、季节依赖
8. **行动路线图** — 30/60/90天计划及具体里程碑

**重要**：将实际抓取的数据（不是摘要）传递给每个代理。从JSON文件包含所有产品ASIN、标题、价格、评分和评论数。代理需要真实数据才能产生有意义的分析。

---

## 第三阶段：报告综合

等待所有4个代理完成（你将收到任务通知）。然后启动一个最终综合代理
（`subagent_type: "general-purpose"`，这次是前台运行，因为我们需要结果）来生成综合报告。

### 最终报告

文件：`reports/{store-slug}/{store-slug}_comprehensive_report.md`

综合代理应：
1. 从 `reports/` 读取所有4份分析报告
2. 结合原始产品数据
3. 生成具有以下确切结构的综合报告：

```markdown
# {Store Name} 亚马逊店铺深度调研报告

## 目录
1. 执行摘要
2. 店铺全景概览
3. 产品组合深度分析
4. 竞争定位与差异化策略
5. 收入与销售表现
6. 增长机会与风险评估
7. 运营优化建议
8. 关键发现与行动建议
```

**必须包含的关键部分：**

- **执行摘要**：1页概览，包含Top 5机会表（细分市场、评分、利润、入场难度）和关键指标仪表板（ASIN数、价格范围、平均评分、预估月收入）
- **店铺概览**：品牌定位、导航结构、产品编号系统、产品数量合集表
- **产品组合**：价格带分布、按合集评分、Top 10产品、新产品线、生命周期分布
- **竞争定位**：SWOT矩阵、主要品牌价格对比、差异化、目标客户细分及百分比
- **收入与销售**：Top 10月估算（3种场景）、合集收入%、店铺月/年收入及季节性
- **增长与风险**：按潜力排序的5个机会、带缓解措施的5个风险、低评分产品诊断
- **运营**：PPC策略、listing优化、评论建立、促销日历
- **关键发现**：Top 5发现、Top 5行动项、30/60/90天路线图

---

## 输出总结

所有阶段完成后，向用户呈现：

1. 所有生成报告的汇总表及文件路径
2. 研究的Top 5关键发现
3. Top 3推荐行动项

## 错误处理

- 如果Playwright导航失败，重试一次，然后尝试 `mcp__web_reader__webReader` 作为备选
- 如果提取脚本返回空结果，使用 `browser_snapshot` 检查页面结构并调整
- 如果合集发现失败，在导航中查找替代URL模式
- 如果合集页面没有产品，跳过并注明空结果
- 如果任何分析代理失败，重新生成该报告
- **数据异常观察**：与产品型号匹配的评论数（例如"40102"条评论）可能是抓取伪影 — 在分析中标记这些
