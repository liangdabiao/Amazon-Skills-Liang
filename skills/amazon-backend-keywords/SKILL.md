---
name: amazon-backend-keywords
description: "Optimize Amazon backend search terms for maximum discoverability. Generate the optimal 250-byte backend keyword set by deduplicating, prioritizing, and formatting keywords that aren't already in your listing."
metadata:
  nexscope:
    emoji: "🏷️"
    category: amazon
---

# Amazon Backend Keywords 🏷️

Optimize Amazon backend search terms for maximum discoverability. Generate the optimal 250-byte backend keyword set by deduplicating, prioritizing, and formatting keywords that aren't already in your listing.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Install

```bash
npx skills add nexscope-ai/eCommerce-Skills --skill amazon-backend-keywords -g
```

## Usage

```
Optimize my backend keywords. My product is a bamboo laptop stand. Here are my current title and bullets: [paste listing]. Here are 50 keyword candidates: [paste keywords].
```

## Capabilities

- 250-byte limit optimization (maximum keyword coverage in minimum space)
- Deduplication against title, bullets, and description
- Keyword prioritization by relevance and search volume signals
- Spanish/multilingual keyword inclusion strategy
- Misspelling and synonym coverage
- Prohibited term filtering (competitor brands, restricted claims)
- Before/after coverage comparison

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### 250-Byte Limit Optimization System

- **Byte Calculation:** English letters/numbers = 1 byte each. Chinese/Japanese = 2-3 bytes each. Special characters may also consume multiple bytes. Use space-separated format (no commas/semicolons) to save delimiter bytes.
- **Exact Deduplication:** Remove keywords already in title or bullets — they won't add extra index weight. Only include keywords not already visible in listing content.
- **Stemming Deduplication:** Amazon's algorithm recognizes word roots. "Running" covers "runner" and "run". Merge variants into one optimal form to avoid redundancy.
- **Semantic Deduplication:** Identify highly similar phrases. Keep the expression with higher search volume or broader coverage.

### Keyword Prioritization Algorithm

- **Search Volume Weighting:** Base score on monthly search volume — higher volume = higher priority.
- **Competition Correction Factor:** High-volume keywords often have intense competition. Apply correction for new products or thin review profiles. Boost medium-competition, decent-volume long-tail keywords.
- **Relevance Strength Assessment:** Only high-relevance keywords drive valuable traffic. Deselect low-relevance high-volume terms (e.g., selling yoga mats but targeting "sneakers").
- **Independent Coverage Value:** Evaluate if each keyword covers search demand no other keyword covers. Low independent value = replaceable when space is tight.

### Misspelling and Synonym Coverage

- **Common Misspellings:** Include high-frequency errors (e.g., "bluetooth" common errors "blutooth" or "bluetooth"). Don't exhaust all variants — only truly frequent misspellings.
- **Synonym Expansion:** Cover regional variations and different consumer terminology (e.g., "portable charger" vs "power bank" for US marketplace).
- **Spanish Keywords:** For US marketplace, allocate ~30-50 bytes for core benefit Spanish translations to capture Spanish-speaking consumers.

### Prohibited Term Filtering

- **Competitor Brand Filter:** Never include other brands' trademarks — may cause ASIN suppression.
- **Restricted Claims Filter:** Prohibit "best", "#1", "free shipping" — violates Amazon policy.
- **Subjective Claims Filter:** Avoid "amazing", "greatest" — unverifiable claims.
- **Punctuation Cleanup:** Remove extra spaces, duplicate delimiters, special characters.

### Data Sources

- User provides title, bullets, and 50-100 keyword candidates.
- No external APIs. Deduplication and prioritization based on built-in logic.

### Limitations

- 250-byte limit is a hard constraint — cannot exceed.
- Duplicate keywords in title/bullets waste bytes without adding index weight.
- Spelling variants consume bytes but capture missed traffic.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps