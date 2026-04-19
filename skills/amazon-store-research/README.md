# Amazon 店铺深度调研（Store Deep Research）

## 概述

店铺深度调研是 Amazon Skills 体系中**店铺级别的全景分析技能**。只需提供一个 Amazon Stores URL，即可自动完成从数据采集到报告生成的全流程，输出 **5 份覆盖店铺决策全链路的专业分析报告**——包括产品组合分析、竞争定位分析、收入估算分析、增长策略分析，以及一份8章节综合研究报告。

### 与其他技能的区别

| 维度 | amazon-one-shot | amazon-category-research | amazon-store-research |
|------|----------------|------------------------|---------------------|
| **分析粒度** | 单个ASIN（单品深度） | 整个Best Sellers品类 | 整个卖家店铺 |
| **数据来源** | 1个产品页面 + 竞品 | Best Sellers排行页 | 店铺首页 + 各主题合集页 |
| **数据规模** | 1个产品 + 3-4个竞品 | 130个产品（主榜30 + 子品类） | 全店铺产品（典型30-60个ASIN） |
| **适用场景** | 已锁定产品，评估单品 | 选品阶段，寻找品类方向 | 竞品分析/卖家调研/品牌研究 |
| **输出报告** | 9份（围绕1个ASIN） | 5份（围绕整个品类） | 5份（围绕整个店铺） |
| **典型用法** | "深度调研 B07PQFT83F" | "调研这个亚马逊品类：[URL]" | "调研这个店铺：[Stores URL]" |

**推荐使用顺序**：
1. `amazon-category-research` — 锁定品类方向
2. `amazon-store-research` — 深度调研竞品/对标店铺
3. `amazon-one-shot` — 对具体产品做深度验证

---

## 核心原理

### 数据采集原理：Amazon Stores 页面解析

技能使用 Playwright 浏览器自动化技术，通过页面 DOM 解析提取 Amazon Stores 页面的产品数据。店铺页面与 Best Sellers 页面结构不同，采用不同的解析策略：

- 通过 `a[href*="/dp/"]` 选择器定位所有产品链接
- 从产品链接文本中提取标题
- 从相邻 DOM 元素中提取价格、评分、评论数
- 通过 `a[href*="/stores/page/"]` 发现所有主题合集页

### 店铺导航解析原理

Amazon Stores 页面的顶部导航栏包含店铺的分类结构。技能通过解析导航链接发现所有主题合集：

- 通过 `nav` 元素内的 `a` 和 `button` 标签提取导航项
- `type: 'dropdown'` 的按钮表示有子分类的下拉菜单
- 每个 `/stores/page/{UUID}` 链接对应一个主题合集页

### 并行分析原理：4 Agent 同时运行

数据采集完成后，技能同时启动 4 个独立的分析 Agent（后台运行），每个 Agent 接收全量原始数据，独立完成分析并写入报告文件：

1. **产品组合分析 Agent** — 产品矩阵、价格策略、爆款画像、编号体系
2. **竞争定位分析 Agent** — SWOT分析、品牌对比、差异化策略、目标客群
3. **收入估算分析 Agent** — 月销估算、系列收入贡献、年度推算
4. **增长策略分析 Agent** — 增长机会、产品优化、运营建议、行动路线图

4 个 Agent 完成后，启动综合报告 Agent，读取全部 4 份分析报告和原始数据，生成最终的8章节综合报告。

---

## 工作流程

