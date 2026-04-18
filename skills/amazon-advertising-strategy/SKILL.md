---
name: amazon-advertising-strategy
description: "Build a comprehensive Amazon advertising strategy combining Sponsored Products, Sponsored Brands, and Sponsored Display. Budget allocation, campaign structure, keyword strategy, and ACoS optimization."
metadata:
  nexscope:
    emoji: "📣"
    category: amazon
---

# Amazon Advertising Strategy 📣

Build a comprehensive Amazon advertising strategy combining Sponsored Products, Sponsored Brands, and Sponsored Display. Budget allocation, campaign structure, keyword strategy, and ACoS optimization.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Install

```bash
npx skills add nexscope-ai/eCommerce-Skills --skill amazon-advertising-strategy -g
```

## Usage

```
Build an ad strategy for my Amazon product line (5 products in kitchen category). Monthly budget: $3,000. Current ACoS: 35%. Target: 25%.
```

## Capabilities

- Full-funnel ad strategy (SP + SB + SD)
- Campaign structure design (auto, broad, phrase, exact)
- Budget allocation across campaign types
- ACoS/TACoS target setting by product lifecycle stage
- Keyword harvesting and negative keyword management workflow
- Bid optimization methodology
- New product launch advertising playbook

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Full-Funnel Advertising Theory

- **SP (Sponsored Products):** Bottom of funnel —精准触达已产生明确购买意图的买家. Highest conversion rate, limited reach.
- **SB (Sponsored Brands):** Middle of funnel — guide potential buyers through brand store to understand brand. Balances awareness and conversion.
- **SD (Sponsored Display):** Full-funnel —再营销触达浏览未购买访客 + 受众定向触达竞品买家. Key for brand defense and competitor traffic capture.

### ACoS and TACoS Dual Optimization Framework

- **ACoS** = Ad Spend / Ad Revenue — measures ad campaign profitability.
- **TACoS** = Ad Spend / Total Revenue — links ad efficiency to overall business health.
- **Product Lifecycle Strategy:** New products tolerate higher ACoS for exposure; growth phase optimizes to target ACoS; mature phase focuses on TACoS control.

### Budget Allocation Marginal Revenue Principle

- Allocate budget to highest marginal revenue ad types and keywords.
- Core keywords: SP phrase/exact match has highest marginal revenue.
- Competitor defense: SD product targeting has outstanding efficiency.
- Brand building: SB video ads have strongest awareness impact.

### Keyword Harvesting Mechanism

- Continuously "harvest" high-converting search terms from broad/match and auto campaigns.
- Graduate winners to exact match single-campaign deployment.
- Add irrelevant terms to negative keyword lists.
- This dynamic cycle keeps ad spend concentrated on efficient direction.

### Data Sources

- No external API calls. All strategy based on Amazon Advertising official documentation.
- Industry benchmarks (CPC ranges, ACoS targets by category) from public industry reports.
- User provides their own ad performance data for personalized recommendations.

### Limitations

- Cannot access Amazon Ad dashboard real-time data. All recommendations are strategic frameworks.
- Amazon algorithm and rules update frequently. Strategies may need adaptation.
- Different categories have vastly different ad competition.通用策略 needs category-specific calibration.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps