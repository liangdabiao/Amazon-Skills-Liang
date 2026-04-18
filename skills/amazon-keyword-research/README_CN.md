# Amazon 关键词研究工具 — 原理详解

## 概述

本工具通过抓取 Amazon 搜索框的**自动补全建议**（Autocomplete Suggestions），挖掘真实买家搜索词，并结合网络搜索获取竞争分析和季节性趋势数据，最终输出市场机会评分报告。

## 核心原理

### 1. Amazon 自动补全 API

Amazon 搜索框在用户输入时会实时返回搜索建议，这些建议来自**真实用户的搜索历史聚合**，直接反映了市场需求。

**API 端点格式**：
```
https://completion.amazon.com/api/2017/suggestions?mid={市场ID}&alias=aps&prefix={编码后的关键词}
```

**参数说明**：
- `mid`：市场标识符（如美国站 `ATVPDKIKX0DER`，英国站 `A1F83G8C2ARO7P`）
- `alias=aps`：搜索所有品类（All Products）
- `prefix`：URL 编码后的搜索词

**响应示例**：
```json
{
  "suggestions": [
    {"value": "portable blender"},
    {"value": "portable blender for travel"},
    {"value": "portable blender usb rechargeable"}
  ]
}
```

### 2. 关键词扩展策略

仅搜索原始关键词只能获得少量建议。`research.sh` 使用了两种扩展策略来最大化覆盖：

**前缀扩展** — 捕获不同购买意图：
```bash
""         → "portable blender"           # 通用搜索
"best "    → "best portable blender"       # 寻找最佳产品
"cheap "   → "cheap portable blender"      # 价格敏感型
"top "     → "top portable blender"        # 排行榜导向
```

**字母后缀扩展** — 捕获长尾词：
```bash
"portable blender a" → "portable blender amazon"
"portable blender b" → "portable blender battery powered"
"portable blender c" → "portable blender cup"
...
"portable blender z" → "portable blender with straw"
```

通过 3 个前缀 × 1 个原始 + 26 个字母后缀，共发起 **29 次 API 请求**，去重后通常能获取 100-200 个独特关键词。

### 3. 多站点支持

12 个 Amazon 站点通过域名和市场 ID 映射实现：

| 站点 | 域名 | 市场 ID |
|------|------|---------|
| 美国 | amazon.com | ATVPDKIKX0DER |
| 英国 | amazon.co.uk | A1F83G8C2ARO7P |
| 德国 | amazon.de | A1PA6795UKMFR9 |
| 日本 | amazon.co.jp | A1VC38T7YXB528 |
| ... | ... | ... |

不同站点的自动补全数据反映当地消费者的搜索习惯和语言差异。

### 4. 数据处理流程

```
种子关键词
    ↓
前缀扩展 + 字母扩展（29次API请求）
    ↓
JSON 解析，提取 suggestions[].value
    ↓
去重 + 排序
    ↓
按购买意图分类：
  ├── 高商业意图（含 buy, best, for, vs 等）
  ├── 信息研究型（含 how to, what is, review 等）
  └── 垂直细分型（长且具体的搜索词）
```

### 5. 竞争分析原理

通过搜索引擎获取竞争情报：
- 搜索 `"关键词" site:amazon.com` → 估算竞争商品数量
- 搜索 `"关键词" amazon best sellers price review` → 提取价格区间、评分、头部品牌

### 6. 季节性分析

通过 Google Trends 数据识别：
- 趋势方向（上升/下降/稳定）
- 季节性峰值月份
- 同比变化

### 7. 市场机会评分（1-10分）

综合四个维度加权评分：
- **竞争密度**：竞争对手数量和品牌集中度
- **价格空间**：是否存在足够的利润空间
- **需求趋势**：需求是增长还是萎缩
- **细分潜力**：是否可以通过差异化切入

## 使用方法

```bash
# 基本用法
bash scripts/research.sh "portable blender" us

# 指定站点
bash scripts/research.sh "yoga mat" de
bash scripts/research.sh "blender" jp
```

## 技术实现

- `research.sh`：Bash 脚本，依赖 `curl` 和 `python3`（用于 URL 编码和 JSON 解析）
- JSON 解析通过 Python 内联单行代码实现，无需额外安装
- 所有数据来自公开接口，**无需 API Key**

## 数据来源

本技能的核心数据来源是Amazon自动补全API（`completion.amazon.com/api/2017/suggestions`），通过 `curl` 直接调用该公开接口获取搜索建议。API请求格式为 `?mid={市场ID}&alias=aps&prefix={编码后的关键词}`，其中 `mid` 参数标识目标市场（如美国站为 `ATVPDKIKX0DER`，英国站为 `A1F83G8C2ARO7P`）。12个Amazon站点各有独立的域名和市场ID映射。单次关键词研究共发起29次API请求——3个前缀（空字符串、`best `、`cheap `）加26个字母后缀，JSON响应中的 `suggestions[].value` 字段经Python内联代码解析后提取为关键词列表。

此外，本技能还使用两个辅助数据源：通过Google Trends（`trends.google.com`）获取关键词的季节性趋势数据（趋势方向、峰值月份、同比变化）；通过通用搜索引擎（`web_search`）获取竞争情报，搜索 `"关键词" site:amazon.com` 估算竞争商品数量，搜索 `"关键词" amazon best sellers price review` 提取价格区间和头部品牌信息。所有数据来自公开接口，无需API Key。

## 局限性

- 自动补全词**不等于搜索量**，仅代表存在搜索行为
- 无法获取精确的月搜索量数据
- 竞争分析依赖搜索引擎，精度有限
- Amazon 可能限制高频请求，大规模研究需注意请求频率
