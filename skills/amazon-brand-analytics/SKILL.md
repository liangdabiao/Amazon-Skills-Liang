---
name: amazon-brand-analytics
description: "Interpret and act on Amazon Brand Analytics data. Analyze Search Frequency Rank (SFR), click share, conversion share, market basket analysis, and repeat purchase behavior to optimize your Amazon strategy."
metadata:
  nexscope:
    emoji: "📋"
    category: amazon
---

# Amazon Brand Analytics 📋

Interpret and act on Amazon Brand Analytics data. Analyze Search Frequency Rank (SFR), click share, conversion share, market basket analysis, and repeat purchase behavior to optimize your Amazon strategy.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Install

```bash
npx skills add nexscope-ai/eCommerce-Skills --skill amazon-brand-analytics -g
```

## Usage

```
Help me analyze my Amazon Brand Analytics data. My top search term has SFR #5,200 with 15% click share but only 8% conversion share. What should I do?
```

## Capabilities

- Search Frequency Rank (SFR) trend interpretation
- Click share and conversion share analysis
- Market basket analysis (frequently bought together insights)
- Repeat purchase behavior patterns
- Demographics data interpretation
- Search term performance optimization recommendations

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Search Frequency Rank (SFR) Analysis Framework

- **SFR Interpretation:** Lower number = higher search frequency. SFR #1 = most searched term on marketplace. Core value is detecting trend changes — when SFR moves from 5,000 to 2,000, demand is rapidly heating up.
- **Trend Detection:** Compare SFR across time periods. Rising SFR trend = growing demand or seasonal shift. Falling SFR = declining interest.
- **Relative vs Absolute:** SFR is a relative ranking, not absolute volume. When overall search volume spikes (e.g., Prime Day), SFR changes may not reflect true search interest changes.

### Click Share vs Conversion Share Diagnostic Model

- **Click Share > Conversion Share:** Consumers show initial interest but drop off at detail page. Root causes: listing quality, pricing, weak reviews, or delivery options.
- **Conversion Share > Click Share:** High conversion efficiency. Consider increasing ad spend to capture more clicks.
- **Gap Analysis:** Calculate difference (e.g., 15% click share with 8% conversion share = 7% leak). Larger gap = more urgent listing optimization needed.

### Market Basket Analysis Framework

- **Cross-Sell Opportunities:** Identify products frequently purchased together. Consider bundle strategies or targeted ads on complementary products.
- **Competitor Intelligence:** Analyze which competitor products appear in same basket = understand substitution patterns.
- **Association Strength:** Higher co-purchase frequency = stronger consumer behavior link. Prioritize high-frequency associations.

### Repeat Purchase Behavior Model

- **High Repeat Rate:** Products with good user experience and consumable demand (skincare, food). Suitable for Subscribe & Save to lock long-term revenue.
- **Low Repeat Rate:** May indicate quality issues or product category is one-time purchase. Compensate by expanding product line for higher customer lifetime value.

### Data Sources

- User exports CSV from Seller Central Brand Analytics dashboard.
- Requires: SFR data, click share, conversion share (minimum).
- Optional: market basket data, repeat purchase data, multiple time periods for trend analysis.
- No direct API connection to Seller Central.

### Limitations

- Brand Analytics available only to brand registry members. Data has ~72 hour delay.
- SFR is relative ranking — cannot compare directly across different overall search volume periods.
- Click/conversion share only shows top 3 brands. Lower-ranked brands need estimation.
- Market basket only shows highest frequency items — may miss low-frequency high-margin opportunities.
- Cannot distinguish why consumers drop off (price, reviews, product issues) — requires additional data inference.
- Cross-marketplace data may have different formats. Analyze each marketplace independently.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps