---
name: amazon-trending-products
description: "Discover trending products and rising categories on Amazon. Analyzes Best Seller Rank (BSR) patterns, new release momentum, seasonal trends, and emerging niches. Helps identify product opportunities before they peak."
metadata:
  nexscope:
    emoji: "📈"
    category: amazon
---

# Amazon Trending Products 📈

Discover trending products and rising categories on Amazon. Analyzes Best Seller Rank (BSR) patterns, new release momentum, seasonal trends, and emerging niches. Helps identify product opportunities before they peak.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Usage

```
What products are trending on Amazon US right now in the kitchen category? I want to find opportunities under $30.
```

## Capabilities

- BSR trend analysis and momentum scoring
- Seasonal trend identification with timing recommendations
- New release tracking and early-mover opportunity detection
- Category growth rate assessment
- Demand forecasting based on search trend patterns
- Competition density evaluation per trending niche

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### BSR Trend Analysis Engine

- **BSR Decline Velocity:** Calculate slope and acceleration of BSR drops. Sharp BSR decline = rapid sales growth. Quantify momentum strength.
- **BSR Stability Assessment:** Stable low BSR indicates established demand; volatile BSR suggests short-term hype or seasonal factors.
- **Cross-Category BSR Comparison:** Compare product BSR across different categories to identify cross-category growth potential.

### New Release Momentum Tracking Model

- **Launch Speed:** How quickly a product enters New Releases top rankings after launch. Fast entry = precisely hitting unmet demand.
- **Retention Duration:** Track how long products stay on New Releases list. Long retention = long-term potential.
- **Review Accumulation Rate:** New product review velocity signals real purchase intent.

### Seasonal Trend Identification System

- **Seasonal Factor Calculation:** Extract seasonal multipliers from multi-year sales data to quantify monthly demand volatility.
- **Lead Time Estimation:** Calculate how early procurement and inventory planning needs to start for seasonal products.
- **Anti-Seasonal Opportunity Mining:** Identify year-round products不受季节波动影响 for stable revenue.

### Emerging Niche Detection

- **New Listing Density Scan:** Sudden increase in new listings within a sub-category signals growing market attention.
- **Search Volume Growth Tracking:** Verify if a niche is truly growing by monitoring keyword search volume trends.
- **Competition Gap Identification:** Find under-served areas within growing niches for blue ocean entry points.

### Data Sources

- **Google Trends:** Get search trends and seasonal patterns for target categories.
- **Amazon Best Sellers:** Scrape BSR rankings and category structure via web_fetch.
- **Web Search:** General search for market context and industry dynamics.

### Limitations

- BSR reflects relative ranking, not absolute sales. Cross-category comparisons require calibration.
- Amazon doesn't provide real-time BSR data. Analysis is based on snapshots with time delays.
- Seasonal predictions based on historical patterns cannot predict black swan events.
- New release analysis depends on early limited data points. Confidence decreases with insufficient data.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps