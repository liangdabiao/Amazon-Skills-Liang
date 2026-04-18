# Amazon Skills 中文总览

> 免费AI智能体技能合集，专为亚马逊卖家打造。涵盖关键词研究、Listing优化、FBA费用计算、PPC广告投放等52项核心能力。无需API Key，安装即用。

## 按类别总览

---

### 🔍 产品研究与关键词

| 技能 | 状态 | 核心能力 |
|------|------|----------|
| [amazon-keyword-research](./amazon-keyword-research/README_CN.md) | ✅ 可用 | 通过Amazon自动补全API挖掘长尾关键词，结合竞争分析和季节性趋势，输出市场机会评分 |
| [amazon-trending-products](./amazon-trending-products/README_CN.md) | 🔶 Beta | 基于BSR趋势分析、新品势能追踪和季节性预测，发现上升趋势中的产品和品类 |
| [amazon-product-research](./amazon-product-research/README_CN.md) | 🔶 Beta | 从需求、竞争、利润、壁垒四个维度评估产品机会，使用HHI指数量化竞争强度 |
| [amazon-niche-finder](./amazon-niche-finder/README_CN.md) | 🔶 Beta | 综合需求信号、竞争密度、利润空间和增长潜力评分，筛选低竞争高需求的利基市场 |
| [amazon-seller-analytics](./amazon-seller-analytics/README_CN.md) | 🔶 Beta | 分析卖家店铺结构，通过BSR估算营收，识别产品生命周期和运营策略模式 |

**原理要点**：关键词研究类工具的核心数据源是Amazon公开的自动补全API（`completion.amazon.com`），该API返回的搜索建议直接来自真实买家的搜索行为聚合，是零成本的需求数据来源。通过前缀扩展和字母后缀扩展策略，可将单个种子关键词扩展为100-200个长尾词。

---

### 📝 Listing优化

| 技能 | 状态 | 核心能力 |
|------|------|----------|
| [amazon-listing-optimization](./amazon-listing-optimization/README_CN.md) | ✅ 可用 | 双模式（创建/优化）Listing引擎，基于A9算法关键词权重分布生成文案，8维度审计评分 |
| [amazon-a-plus-content](./amazon-a-plus-content/README_CN.md) | 🔶 Beta | 策划A+内容模块布局，设计说服链路，生成对比图表和图片需求文档 |
| [amazon-backend-keywords](./amazon-backend-keywords/README_CN.md) | 🔶 Beta | 在250字节限制内最大化关键词覆盖率，实现三级去重（精确/词根/语义）和拼写变体覆盖 |
| [amazon-search-optimization](./amazon-search-optimization/README_CN.md) | 🔶 Beta | 解析A9/COSMO算法排名因素（相关性、销量、满意度），提供索引验证和排名提升方案 |
| [amazon-listing-images](./amazon-listing-images/README_CN.md) | 🔶 Beta | 七张图片战略规划，信息图表设计原理，生活场景拍摄需求，移动端显示优化 |

**原理要点**：Amazon搜索排名的核心是A9算法，其关键词权重分布为：标题 > 卖点 > 描述 > 后台搜索词。Listing优化的本质是将目标关键词按优先级分配到对应位置，实现最大覆盖率。8维度审计体系（满分100分）量化了Listing质量，其中SEO覆盖率占10分。

---

### 🕵️ 竞争分析

| 技能 | 状态 | 核心能力 |
|------|------|----------|
| [amazon-competitor-analysis](./amazon-competitor-analysis/README_CN.md) | 🔶 Beta | 全维度竞品对比——Listing质量、评论情感、定价策略、广告可见度和市场定位 |
| [amazon-brand-analytics](./amazon-brand-analytics/README_CN.md) | 🔶 Beta | 解读品牌分析数据——搜索频率排名(SFR)、点击份额vs转化份额差距诊断、购物篮分析 |
| [amazon-review-analyzer](./amazon-review-analyzer/README_CN.md) | 🔶 Beta | 从评论中提取情感模式、重复投诉、功能需求和竞品洞察，转化为产品改进优先级矩阵 |

**原理要点**：品牌分析中"点击份额高但转化份额低"是最关键的诊断信号——说明你的Listing被看到了但没能说服买家，需要优化图片、价格或评论。购物篮分析（"经常一起购买"）揭示交叉销售机会。

---

### 💰 定价与利润

| 技能 | 状态 | 核心能力 |
|------|------|----------|
| [amazon-fba-calculator](./amazon-fba-calculator/README_CN.md) | ✅ 可用 | 基于产品尺寸/重量自动判定尺寸等级，精确计算全部FBA费用（配送费、仓储费、长期仓储费、佣金）及利润分析 |
| [tariff-calculator-amazon](./tariff-calculator-amazon/README_CN.md) | ✅ 可用 | 通用关税与到岸成本计算——HS编码查询、Section 301附加税、VAT/GST、贸易协定优惠、完整成本链 |
| [amazon-profit-analyzer](./amazon-profit-analyzer/README_CN.md) | 🔶 Beta | 收入瀑布模型——从营收到净利润的完整费用链拆解，含隐藏费用识别（长期仓储、移除、优惠券成本） |
| [amazon-repricing-strategy](./amazon-repricing-strategy/README_CN.md) | 🔶 Beta | 基于Buy Box算法的价格调整规则设计——底价/天花板价、竞品响应策略、分时段定价 |
| [amazon-buy-box](./amazon-buy-box/README_CN.md) | 🔶 Beta | Buy Box多因素评分算法分析——价格权重、FBA结构性优势、卖家绩效指标和库存充足率 |
| [amazon-deal-finder](./amazon-deal-finder/README_CN.md) | 🔶 Beta | 四种促销类型ROI对比（秒杀/镇店之宝/优惠券/Prime专享），叠加策略风险与收益计算 |
| [amazon-shipping-calculator](./amazon-shipping-calculator/README_CN.md) | 🔶 Beta | FBA完整费用计算（体积重量、月度仓储、长期仓储、移除费）与FBA vs FBM决策框架 |

**原理要点**：FBA费用计算的核心是尺寸分级——产品被归入6个等级（小标/大标/小超大/中超大/大超大/特殊超大），每个等级对应完全不同的配送费率。体积重量公式为 `(长×宽×高)/139`，当体积重量超过实际重量的1.5倍时，优化包装尺寸是最有效的降本手段。关税计算的核心公式为：到岸成本 = FOB + 运费 + 保险 + 进口关税 + VAT/GST + 各项杂费。

---

### 📢 广告投放

| 技能 | 状态 | 核心能力 |
|------|------|----------|
| [amazon-ppc-campaign](./amazon-ppc-campaign/README_CN.md) | ✅ 可用 | PPC完整策略引擎——ACoS财务框架（盈亏平衡/目标ACoS/最大CPC）、4层广告架构、关键词漏斗模型 |
| [amazon-advertising-strategy](./amazon-advertising-strategy/README_CN.md) | 🔶 Beta | 全漏斗广告策略（SP+SB+SD），预算边际收益分配，产品生命周期ACoS目标设定 |
| [amazon-negative-keywords](./amazon-negative-keywords/README_CN.md) | 🔶 Beta | 搜索词效率分层筛选，否定精准vs否定词组选择逻辑，节省金额预估模型 |
| [amazon-display-ads](./amazon-display-ads/README_CN.md) | 🔶 Beta | SD广告策略——受众重定向漏斗回收、竞品商品页拦截、情境定位与受众定位互补 |
| [amazon-dayparting-strategy](./amazon-dayparting-strategy/README_CN.md) | 🔶 Beta | 分时投放策略——消费者购物时段行为模式、时段转化率差异与竞价调整 |

**原理要点**：PPC优化的基石是三个公式：盈亏平衡ACoS = 利润率，目标ACoS = 盈亏平衡ACoS - 期望利润率，最大CPC = 售价 × 目标ACoS × 转化率。关键词漏斗（Auto → Broad → Exact）是核心优化循环，每上移一级必须在原广告中添加否定词以防止内部竞价。

---

### 📊 数据分析与监控

| 技能 | 状态 | 核心能力 |
|------|------|----------|
| [amazon-sales-estimator](./amazon-sales-estimator/README_CN.md) | ✅ 可用 | 基于BSR的销量估算——幂律分布模型、品类系数和站点系数修正、市场集中度分析 |
| [amazon-rank-tracker](./amazon-rank-tracker/README_CN.md) | 🔶 Beta | 关键词排名追踪与排名变动归因诊断（相关性/销量/转化率/评论/库存因素） |
| [amazon-keyword-tracker](./amazon-keyword-tracker/README_CN.md) | 🔶 Beta | SERP动态分析，统计基线方法区分正常波动与异常排名变化 |
| [amazon-price-tracker](./amazon-price-tracker/README_CN.md) | 🔶 Beta | Buy Box动态竞争博弈分析，促销检测与影响评估，历史价格周期模式识别 |

**原理要点**：BSR与销量呈幂律反比关系（非线性衰减），通过品类系数（电子产品1.2x、服装0.8x等）和站点系数（美国1.0x、日本0.6x等）修正后可得到相对可靠的估算值。市场集中度分析判断机会：Top 3占比 < 30% 为碎片化市场，新卖家有进入空间。

---

### 🚀 增长与运营

| 技能 | 状态 | 核心能力 |
|------|------|----------|
| [amazon-global-selling](./amazon-global-selling/README_CN.md) | 🔶 Beta | 国际站点拓展规划——市场评估、各国法规合规（CE/UKCA/PSE认证）、物流模式对比、本地化策略 |
| [amazon-fba-prep](./amazon-fba-prep/README_CN.md) | 🔶 Beta | FBA入库准备——FNSKU标签规范、包装合规、装箱优化、常见拒收原因规避 |
| [amazon-brand-registry](./amazon-brand-registry/README_CN.md) | 🔶 Beta | 品牌注册指南——商标资格、审核流程、三层品牌保护体系、A+内容权限解锁 |
| [amazon-brand-tailored-promotions](./amazon-brand-tailored-promotions/README_CN.md) | 🔶 Beta | 品牌定制促销——买家受众细分、差异化折扣、竞品流量拦截 |
| [amazon-category-ungating](./amazon-category-ungating/README_CN.md) | 🔶 Beta | 类目解锁——风险分级管理、资质验证、各品类审核标准 |
| [amazon-coupon-strategy](./amazon-coupon-strategy/README_CN.md) | 🔶 Beta | 促销策略——优惠券展示机制、叠加风险计算、各工具费用结构对比 |
| [amazon-enhanced-brand-content](./amazon-enhanced-brand-content/README_CN.md) | 🔶 Beta | 高级A+与品牌故事——视觉层级设计、生活化场景营销、产品对比图表 |
| [amazon-international-listings](./amazon-international-listings/README_CN.md) | 🔶 Beta | 多站点Listing管理——BIL同步机制、本地化翻译、跨市场定价 |
| [amazon-inventory-management](./amazon-inventory-management/README_CN.md) | 🔶 Beta | FBA库存管理——补货时机模型、安全库存公式、IPI四维度优化、滞留库存恢复 |
| [amazon-private-label](./amazon-private-label/README_CN.md) | 🔶 Beta | 自有品牌发售——蓝海选品、品牌资产构建、供应商管理、差异化竞争 |
| [amazon-product-bundling](./amazon-product-bundling/README_CN.md) | 🔶 Beta | 捆绑销售——虚拟捆绑机制、多件装阶梯定价、搜索权重叠加效应 |
| [amazon-product-compliance](./amazon-product-compliance/README_CN.md) | 🔶 Beta | 产品合规——各国认证体系（FDA/CE/PSE）、标签规范、受限物质管控 |
| [amazon-product-photography](./amazon-product-photography/README_CN.md) | 🔶 Beta | 产品摄影——拍摄清单、灯光布置、信息图表简报、生活场景规划 |
| [amazon-return-reduction](./amazon-return-reduction/README_CN.md) | 🔶 Beta | 退货率降低——根因分析法、Listing准确性管理、包装改进、尺码指南优化 |
| [amazon-review-strategy](./amazon-review-strategy/README_CN.md) | 🔶 Beta | 评论获取策略——Request a Review自动化、跟进邮件合规、Vine计划机制 |
| [amazon-seasonal-planning](./amazon-seasonal-planning/README_CN.md) | 🔶 Beta | 季节性规划——年度销售日历、库存前置时间管理、促销提报、广告季节性调整 |
| [amazon-storefront-design](./amazon-storefront-design/README_CN.md) | 🔶 Beta | 品牌店铺设计——页面布局、品牌故事、可购物图片、流量引导、转化优化 |
| [amazon-subscribe-save](./amazon-subscribe-save/README_CN.md) | 🔶 Beta | 订阅省钱优化——折扣阶梯、配送频率优化、留存分析 |
| [amazon-suspension-appeal](./amazon-suspension-appeal/README_CN.md) | 🔶 Beta | 账号申诉——政策违规分析、行动计划（POA）编写、恢复流程 |
| [amazon-variation-strategy](./amazon-variation-strategy/README_CN.md) | 🔶 Beta | 变体策略——父子ASIN合并/拆分规则、颜色/尺寸变体、排名权重共享机制 |
| [amazon-vine-program](./amazon-vine-program/README_CN.md) | 🔶 Beta | Vine评论计划——产品选择、时机策略、评论质量最大化 |
| [amazon-wholesale-sourcing](./amazon-wholesale-sourcing/README_CN.md) | 🔶 Beta | 批发选品——供应商发现、谈判策略、MOQ优化、利润率分析 |

---

## 技能架构说明

本项目所有技能遵循统一的 [Skills 格式](https://skills.sh)，兼容以下AI智能体平台：

- **OpenClaw** / **Claude Code** / **Cursor** / **Windsurf** / **Codex**

### 技能结构

```
amazon-[skill-name]/
├── SKILL.md          # 技能定义（frontmatter + 使用文档 + 工作流）
├── _meta.json        # 元数据（可选）
└── scripts/          # 脚本（可选）
    ├── *.py          # Python计算脚本
    └── *.sh          # Bash数据采集脚本
```

### 两大类型

| 类型 | 特征 | 代表技能 |
|------|------|----------|
| **脚本驱动型** | 含Python/Bash脚本，提供实际计算和数据采集能力 | fba-calculator, keyword-research, tariff-calculator |
| **Prompt驱动型** | 纯AI策略指导，依赖公开数据和用户输入 | listing-optimization, ppc-campaign, sales-estimator |

### 安装方式

```bash
# 安装全部技能
npx skills add nexscope-ai/Amazon-Skills -g

# 安装单个技能
npx skills add nexscope-ai/Amazon-Skills --skill amazon-fba-calculator -g
```

## 数据来源说明

本项目所有技能**无需付费API Key**，数据来自以下公开渠道和内置数据集：

### 一、Amazon 公开接口（脚本直接调用）

| 数据源 | 端点/方式 | 获取的数据 | 使用该数据的技能 |
|--------|----------|-----------|----------------|
| **Amazon 自动补全API** | `https://completion.{domain}/api/2017/suggestions?mid={市场ID}&alias=aps&prefix={关键词}` | 真实买家的搜索建议词（长尾关键词） | keyword-research, ppc-campaign, listing-optimization |
| **Amazon 商品页面** | `https://{domain}/dp/{ASIN}` | 标题、价格、BSR排名、评分、评论数、图片数、品类、卖点 | listing-optimization（fetch-listing.sh）、ppc-campaign（fetch-competitor.sh）、sales-estimator |
| **Amazon 搜索结果页** | `https://{domain}/s?k={关键词}` | 搜索结果中的竞品列表、价格分布、广告位 | product-research, niche-finder, competitor-analysis |

**自动补全API 工作原理**：Amazon搜索框在用户输入时实时返回搜索建议，数据来自真实买家搜索行为的聚合。通过前缀扩展（`best`、`cheap`、`top`）和字母后缀扩展（`a`-`z`），单次查询可扩展为29次API请求，去重后获取100-200个独特关键词。

**商品页面抓取原理**：Bash脚本通过 `curl` 请求商品页面HTML，使用 `grep` 正则提取结构化数据（BSR、价格、标题等）。支持12个站点，通过域名和市场ID映射实现。

### 二、第三方公开数据（AI智能体间接调用）

| 数据源 | 访问方式 | 获取的数据 | 使用该数据的技能 |
|--------|----------|-----------|----------------|
| **Google Trends** | `https://trends.google.com/trends/explore?q={关键词}&geo={国家}` | 12个月搜索趋势、季节性峰值、同比变化 | keyword-research（季节性分析）、trending-products |
| **通用搜索引擎** | AI智能体的 `web_search` 能力 | 竞品情报、市场概况、品类分析、行业数据 | product-research, competitor-analysis, niche-finder, seller-analytics |
| **网页抓取** | AI智能体的 `web_fetch` 能力 | 特定网页内容（Amazon页面、行业报告等） | sales-estimator, listing-optimization, review-analyzer |

### 三、内置数据集（硬编码在脚本中）

| 数据集 | 内容 | 数据规模 | 使用该数据的技能 |
|--------|------|----------|----------------|
| **Amazon FBA 费率表** | 2024年美国站配送费（6个尺寸等级）、月度仓储费（标准季/旺季）、长期仓储费、移除费、销售佣金（20+品类） | ~30条费率规则 | fba-calculator, shipping-calculator |
| **HS 编码数据库** | 24个常见跨境电商产品的HS编码、中英文描述、Section 301附加税率 | 24条编码 + 关键词映射 | tariff-calculator（hs_lookup.py） |
| **关税税率表** | 11个HS章节的基础关税率（5个目的国）、Section 301附加税率（14个HS税号）、VAT/GST税率（5国+欧盟6国）、6个贸易协定 | ~50条税率规则 | tariff-calculator（calculator.py） |
| **BSR-销量对照表** | 美国站Home & Kitchen品类的BSR区间→月销量估算值、7个品类系数、7个站点系数 | ~20条参考数据 | sales-estimator |

### 四、用户自行提供的数据

| 数据类型 | 来源 | 用途 |
|----------|------|------|
| **产品成本/尺寸/重量** | 卖家内部数据 | fba-calculator, profit-analyzer, shipping-calculator 的计算输入 |
| **PPC广告数据** | Seller Central 广告管理后台导出 | ppc-campaign 优化、negative-keywords 分析、dayparting 策略 |
| **搜索词报告** | Seller Central 广告→搜索词报告 | ppc-campaign 优化模式的核心数据 |
| **竞品ASIN** | 卖家自行收集或通过搜索发现 | listing-optimization、competitor-analysis、ppc-campaign 的竞品分析输入 |
| **商品评论** | Amazon公开页面 | review-analyzer 的分析对象 |
| **品牌分析数据** | Seller Central → 品牌分析（需品牌注册） | brand-analytics 的解读对象 |

### 数据可靠性说明

| 数据类型 | 可靠性 | 说明 |
|----------|--------|------|
| Amazon 自动补全词 | ⭐⭐⭐⭐ 高 | 直接来自Amazon搜索引擎，反映真实搜索行为，但不等于搜索量 |
| 商品页面数据（BSR/价格） | ⭐⭐⭐ 中 | 实时快照，BSR每小时更新，但无法获取历史趋势 |
| FBA费率表 | ⭐⭐⭐⭐ 高 | 来自Amazon官方公开费率表，但每年可能调整 |
| 关税税率 | ⭐⭐⭐ 中 | 章节级近似值，精确税率需HS 10位编码查询 |
| BSR-销量估算 | ⭐⭐ 低 | 统计估算值，Amazon不公开实际销量，误差可能达30-50% |
| Google Trends | ⭐⭐⭐ 中 | 相对趋势准确，绝对值不可靠，部分关键词数据稀疏 |

## 支持的站点

🇺🇸 美国 · 🇬🇧 英国 · 🇩🇪 德国 · 🇫🇷 法国 · 🇮🇹 意大利 · 🇪🇸 西班牙 · 🇯🇵 日本 · 🇨🇦 加拿大 · 🇦🇺 澳大利亚 · 🇮🇳 印度 · 🇲🇽 墨西哥 · 🇧🇷 巴西

## 许可证

MIT License
