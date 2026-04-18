---
name: amazon-brand-tailored-promotions
description: "Brand Tailored Promotions — audience targeting, discount tiers, customer segmentation, repeat purchase incentives"
metadata:
  nexscope:
    category: amazon
---

# Amazon Brand Tailored Promotions

Brand Tailored Promotions — audience targeting, discount tiers, customer segmentation, repeat purchase incentives

**Supported platforms:** Amazon (US, UK, DE, CA, JP, AU, and all marketplaces).


## Install

```bash
npx skills add nexscope/amazon-brand-tailored-promotions
```

## Usage

```
Help me with amazon brand tailored promotions for my e-commerce business.
```

## Capabilities

- Brand Tailored Promotions
- audience targeting
- discount tiers
- customer segmentation
- repeat purchase incentives

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Buyer Audience Segmentation Framework

- **Brand Shoppers:** Buyers who purchased brand products in past 12 months. Can be split into recent buyers and repeat buyers. Lower price sensitivity — 5-10% discount may be enough for repurchase.
- **Browse Retargeting:** Buyers who viewed brand products in past 14 days but didn't purchase. Mid-range price sensitivity.
- **Cart Abandoners:** Buyers who added brand items to cart but didn't checkout. High conversion potential — they're close to purchase decision.
- **Competitor Audience:** Buyers who browsed specific competitor ASINs. Higher price sensitivity — need 15-25% discount to shift brand inertia.
- **High-Value Buyers:** Historical high-ticket purchasers. Target for loyalty programs.
- **Holiday Shoppers:** Buyers active during specific seasonal periods.

### Discount Tiering and Margin Balance Model

- **Price Elasticity by Segment:** Brand loyalists have lower elasticity — smaller discount drives repurchase. Competitor shoppers have higher elasticity — need bigger discount for brand switch.
- **Margin Calculation:** Calculate profit impact at each discount level. Ensure positive margin (or controlled loss for ranking/review strategy).
- **Discount Types:** Percentage off vs fixed dollar amount. Percentage often cleaner for buyers, fixed works for lower-priced items.
- **Minimum Discount Rules:** Amazon typically requires at least 10% off or $5 off, whichever is greater.

### Conversion Funnel Optimization

- **Browse Stage:** Discount attracts clicks from browsers.
- **Consideration Stage:** Discount drives add-to-cart.
- **Purchase Stage:** Discount completes checkout.
- **Retargeting Funnel:** Set up promotions at each key drop-off point to reduce leak rate.

### Customer Lifetime Value (CLV) Maximization

- **First-Time Buyer → Repeat:** Offer repurchase incentive to convert one-time buyers.
- **High-Value Retention:** Exclusive discounts for top customers to boost loyalty.
- **Win-Back Campaigns:** Target dormant customers (past purchases but no recent activity) with reactivation discounts.
- **Cross-Sell Opportunities:** Promote complementary products to existing customers.

### Competitor Traffic Interception Strategy

- **Target Selection:** Choose competitors with similar products but higher price, lower rating, or fewer features. These are "beatable" competitors.
- **Discount Calibration:** Discount must overcome buyer brand inertia but not destroy margin.
- **Timing:** Competitor audience targeting works best when competitor has active promotions or negative reviews accumulating.

### Data Sources

- No external data sources. Based on Amazon Brand Tailored Promotions official documentation.
- User provides brand products, customer data, target audience characteristics.

### Limitations

- Requires Amazon Brand Registry enrollment.
- Audience precision limited by Amazon's data dimensions. Cannot target by age group or specific geography.
- Ad placement and frequency controlled by Amazon algorithm — no guarantee target audience sees promotions.
- Stacking discounts (BTP + coupons + deals) may cause unexpected deep discounts.
- Competitor targeting limited to Amazon-recognized competitors only.
- Frequent promotions may train buyers to wait for discounts, weakening full-price sales.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps