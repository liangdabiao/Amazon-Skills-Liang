# Amazon 品类深度调研（Category Deep Research）

## 概述

品类深度调研是 Amazon Skills 体系中**品类级别的全景分析技能**。只需提供一个 Amazon Best Sellers URL，即可自动完成从数据采集到报告生成的全流程，输出 **5 份覆盖品类决策全链路的专业分析报告**——包括利基市场分析、竞品格局、关键词SEO策略、利润机会分析，以及一份9章节综合研究报告。

### 与 amazon-one-shot 的区别

| 维度 | amazon-one-shot | amazon-category-research |
|------|----------------|------------------------|
| **分析粒度** | 单个ASIN（单品深度） | 整个Best Sellers品类（品类广度） |
| **数据规模** | 1个产品 + 3-4个竞品 | 130个产品（主榜30 + 5子品类各20） |
| **适用场景** | 已锁定产品，评估是否值得做 | 还在选品阶段，寻找有潜力的品类方向 |
| **输出报告** | 9份（围绕1个ASIN） | 5份（围绕整个品类） |
| **典型用法** | "深度调研 B07PQFT83F" | "调研这个亚马逊品类：[Best Sellers URL]" |

**推荐使用顺序**：先用 `amazon-category-research` 锁定品类方向，再用 `amazon-one-shot` 对具体产品做深度验证。

---

## 核心原理

### 数据采集原理：Best Sellers 页面解析

技能使用 Playwright 浏览器自动化技术，通过页面文本行解析提取 Amazon Best Sellers 页面的产品数据。与 one-shot 不同的是，品类调研不依赖特定的 DOM 选择器（因为 Best Sellers 页面结构可能因品类而异），而是采用通用的文本模式匹配：

- 通过 `#1`、`#2` 等排名标识定位产品起始位置
- 依次解析标题、评分（`out of 5 stars`）、价格（`$XX.XX` 或 `X offers from $X.XX`）、评论数
- 在 "New Releases" 标记处截断，确保只获取 Best Sellers 部分

### 子品类发现原理：侧边栏导航解析

Amazon Best Sellers 页面的左侧导航栏包含该品类的所有子品类链接。技能通过遍历页面所有 `<ul>` 列表，找到第一个子品类名称（如 "Action & Toy Figures"）所在的列表，从而提取全部子品类链接。

### 并行分析原理：4 Agent 同时运行

数据采集完成后，技能同时启动 4 个独立的分析 Agent（后台运行），每个 Agent 接收全量原始数据，独立完成分析并写入报告文件：

1. **利基分析 Agent** — 品类趋势、价格分布、Top 5 利基推荐、供应链建议
2. **竞品分析 Agent** — 品牌格局、竞争壁垒、评论门槛、新卖家入场建议
3. **关键词分析 Agent** — 高频词提取、搜索意图、PPC策略、季节性规划
4. **利润分析 Agent** — 单位经济学、FBA费用、ROI估算、盈亏平衡

4 个 Agent 完成后，启动综合报告 Agent，读取全部 4 份分析报告和原始数据，生成最终的9章节综合报告。

---

## 工作流程

```
用户提供 Best Sellers URL
         │
         ▼
┌─────────────────────────────┐
│ Step 1: 主榜数据采集          │  ← 导航到 Best Sellers 页面
│ • Top 30 产品（排名/标题/     │  ← 文本解析提取
│   价格/评分/评论数）          │
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Step 2: 子品类发现            │  ← 解析侧边栏导航
│ • 发现全部子品类链接          │  ← 选择Top 5（基于主榜）
│ • 创建子目录                  │
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Step 3: 子品类数据采集        │  ← 依次导航5个子品类页面
│ • 每个子品类 Top 20           │  ← 相同解析逻辑
│ • 共100个额外数据点            │  ← 保存为JSON
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Step 4: 并行分析（4 Agent）   │  ← 后台同时运行
│ • 利基分析                    │  ← 全量数据
│ • 竞品分析                    │  ← 独立分析
│ • 关键词分析                   │  ← 独立分析
│ • 利润分析                    │  ← 独立分析
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Step 5: 综合报告              │  ← 等待4个Agent完成
│ • 读取4份分析报告            │  ← 交叉引用
│ • 9章节综合报告              │  ← 最终输出
└─────────────────────────────┘
```

---

## 输出结构

```
reports/
├── toys-and-games/                            ← Toys & Games 品类
│   ├── toys_games_comprehensive_report.md         # 综合报告（9章节）
│   ├── toys_games_niche_analysis.md             # 利基市场分析
│   ├── toys_games_competitor_analysis.md        # 竞品格局分析
│   ├── toys_games_keyword_analysis.md           # 关键词SEO分析
│   ├── toys_games_profit_analysis.md            # 利润机会分析
│   └── *_bestsellers.json                      # 原始数据文件
│
├── building-toys/                             ← Building Toys 子品类
│   ├── building_toys_comprehensive_report.md
│   ├── building_toys_niche_analysis.md
│   ├── building_toys_competitor_analysis.md
│   ├── building_toys_keyword_analysis.md
│   ├── building_toys_profit_analysis.md
│   ├── building_toys_top30.json
│   └── *_top20.json
│
└── 2026-04-18_B0033SHO4Q/                  ← 单品报告（one-shot）
    └── ...（9份报告）
```

---

## 使用方法

### 触发方式

```
# 中文
"调研这个亚马逊品类：https://www.amazon.com/gp/bestsellers/toys-and-games/"
"分析Amazon Best Sellers Building Toys"
"深度调研Amazon类目 https://www.amazon.com/gp/bestsellers/toys-and-games/166092011"

# 英文
"research this Amazon category: https://www.amazon.com/gp/bestsellers/toys-and-games/"
"analyze Amazon Best Sellers in Baby & Toddler Toys"
```

### 前置要求

| 要求 | 说明 | 是否必须 |
|---|---|---|
| Playwright MCP | 浏览器自动化，用于抓取 Best Sellers 页面 | ✅ 必须 |
| 工作目录 | 报告输出到 `reports/{category-slug}/` | ✅ 自动创建 |

### 参数说明

| 参数 | 说明 | 默认值 |
|---|---|---|
| **品类URL**（必须） | Amazon Best Sellers 页面链接 | 无 |
| **子品类**（可选） | 指定要深入调研的子品类 | 自动选择Top 5 |
| **报告语言**（可选） | 报告输出语言 | 简体中文 |

---

## 已验证的品类

| 品类 | 子品类数 | 产品数 | 核心发现 |
|------|---------|--------|---------|
| **Toys & Games** | 21个子品类 | 130 | 派对用品占23.3%主导，$5-$10核心价格带，捏捏/解压玩具评分两极分化 |
| **Building & Construction Toys** | 6个子品类 | 130 | LEGO占主榜80%，磁力片是非LEGO最大机会（综合评分92/100），叠叠乐入门门槛最低 |

---

## 与其他技能的关系

```
                    ┌─────────────────────┐
                    │ amazon-category-    │
                    │ research (品类调研)  │
                    └──────────┬──────────┘
                               │ 锁定品类方向后
                               ▼
                    ┌─────────────────────┐
                    │ amazon-one-shot      │
                    │ (单品深度调研)     │
                    └──────────┬──────────┘
                               │ 跨品类复用
                ┌──────────────┼──────────────┐
                ▼              ▼              ▼
        ┌──────────┐  ┌──────────┐  ┌──────────┐
        │ keyword │  │ listing  │  │ fba-      │
        │ research │  │ optimize │  │calculator│
        └──────────┘  └──────────┘  └──────────┘
```

category-research 是品类级扫描工具，one-shot 是单品级验证工具。先用前者回答"哪个品类值得做"，再用后者回答"这个具体产品值不值得做"。

---

## 版本信息

- **版本**: 1.0.0
- **创建日期**: 2026-04-19
- **已测试品类**: Toys & Games, Building & Construction Toys
- **平台**: Amazon US (amazon.com)
- **语言**: 中文输出
