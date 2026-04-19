---
name: amazon-competitor-analysis
description: "Full-spectrum Amazon competitor analysis. Compare listings, pricing, reviews, advertising strategy, and market positioning against direct competitors. Identify weaknesses to exploit and strengths to counter."
metadata:
  nexscope:
    emoji: "🏆"
    category: amazon
---

# Amazon Competitor Analysis 🏆

Full-spectrum Amazon competitor analysis. Compare listings, pricing, reviews, advertising strategy, and market positioning against direct competitors. Identify weaknesses to exploit and strengths to counter.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Usage

```
Compare my product (ASIN B0EXAMPLE1) against these competitors: B0EXAMPLE2, B0EXAMPLE3. I sell dog beds on Amazon.
```

## Capabilities

- Listing quality comparison (title, bullets, images, A+ content)
- Review sentiment comparison and pain point extraction
- Pricing strategy analysis and positioning map
- Advertising visibility assessment (sponsored placement frequency)
- Inventory and fulfillment strategy comparison (FBA vs FBM)
- Actionable competitive counter-strategy generation

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Listing Quality Comparison Framework

- **A9/A10 SEO Scoring:** Rate each listing on title keyword coverage, bullet point information density, image quality (CTR and scene richness), and A+ content completeness.
- **Keyword Gap Analysis:** Identify which high-volume search terms competitors rank for that you don't.
- **Content Depth Evaluation:** Compare bullet points — do they address consumer pain points and selling points comprehensively?

### Review Sentiment Analysis Model

- **Complaint Theme Extraction:** Identify recurring negative themes (quality issues, sizing deviations, shipping complaints). These are your differentiation opportunities.
- **Praise Keyword Mining:** Extract high-frequency positive keywords revealing what customers value most. Use for listing copy and ad messaging.
- **Sentiment Distribution:** Compare star rating distribution across competitors. 4.5+ avg = baseline expectation you must meet.

### Pricing Positioning Map

- **Price-Review-Quality Matrix:** Plot competitors on 2D map with price and review count/rating as axes. Identify price band gaps and underserved segments.
- **Price War Detection:** Identify if market is in destructive price competition (prices near cost).

### Advertising Visibility Assessment

- **Ad Placement Frequency:** Monitor competitor sponsored ad frequency on target keywords.
- **Budget Inference:** Top ad positions on high-traffic keywords = substantial ad budget and mature strategy.
- **Low-Hanging Fruit Keywords:** Keywords with few advertisers = opportunity for cost-effective traffic.

### Data Sources

- **Amazon Product Pages:** Scrape titles, prices, bullets, images, ratings, reviews, BSR via web_fetch.
- **Web Search (site:amazon.com):** Assess competitor search visibility and ad distribution.

### Limitations

- Cannot access internal data (real ad budget, conversion rates, inventory levels).
- Ad visibility is snapshot-based. Frequent changes mean single analysis may be outdated.
- Market conditions change constantly. Regular updates needed for时效性.
- New competitors with few reviews lack statistically significant sentiment data.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps