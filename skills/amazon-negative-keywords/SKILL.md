---
name: amazon-negative-keywords
description: "Optimize Amazon PPC campaigns by identifying and managing negative keywords. Reduce wasted ad spend by eliminating irrelevant search terms while protecting valuable converting terms."
metadata:
  nexscope:
    emoji: "🚫"
    category: amazon
---

# Amazon Negative Keywords 🚫

Optimize Amazon PPC campaigns by identifying and managing negative keywords. Reduce wasted ad spend by eliminating irrelevant search terms while protecting valuable converting terms.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Install

```bash
npx skills add nexscope-ai/Amazon-Skills --skill amazon-negative-keywords -g
```

## Usage

```
Analyze my Amazon search term report. I'm spending $2,000/month on PPC with 40% ACoS. Help me find negative keywords to cut waste.
```

## Capabilities

- Search term report analysis for negative keyword candidates
- Negative keyword categorization (irrelevant, low-converting, competitor)
- Campaign-level vs ad-group-level negative targeting strategy
- Negative phrase vs negative exact match decision framework
- Estimated savings calculation from negative keyword implementation
- Ongoing negative keyword management workflow

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Search Term Efficiency Stratification

Four tiers based on conversion efficiency:
1. **High-Conversion Core Keywords:** Directly drive sales. Protect and increase bid.
2. **Low-Frequency Precision Keywords:** Some conversion, low click volume. Continue observing.
3. **Weak-Relevance Occasional Converters:** Low conversion but occasional sales. Evaluate based on CPC vs conversion value.
4. **Completely Irrelevant Waste Keywords:** Must immediately add as negatives.

Framework: classify each search term from the search term report into appropriate tier.

### Negative Exact vs Negative Phrase Matching Logic

- **Negative Exact:** Only blocks exact matching search term from triggering ads.
- **Negative Phrase:** Blocks all search variations containing the term.
- **Decision Rule:** Use negative exact for single waste terms. Use negative phrase for categories of irrelevant searches.
- **Example:** "free" as phrase negative blocks "free shipping", "buy free", "totally free" — captures all "free" related waste.

### Campaign-Level vs Ad Group-Level Negative Strategy

- **Campaign-Level Negatives:** Apply to all ad groups under campaign. Use for terms irrelevant to entire product line.
- **Ad Group-Level Negatives:** Only affect specific ad group. Use for fine-tuning across different match types.
- **Strategy Example:**
  - Exact match ad group: negative phrase for core keywords already separately targeted
  - Broad match ad group: stay open to continuously discover new search terms

### Savings Estimation Model

**Estimated Savings = Irrelevant Search Spend - Potential Lost Conversion Value**

Before implementing each negative, evaluate net savings effect. Ensure negative action's benefit exceeds potential loss.

### Ongoing Management Framework

- **Review Frequency:** Weekly search term report review recommended.
- **Seasonal/Temporary Negatives:** Negatives added for seasonal promotions should be removed after promotion ends.
- **Keyword Harvesting Workflow:** Continuously "harvest" high-converting terms from broad/auto campaigns and graduate to exact match.

### Data Sources

- User exports Search Term Report from Amazon Seller Central (recommended: 14-30 days minimum).
- Report contains: search terms, clicks, spend, conversions, ACoS.
- No direct API connection to Seller Central.

### Limitations

- Report data completeness and accuracy directly impacts analysis reliability.
- Search term report has ~72 hour data delay.
- Amazon hides some low-frequency search terms — not all waste spend visible.
- Effects take time to manifest — short-term ACoS improvement may not be noticeable.
- Search term intent is dynamic — terms irrelevant now may become high converters later (seasonal, trends). Regular review needed.
- Cannot directly connect to Amazon Ad dashboard — relies on user-provided data.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps