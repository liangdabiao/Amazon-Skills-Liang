---
name: amazon-seller-analytics
description: "Analyze Amazon seller storefronts and product portfolios. Estimate revenue, identify top products, assess growth trajectory, and uncover strategy patterns. Useful for competitive intelligence and market research."
metadata:
  nexscope:
    emoji: "📊"
    category: amazon
---

# Amazon Seller Analytics 📊

Analyze Amazon seller storefronts and product portfolios. Estimate revenue, identify top products, assess growth trajectory, and uncover strategy patterns. Useful for competitive intelligence and market research.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Usage

```
Analyze this Amazon seller's strategy: they sell kitchen gadgets and have about 50 products. Help me understand their approach.
```

## Capabilities

- Seller storefront analysis (product count, categories, pricing strategy)
- Revenue estimation from BSR and category benchmarks
- Product portfolio assessment (hero products, long-tail, new launches)
- Review velocity and quality scoring
- Growth trajectory estimation
- Competitive positioning analysis

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Seller Storefront Structure Analysis Model

- **Product Portfolio Stratification:** Classify seller's products by sales contribution (BSR as proxy). Head products (core bestsellers), middle products (stable contributors), tail products (strategic experiments). Distribution reveals if strategy is "bestseller-driven" vs "long-tail coverage".
- **Category Span Assessment:** Analyze category coverage and inter-category relationships. Cross-category sellers have stronger supply chain integration but higher operational complexity.
- **Variation Strategy Identification:** Determine if variations are "horizontal expansion" (many variants for different preferences) or "vertical depth" (maximum quality in each variant).

### Revenue Estimation Engine

- **BSR-to-Sales Mapping Model:** Map BSR ranking to estimated monthly sales using category-specific conversion rate benchmarks. Different categories have very different BSR-to-sales relationships.
- **Category Benchmark Calibration:** Calibrate model using known reference products from industry reports or public data.
- **Price-Weighted Revenue Calculation:** Multiply estimated sales volume by current price for each product, aggregate to seller monthly revenue range (output as range to reflect uncertainty).
- **Seasonal Adjustment:** Apply seasonal factors if analysis period is off-peak season.

### Product Lifecycle Positioning

- **New Product Detection:** Identify recent launches by listing age, review count, and BSR trajectory.
- **Mature Product Identification:** Products with stable BSR, sufficient reviews, and slowing growth = profit pillars but at risk of being overtaken.
- **Declining Product Detection:** Products with continuously falling BSR, stagnant review growth = candidates for clearance or discontinuation.

### Strategy Pattern Recognition

- **Pricing Pattern:** Frequent price adjustments = automated repricing tool usage. Stable prices = brand premium positioning.
- **Advertising Intensity Inference:** Correlate BSR changes with ranking changes to infer ad dependency. Stable ranking + volatile BSR = organic traffic driven. Synchronized changes = ad-driven.
- **Launch Rhythm Analysis:** Detect if launches are burst-style or continuous, seasonal patterns.
- **Review Acquisition Strategy:** Analyze review velocity patterns to identify Vine program usage, request review features, or other legitimate review tactics.

### Data Sources

- **Amazon Seller Storefront Pages:** Scrape product listings via web_fetch — titles, prices, review counts, ratings, listing dates.
- **Product Detail Pages:** Individual BSR data requires separate web_fetch per product.
- **Built-in BSR Models:** Industry statistics and experience-based parameters for BSR-to-sales mapping.

### Limitations

- All analysis based on publicly visible information. Cannot access private operational data.
- BSR-to-sales estimates have inherent error margins (typically ±30% to ±50%).
- Large storefronts require significant data collection time (one BSR fetch per product).

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps