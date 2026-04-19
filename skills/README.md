![Amazon Skills Banner](./banner.png)

# 🔍 Amazon Skills  Liang

> ⭐ If you find these skills useful, please star the repo — it helps others discover it!

Free AI agent skills for Amazon sellers — keyword research, listing optimization, FBA calculations, PPC campaigns & more.

Works with **OpenClaw**, **Claude Code**, **Cursor**, **Windsurf**, **Codex**, and any agent that supports the [Skills format](https://skills.sh).

**Status key:** ✅ Available (production-ready) · 🔶 Beta (functional, being improved)

## Available Skills

### 🎯 All-in-One Deep Research

| Skill | Description | Status |
|-------|-------------|--------|
| [**amazon-one-shot**](../skills/amazon-one-shot/) | **One-shot comprehensive product research. Provide one ASIN → get 9 professional reports: product info extraction, keyword research, competitor analysis, review deep analysis, sales/revenue estimation, listing optimization audit, image strategy, reusable listing templates, and product selection feasibility score.** Powered by Playwright browser automation — scrapes Amazon pages in real-time, no API key needed. [→ Full README](../skills/amazon-one-shot/README.md) | ✅ Available |
| [**amazon-category-research**](../skills/amazon-category-research/SKILL.md) | **Category-level deep research. Provide an Amazon Best Sellers URL → get 5 professional reports: niche analysis, competitor landscape, keyword SEO strategy, profit analysis, and a 9-chapter comprehensive report.** Scrapes main Top 30 + 5 subcategories Top 20 (130 products total) via Playwright. 4 analysis agents run in parallel. Reports saved to `reports/{category-slug}/`. Verified: Toys & Games, Building & Construction Toys. | ✅ Available |
| [**amazon-store-research**](../skills/amazon-store-research/SKILL.md) | **Store-level deep research. Provide an Amazon Stores URL → get 5 professional reports: product portfolio, competitive positioning, revenue estimation, growth strategy, and an 8-chapter comprehensive report.** Scrapes home page, Best Sellers, New Releases, and all theme collection pages. 4 analysis agents run in parallel. Reports saved to `reports/{store-slug}/`. Verified: JMBricklayer. | ✅ Available |

---

### 🔍 Product Research & Keywords

| Skill | Description | Status |
|-------|-------------|--------|
| [amazon-keyword-research](./amazon-keyword-research/) | Long-tail keyword mining from Amazon autocomplete, competition analysis, seasonality trends, and market opportunity scoring. 12 marketplaces. | ✅ Available |
| [amazon-trending-products](./amazon-trending-products/) | Trending products and rising categories — BSR patterns, seasonal trends, emerging niches. | 🔶 Beta |
| [amazon-product-research](./amazon-product-research/) | Product research and opportunity analysis — demand, competition, profit potential, entry barriers. | 🔶 Beta |
| [amazon-niche-finder](./amazon-niche-finder/) | Profitable niche discovery — demand, competition, margins, growth potential scoring. | 🔶 Beta |
| [amazon-seller-analytics](./amazon-seller-analytics/) | Seller storefront analysis — revenue estimation, product portfolio, growth trajectory. | 🔶 Beta |

---

### 📝 Listing Optimization

| Skill | Description | Status |
|-------|-------------|--------|
| [amazon-listing-optimization](./amazon-listing-optimization/) | Create keyword-optimized listings from scratch or audit existing ones. Supports competitor ASIN analysis and 8-dimension scoring. | ✅ Available |
| [amazon-a-plus-content](./amazon-a-plus-content/) | A+ Content planning — module layouts, persuasive copy, comparison charts, image briefs. | 🔶 Beta |
| [amazon-backend-keywords](./amazon-backend-keywords/) | Backend search term optimization — 250-byte limit, deduplication, prioritization. | 🔶 Beta |
| [amazon-search-optimization](./amazon-search-optimization/) | Amazon search ranking optimization — A9 algorithm factors, indexing, rank improvement. | 🔶 Beta |
| [amazon-listing-images](./amazon-listing-images/) | Product listing image planning — shot lists, infographics, lifestyle scenes, mobile optimization. | 🔶 Beta |

---

### 🕵️ Competitor Analysis

| Skill | Description | Status |
|-------|-------------|--------|
| [amazon-competitor-analysis](./amazon-competitor-analysis/) | Full-spectrum competitor analysis — listings, pricing, reviews, ads, positioning. | 🔶 Beta |
| [amazon-brand-analytics](./amazon-brand-analytics/) | Brand Analytics interpretation — SFR, click share, conversion share, market basket. | 🔶 Beta |
| [amazon-review-analyzer](./amazon-review-analyzer/) | Deep review analysis — sentiment, complaints, feature requests, competitive insights. | 🔶 Beta |

---

### 💰 Pricing & Profitability

| Skill | Description | Status |
|-------|-------------|--------|
| [amazon-fba-calculator](./amazon-fba-calculator/) | Complete FBA fee breakdown and profit analysis. Calculate referral fees, fulfillment fees, storage costs, and net margins. | ✅ Available |
| [tariff-calculator-amazon](./tariff-calculator-amazon/) | Universal tariff calculator. Import duties, landed costs, VAT/GST for any trade route. | ✅ Available |
| [amazon-profit-analyzer](./amazon-profit-analyzer/) | Comprehensive profit analysis — revenue waterfall, hidden fees, ACoS impact, return costs, optimization. | 🔶 Beta |
| [amazon-repricing-strategy](./amazon-repricing-strategy/) | Repricing strategy — Buy Box optimization, pricing rules, margin protection, tool selection. | 🔶 Beta |
| [amazon-buy-box](./amazon-buy-box/) | Buy Box strategy — eligibility factors, competitive pricing, FBA vs FBM impact. | 🔶 Beta |
| [amazon-deal-finder](./amazon-deal-finder/) | Deal planning — Lightning Deals, Best Deals, Coupons, Prime Exclusive, ROI calculator. | 🔶 Beta |
| [amazon-shipping-calculator](./amazon-shipping-calculator/) | FBA/FBM shipping and fulfillment cost calculation — dimensional weight, storage, removal. | 🔶 Beta |

---

### 📢 Advertising

| Skill | Description | Status |
|-------|-------------|--------|
| [amazon-ppc-campaign](./amazon-ppc-campaign/) | Build PPC campaign structures or optimize existing campaigns. Calculates ACoS targets, groups keywords, sets bid strategies. | ✅ Available |
| [amazon-advertising-strategy](./amazon-advertising-strategy/) | Comprehensive ad strategy — SP + SB + SD, budget allocation, ACoS optimization. | 🔶 Beta |
| [amazon-negative-keywords](./amazon-negative-keywords/) | Negative keyword management — search term analysis, waste reduction, savings estimation. | 🔶 Beta |
| [amazon-display-ads](./amazon-display-ads/) | Sponsored Display campaigns — audience targeting, retargeting, creative optimization. | 🔶 Beta |

---

### 📊 Analytics & Monitoring

| Skill | Description | Status |
|-------|-------------|--------|
| [amazon-sales-estimator](./amazon-sales-estimator/) | Estimate monthly sales from BSR, ASIN, or keyword. Three modes: BSR Calculator, ASIN Lookup, Keyword Market Analysis. | ✅ Available |
| [amazon-rank-tracker](./amazon-rank-tracker/) | Keyword rank tracking — ranking factors, change diagnosis, improvement strategy. | 🔶 Beta |
| [amazon-keyword-tracker](./amazon-keyword-tracker/) | Keyword rank monitoring — position tracking, SERP changes, competitor movement alerts. | 🔶 Beta |
| [amazon-price-tracker](./amazon-price-tracker/) | Price monitoring — competitor pricing changes, Buy Box history, promotion detection. | 🔶 Beta |
| [amazon-product-photography](./amazon-product-photography/) | Product photography planning — shot lists, infographics, lifestyle scenes, image optimization. | 🔶 Beta |

---

### 🚀 Growth & Expansion

| Skill | Description | Status |
|-------|-------------|--------|
| [amazon-global-selling](./amazon-global-selling/) | International marketplace expansion — EU, UK, Japan, regulatory, logistics, localization. | 🔶 Beta |
| [amazon-fba-prep](./amazon-fba-prep/) | FBA prep guide — labeling, packaging, shipment planning, rejection prevention. | 🔶 Beta |

---

## 📊 Summary

| Category | ✅ Available | 🔶 Beta | Total |
|----------|:---:|:---:|:---:|
| 🎯 All-in-One Deep Research | 2 | 0 | 2 |
| 🔍 Product Research & Keywords | 1 | 4 | 5 |
| 📝 Listing Optimization | 1 | 4 | 5 |
| 🕵️ Competitor Analysis | 0 | 3 | 3 |
| 💰 Pricing & Profitability | 2 | 5 | 7 |
| 📢 Advertising | 1 | 3 | 4 |
| 📊 Analytics & Monitoring | 1 | 4 | 5 |
| 🚀 Growth & Expansion | 0 | 2 | 2 |
| **Total** | **8** | **25** | **33** |

## Quick Install

### Install all skills

> For the all-in-one deep research skill, install it directly from the `amazon-one-shot/` directory:

```bash
npx skills add ./amazon-one-shot -g
```

### Install all skills

```bash
npx skills add nexscope-ai/Amazon-Skills -g
```

### Install a specific skill

```bash
npx skills add nexscope-ai/Amazon-Skills --skill amazon-keyword-research -g
```

```bash
npx skills add nexscope-ai/Amazon-Skills --skill amazon-listing-optimization -g
```

```bash
npx skills add nexscope-ai/Amazon-Skills --skill amazon-ppc-campaign -g
```

```bash
npx skills add nexscope-ai/Amazon-Skills --skill amazon-sales-estimator -g
```

```bash
npx skills add nexscope-ai/Amazon-Skills --skill amazon-fba-calculator -g
```

```bash
npx skills add nexscope-ai/Amazon-Skills --skill tariff-calculator-amazon -g
```

## Usage

Once installed, just ask your AI agent naturally. The agent will automatically pick the right skill.

### 🎯 amazon-one-shot (All-in-One Deep Research)

```
深度调研 B07PQFT83F
```

```
deep research https://www.amazon.com/dp/B07PQFT83F
```

> Provide one ASIN or Amazon URL → get 9 reports automatically generated to `reports/{YYYY-MM-DD}_{ASIN}/`. Reports cover: product info, keywords, competitors, reviews, sales estimation, listing audit, image strategy, listing templates, and final selection score. Requires Playwright MCP for browser automation. Log in to Amazon first for deeper review analysis (40+ reviews vs 10).

### 🎯 amazon-category-research (Category Deep Research)

```
调研这个亚马逊品类：https://www.amazon.com/gp/bestsellers/toys-and-games/
```

```
分析Amazon Best Sellers Building Toys
```

> Provide an Amazon Best Sellers URL → get 5 reports automatically generated to `reports/{category-slug}/`. Reports cover: niche opportunities, competitor landscape, keyword SEO, profit analysis, and a 9-chapter comprehensive report. Scrapes main Top 30 + 5 subcategories Top 20. 4 analysis agents run in parallel. All outputs in Chinese (简体中文). Requires Playwright MCP.

### 🎯 amazon-store-research
```
调研这个亚马逊店铺：https://www.amazon.com/stores/JMBricklayer/page/...
```

```
research this Amazon store: https://www.amazon.com/stores/JMBricklayer/page/...
```

> Provide an Amazon Stores URL → get 5 reports automatically generated to `reports/{store-slug}/`. Reports cover: product portfolio, competitive positioning, revenue estimation, growth strategy, and an 8-chapter comprehensive report. Scrapes home page, Best Sellers, New Releases, and all theme collection pages. 4 analysis agents run in parallel. All outputs in Chinese (简体中文). Requires Playwright MCP.

### 🔍 amazon-keyword-research
```
Research the keyword "portable blender" on Amazon US
```

### 📝 amazon-listing-optimization
```
Create a listing for my dog t-shirt. Competitors: B0DJ5GMZHQ, B0CMD17929. Cotton, 10 colors.
```

### 📢 amazon-ppc-campaign
```
Build PPC campaigns for my product B0D72TSM62. Cost is $1.50, budget $50/day.
```

### 📊 amazon-sales-estimator
```
Estimate sales for BSR 1500 in Home & Kitchen on Amazon US
```

### 💵 amazon-fba-calculator
```
Calculate FBA fees: $15 selling price, 1.2 lbs, standard size, Home & Kitchen
```

### 🌍 tariff-calculator-amazon
```
Calculate import duties for shipping electronics from China to US. Product value $5,000.
```

## Supported Marketplaces

🇺🇸 US · 🇬🇧 UK · 🇩🇪 DE · 🇫🇷 FR · 🇮🇹 IT · 🇪🇸 ES · 🇯🇵 JP · 🇨🇦 CA · 🇦🇺 AU · 🇮🇳 IN · 🇲🇽 MX · 🇧🇷 BR

## Why Free?

These skills use publicly available data — no API key, no paid subscription, no setup friction. Install and go.

## License

MIT