```
用户提供 Store URL
         │
         ▼
┌─────────────────────────────┐
│ Step 1: 店铺首页采集          │  ← 导航到 Store 页面
│ • 导航结构(分类/合集)         │  ← DOM 解析提取
│ • 首页展示产品                │  ← 产品链接提取
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Step 2: 关键页面采集          │  ← Best Sellers
│ • Best Sellers 产品列表       │  ← New Releases
│ • New Releases 产品列表       │  ← About us
│ • 店铺介绍信息                │
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Step 3: 合集页采集            │  ← 逐个导航到合集页
│ • 每个主题合集的产品          │  ← 相同解析逻辑
│ • 按分类整理产品数据          │  ← 标记所属合集
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Step 4: 数据整合              │  ← 关闭浏览器
│ • ASIN 去重统计               │  ← 保存 JSON 数据文件
│ • 构建完整数据结构            │
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Step 5: 并行分析（4 Agent）   │  ← 后台同时运行
│ • 产品组合分析                │  ← 全量数据
│ • 竞争定位分析                │  ← 独立分析
│ • 收入估算分析                │  ← 独立分析
│ • 增长策略分析                │  ← 独立分析
└──────────┬──────────────────┘
           │
           ▼
┌─────────────────────────────┐
│ Step 6: 综合报告              │  ← 等待4个Agent完成
│ • 读取4份分析报告            │  ← 交叉引用
│ • 8章节综合报告              │  ← 最终输出
└─────────────────────────────┘
```

---

## 输出结构

```
reports/
├── jmbricklayer/                                  ← JMBricklayer 店铺
│   ├── jmbricklayer_comprehensive_report.md           # 综合报告（8章节）
│   ├── jmbricklayer_portfolio_analysis.md             # 产品组合分析
│   ├── jmbricklayer_competitive_analysis.md           # 竞争定位分析
│   ├── jmbricklayer_revenue_analysis.md              # 收入估算分析
│   ├── jmbricklayer_growth_strategy.md              # 增长策略建议
│   └── jmbricklayer_store_data.json                  # 原始数据文件
│
├── some-brand/                                    ← 其他店铺
│   ├── some_brand_comprehensive_report.md
│   ├── some_brand_portfolio_analysis.md
│   ├── some_brand_competitive_analysis.md
│   ├── some_brand_revenue_analysis.md
│   ├── some_brand_growth_strategy.md
│   └── some_brand_store_data.json
│
├── toys-and-games/                                ← 品类调研（category-research）
│   └── ...
│
└── 2026-04-18_B0033SHO4Q/                         ← 单品报告（one-shot）
    └── ...
```

---

## 使用方法

### 触发方式

```
# 中文
"调研这个亚马逊店铺：https://www.amazon.com/stores/JMBricklayer/page/..."
"分析Amazon卖家店铺"
"深度调研这个竞品店铺"
"分析竞争对手的Amazon品牌"

# 英文
"research this Amazon store: https://www.amazon.com/stores/..."
"analyze this Amazon seller storefront"
"deep research this competitor store"
```

### 前置要求

| 要求 | 说明 | 是否必须 |
|---|---|---|
| Playwright MCP | 浏览器自动化，用于抓取 Store 页面 | ✅ 必须 |
| 工作目录 | 报告输出到 `reports/{store-slug}/` | ✅ 自动创建 |

### 参数说明

| 参数 | 说明 | 默认值 |
|---|---|---|
| **店铺URL**（必须） | Amazon Stores 页面链接 | 无 |
| **报告语言**（可选） | 报告输出语言 | 简体中文 |

---

## 已验证的店铺

| 店铺 | 品类 | 产品数 | 核心发现 |
|------|------|--------|---------|
| **JMBricklayer** | Building Toys | 45 | 8大主题系列，月收入约$40万，植物系列评分最高4.5+，军事系列是蓝海赛道 |
| **标星模王** | Building Toys | - | 待验证 |

---

## 与其他技能的关系

```
           ┌─────────────────────┐
           │ amazon-category-    │
           │ research (品类调研)  │
           └──────────┬──────────┘
                      │ 锁定品类后
                      ▼
           ┌─────────────────────┐
           │ amazon-store-       │
           │ research (店铺调研)  │
           └──────────┬──────────┘
                      │ 找到对标产品后
                      ▼
           ┌─────────────────────┐
           │ amazon-one-shot      │
           │ (单品深度调研)     │
           └─────────────────────┘
```

- **category-research** 回答 "哪个品类值得做"
- **store-research** 回答 "这个竞品/对标店铺做得怎么样"
- **one-shot** 回答 "这个具体产品值不值得做"

---

## 版本信息

- **版本**: 1.0.0
- **创建日期**: 2026-04-19
- **已测试店铺**: JMBricklayer
- **平台**: Amazon US (amazon.com)
- **语言**: 中文输出
