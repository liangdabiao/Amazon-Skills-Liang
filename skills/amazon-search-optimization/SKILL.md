---
name: amazon-search-optimization
description: "Optimize product visibility in Amazon search results. Analyze current search ranking factors, identify optimization gaps, and provide actionable improvements for Amazon's A9/COSMO algorithm."
metadata:
  nexscope:
    emoji: "🔍"
    category: amazon
---

# Amazon Search Optimization 🔍

Optimize product visibility in Amazon search results. Analyze current search ranking factors, identify optimization gaps, and provide actionable improvements for Amazon's A9/COSMO algorithm.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Install

```bash
npx skills add nexscope-ai/eCommerce-Skills --skill amazon-search-optimization -g
```

## Usage

```
My product ranks on page 3 for my main keyword. Help me create a plan to get to page 1. Product: wireless phone charger, 150 reviews, 4.3 stars.
```

## Capabilities

- Search ranking factor analysis (relevance, performance, customer satisfaction)
- Title optimization for A9 algorithm (keyword placement, structure)
- Bullet point optimization for conversion and indexing
- Index verification methodology
- Search term harvesting from auto-campaigns
- Ranking improvement action plan with priority scoring

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### A9 Algorithm Analysis

Amazon's A9 algorithm (now evolved into comprehensive search system with COSMO semantic understanding) is core engine determining product ranking:

**Relevance Priority Principle:**
- A9 first filters products relevant to user search query.
- Relevance based on: product info (title, bullet points, backend keywords) matching search terms.
- **Keyword Weight by Position:** Title highest → Bullet points → Backend keywords.
- Keywords appearing earlier in title have higher weight.

**Sales Performance Weighting:**
- Among relevant products, A9 ranks by historical sales performance.
- Core metrics: Recent Sales Velocity (past 24-48 hours window), Conversion Rate, Click-Through Rate.
- Sales momentum (growth rate of recent sales) particularly influential — why new products need advertising/promotions to accumulate initial sales.

**Customer Satisfaction Factors:**
- Star Rating, Review Count, Return Rate.
- High rating + low return = ranking bonus; low rating + high return = ranking penalty.

### COSMO Semantic Understanding System

COSMO adds deep semantic understanding to search — traditional keyword stuffing less effective:

- **Intent Recognition:** COSMO understands consumer intent behind search queries, not just keyword matching. E.g., "birthday gift for 12 year old boy" = gift recommendation intent, not just products containing those exact words.
- **Context Analysis:** COSMO analyzes consumer browsing/purchase history context — same search may show different results to different consumers.
- **Knowledge Graph Integration:** COSMO builds product relationship knowledge graph — understands attribute relationships (e.g., "wireless earphones" same as "Bluetooth earphones").

### Index Verification Methodology

Search optimization first step = confirm product is correctly indexed by Amazon:

- **ASIN Index Detection:** Search "ASIN + product keyword" in Amazon search box — if product appears, it's indexed for that keyword.
- **Long-tail Verification Priority:** Verify lower-competition long-tail keywords first (fewer results = easier confirmation). Progress from long-tail to core keywords.
- **New Index Trigger:** Product info updates (title change, new backend keywords) require hours to days for re-indexing.

### Ranking Improvement Action Framework

- **Title Optimization:** Reposition keywords based on search volume and competition. Core principle: most important keywords first, remaining space for secondary keywords, maintain readability and brand recognition.
- **Bullet Point Dual Optimization:** Bullets affect both search indexing and conversion. Optimization covers: index coverage (ensure key search terms in bullets) AND conversion guidance (most attractive selling points first).
- **Search Term Expansion:** Mine high-converting search terms from auto campaign reports, add to backend or product info.
- **Sales Signal Activation:** Through advertising, promotions, coupons — activate sales signals short-term to drive ranking improvement. Calculate estimated sales needed for first-page ranking based on target keyword competition intensity.

### Data Sources

- web_fetch for Amazon product pages and search results.
- web_search for competitor listing info, keyword index verification.
- User provides: current ranking position, target keywords, review count, rating, product price.

### Limitations

- A9/COSMO exact ranking formulas are Amazon trade secrets — analysis based on industry research, cannot guarantee exact match with actual algorithm.
- Ranking improvement timeline and magnitude affected by uncontrollable factors — competitor optimization actions, platform algorithm adjustments, market environment changes. No guaranteed ranking improvement commitments.
- Budget estimates for sales activation based on industry averages — actual execution may vary significantly due to category competition and ad quality scores.
- Index verification based on surface observation of search results — cache delays may cause misjudgment, multiple verifications needed.
- Search optimization requires long-term sustained effort — short-term ranking fluctuations should not be over-interpreted.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps