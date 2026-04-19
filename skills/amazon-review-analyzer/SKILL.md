---
name: amazon-review-analyzer
description: "Deep-dive Amazon review analysis. Extract sentiment patterns, recurring complaints, feature requests, and competitive insights from product reviews. Turn customer feedback into product improvement and marketing opportunities."
metadata:
  nexscope:
    emoji: "💬"
    category: amazon
---

# Amazon Review Analyzer 💬

Deep-dive Amazon review analysis. Extract sentiment patterns, recurring complaints, feature requests, and competitive insights from product reviews. Turn customer feedback into product improvement and marketing opportunities.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Usage

```
Analyze the reviews for my competitor's yoga mat (has 2,500 reviews, 4.2 stars). What are customers complaining about that I can fix in my product?
```

## Capabilities

- Sentiment analysis across star ratings (positive/negative/neutral themes)
- Recurring complaint identification and severity ranking
- Feature request extraction from customer language
- Competitor review comparison (what customers like about alternatives)
- UGC (user-generated content) mining for marketing copy
- Review-based product improvement priority matrix

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Multi-Dimensional Sentiment Analysis Model

- **Star-Rating Stratification:** Analyze reviews by star tier (1-2 star negative, 3 star neutral, 4-5 star positive). Within each tier, identify specific sentiment themes (e.g., 5-star reviews may praise "quality", "packaging", or "customer service" for different reasons).
- **Complaint Severity Ranking:** Rank complaints by frequency, severity (returns, A-to-Z claims), and distribution pattern (isolated vs systemic). High-frequency systemic complaints = top priority.
- **Implicit Feature Request Mining:** Extract implicit desires from review language: "wish it came with a storage bag", "if only it were slightly bigger" — these reveal product improvement directions.

### Competitor Review Comparison Framework

- Identify what competitors' customers praise repeatedly = benchmark for your product.
- Find where competitors' customers complain = your differentiation opportunities.
- Map competitive positioning based on review themes.

### UGC (User-Generated Content) Extraction

- Extract compelling customer phrases from positive reviews for marketing copy.
- Identify viral review patterns for listing optimization.
- Find emotional trigger words that resonate with buyers.

### Improvement Priority Matrix

- Plot identified issues/opportunities on Impact vs Implementation Difficulty matrix.
- High impact + low difficulty = quick wins.
- High impact + high difficulty = strategic priorities.

### Data Sources

- **Amazon Review Pages:** Scrape review content, titles, dates, and reviewer info via web_fetch.
- **Note:** Amazon pages load limited reviews per page. Large sample analysis may require multiple paginated fetches.

### Limitations

- Analysis quality depends on review quantity. Products with <50 reviews have low statistical significance.
- Some fake/suspicious reviews may exist despite Amazon filtering.
- Consumers tend to leave extreme reviews (very satisfied or very dissatisfied). Middle ground voices may be under-represented.
- Implicit feature requests are often vague and fragmented. Requires product domain knowledge to translate into actionable improvements.
- Review data reflects post-purchase experience only. No insight into pre-purchase drop-off reasons (price, images, titles).

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps