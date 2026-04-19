---
name: amazon-niche-finder
description: "Discover profitable Amazon niches with low competition and high demand. Evaluates niche viability using demand indicators, competition metrics, profit margins, and growth potential."
metadata:
  nexscope:
    emoji: "💎"
    category: amazon
---

# Amazon Niche Finder 💎

Discover profitable Amazon niches with low competition and high demand. Evaluates niche viability using demand indicators, competition metrics, profit margins, and growth potential.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Usage

```
Help me find a profitable niche on Amazon US. I have $5000 to invest and want at least 30% margins. No electronics or supplements.
```

## Capabilities

- Niche viability scoring (demand, competition, margins, barriers)
- Sub-niche discovery from broad categories
- Competition density assessment (reviews, ratings, brand presence)
- Average revenue estimation per niche
- Seasonal vs evergreen niche classification
- Entry strategy recommendation per niche

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Demand Signal Detection System

- **Search Demand Verification:** Analyze keyword search volume, trends, and click distribution. Stable search demand = healthy niche. Focus on long-tail keyword distribution — broad demand across many terms = less fragile than single-keyword dependence.
- **Purchase Intent Signals:** Assess purchase intent by analyzing semantic features (presence of "best", "review", "buy" terms). High purchase intent = better conversion with less ad spend.
- **Review Activity Indicators:** Track monthly new reviews on existing products. Stagnant or declining reviews signal shrinking demand.
- **Cross-Platform Validation:** Cross-reference with other e-commerce platforms to validate demand beyond Amazon.

### Competition Density Assessment Model

- **Seller Count & Concentration:** Count active sellers and analyze market share distribution. Lower concentration = easier entry for new sellers.
- **Review Barrier Height:** Analyze review count distribution. If most products have <500 reviews, barrier is low and new entrants can build trust quickly. If dominated by 10K+ review products, barrier is high.
- **Brand Penetration:** Evaluate presence of strong brands with registry and trademarks. Strong brand presence = traffic advantage for incumbents.
- **Price Competition Intensity:** Analyze price distribution and margins. Price-warred niches near cost = avoid.

### Profit Margin Calculation Framework

- **Price Elasticity Analysis:** Compare sales volume and review distribution across price points. Premium niche = customers willing to pay for differentiation, not just lowest price.
- **Full Cost Breakdown:** Calculate complete cost chain: COGS, shipping, FBA fees, advertising costs.
- **Premium Opportunity Assessment:** Evaluate potential for price premium through better design, quality materials, or superior packaging.

### Growth Potential Scoring System

- **Demand Growth Trend:** Analyze historical trends in search volume, BSR, and reviews to identify if niche is growing, plateauing, or declining.
- **Scalability Assessment:** Evaluate if niche can expand through variation additions, sub-niche extensions, or adjacent market entry.
- **Evergreen vs Seasonal Classification:** Classify as "evergreen" (year-round stable demand) or "seasonal" (peaks at specific times). Match to your capital and operational capacity.

### Data Sources

- **Web Search (site:amazon.com):** Get product counts, price distribution, seller counts for macro competition data.
- **Amazon Product Pages:** Scrape BSR, reviews, ratings, monthly review velocity via web_fetch.
- **Google Trends:** Verify demand growth direction and filter false signals.

### Limitations

- Small niches lose low-competition advantage quickly when multiple sellers discover them simultaneously.
- Small niche search volumes have lower statistical confidence than broad categories.
- Profit estimates based on category averages. Actual results vary by supplier bargaining power, differentiation, and operational efficiency.
- Growth predictions based on historical trends cannot predict disruptive innovations or market changes.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps