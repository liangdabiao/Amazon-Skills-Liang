---
name: amazon-product-research
description: "Comprehensive Amazon product research and opportunity analysis. Evaluate market demand, competition intensity, profit potential, and entry barriers for any product category or niche. Uses BSR data, review analysis, and pricing patterns."
metadata:
  nexscope:
    emoji: "🔎"
    category: amazon
---

# Amazon Product Research 🔎

Comprehensive Amazon product research and opportunity analysis. Evaluate market demand, competition intensity, profit potential, and entry barriers for any product category or niche. Uses BSR data, review analysis, and pricing patterns.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Install

```bash
npx skills add nexscope-ai/eCommerce-Skills --skill amazon-product-research -g
```

## Usage

```
I want to sell silicone kitchen utensils on Amazon. Is this a good market? What's the competition like?
```

## Capabilities

- Market demand estimation using BSR and category benchmarks
- Competition intensity scoring (number of sellers, review counts, brand dominance)
- Profit potential calculation including FBA fees and advertising costs
- Entry barrier assessment (capital required, IP risks, certification needs)
- Product differentiation opportunity identification from review gaps
- Seasonal demand pattern analysis

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Market Demand Quantification Model

- **BSR Benchmarking:** Map BSR distribution to estimated sales volume. Collect products across BSR tiers (Top 100, 100-500, 500-2000), calculate average BSR per tier, apply conversion rate benchmarks to estimate monthly sales per tier, then aggregate for total category demand.
- **Search Volume Analysis:** Analyze core keyword search frequency distributions to assess demand breadth and depth. Determine if category is in introduction, growth, or maturity phase.
- **Review Velocity:** Track monthly new reviews on multiple products to validate BSR demand trends against actual purchase behavior.

### Competition Intensity Framework

- **Seller Concentration (HHI):** Calculate Herfindahl-Hirschman Index to quantify seller concentration. Higher HHI = more monopolized = harder for new entrants.
- **Review Barrier Calculation:** Assess how many reviews the top products have and estimate the time/cost for a new product to build competitive review base.
- **Price Competition Analysis:** Calculate average selling price, median price, and price standard deviation. Identify if category is in price war red ocean.
- **Brand Barrier Identification:** Evaluate presence of strong brands with brand registry, patents, or trademarks.

### Profit Potential Calculation Engine

- **FBA Fee Estimation:** Calculate exact fees based on product dimensions, weight, and category: fulfillment fees, monthly storage, long-term storage.
- **Advertising Cost Simulation:** Model ad spend and ACoS based on keyword bid levels and estimated CTR for the category.
- **Return Loss Estimation:** Factor in historical return rates, return shipping costs, and restocking fees.
- **Dynamic Profit Curves:** Generate profit curves across different sales volumes to understand profitability at different growth stages.

### Entry Barrier Assessment

- **Capital Requirement:** Calculate minimum funding needed: initial inventory, shipping, FBA storage, advertising budget, operational runway.
- **Compliance Requirements:** Identify required certifications (FDA, CE, UL, etc.) and their timeline/cost.
- **IP Risk Analysis:** Check existing patents and trademarks in the category for infringement risks.

### Data Sources

- **Amazon Product Pages:** Scrape BSR, price, review count, and ratings via web_fetch.
- **Google Trends:** Get seasonal demand patterns.
- **Keyword Search:** Use web_search with site:amazon.com to assess competition scope.
- **Built-in FBA Calculator:** Use amazon-fba-calculator for fee breakdowns.

### Limitations

- BSR-to-sales model is statistical estimation, not official Amazon data. Accuracy degrades with smaller sample sizes.
- Competition analysis cannot access internal data (ad spend, actual conversion rates, repeat purchase rates).
- Profit estimates use category average for ad costs and return rates. Actual results may vary significantly.
- IP risk analysis cannot cover trade secrets or unpublished patent applications.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps