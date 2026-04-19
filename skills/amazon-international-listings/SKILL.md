---
name: amazon-international-listings
description: "Multi-marketplace listing management — translation, pricing localization, BIL (Build International Listings)"
metadata:
  nexscope:
    category: amazon
---

# Amazon International Listings

Multi-marketplace listing management — translation, pricing localization, BIL (Build International Listings)

**Supported platforms:** Amazon (US, UK, DE, CA, JP, AU, and all marketplaces).


## Usage

```
Help me with amazon international listings for my e-commerce business.
```

## Capabilities

- Multi-marketplace listing management
- translation
- pricing localization
- BIL (Build International Listings)

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Cross-Market Product Information Sync Mechanism

Amazon's Build International Listings (BIL) tool connects source and target marketplaces:
- Create/maintain main Listing in "Source Marketplace" → BIL auto-syncs to target marketplaces.
- System auto-converts currency and basic translation during sync.
- Price rules can be set per target marketplace (premium/discount percentage).

### Localization Translation Principle

High-quality translation requires three layers:
1. **Terminology Accuracy:** Correct translation of technical parameters, material descriptions, industry terms.
2. **Cultural Adaptation:** Ensure product descriptions match target market language habits and cultural background.
3. **SEO Keyword Localization:** Different markets use different search terms. Direct translation often ineffective. E.g., US consumers search "water bottle" more than "drinking vessel."

### Pricing Localization Mechanism

Cross-market pricing considers:
- Consumer purchasing power in target market.
- Competitor price ranges.
- Import duties and VAT differences.
- Logistics costs.
- Exchange rate fluctuations.

BIL allows price rules based on source price, but sophisticated strategy requires independent pricing per market based on local competitive environment. Fee structures (commissions, FBA fees) vary by marketplace.

### Multi-Market Compliance and Category Matching

Different marketplaces may classify same product differently, some may have category restrictions.
- E.g., certain electronics accessories regular in US, but require CE certification in EU.
- BIL tries to auto-match categories, but seller must verify accuracy.
- Wrong categories → Listing removed or traffic loss.

### Data Sources

- No external dependencies. Based on Amazon Seller Central BIL documentation.
- User provides: original Listing content (title, bullets, images), target market info.

### Limitations

- **Auto-translation quality limited:** BIL auto-translation varies widely — technical terms, brand expressions, culturally sensitive content often poorly handled.
- **Category/compliance differences handled imperfectly:** BIL auto-matching not 100% accurate. Different marketplace classifications and compliance requirements (CE, PSE, etc.) may be missed.
- **Exchange rate pricing risk:** BIL uses fixed exchange rates — actual rates fluctuate. Unadjusted rates may cause overpriced (uncompetitive) or underpriced (low margin) situations.
- **Limited differentiation capability:** BIL philosophy is "one source Listing across markets" — limits differentiated operations. Different markets need different approaches.
- **Data silo problem:** Marketplace sales/ad data independent — no unified cross-marketplace analytics. Managing 5+ marketplaces requires significant time/effort.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps