---
name: amazon-deal-finder
description: "Plan and optimize Amazon promotional deals — Lightning Deals, Best Deals, Coupons, and Prime Exclusive Discounts. Evaluate deal ROI, timing, and strategy for maximum sales impact."
metadata:
  nexscope:
    emoji: "🎫"
    category: amazon
---

# Amazon Deal Finder 🎫

Plan and optimize Amazon promotional deals — Lightning Deals, Best Deals, Coupons, and Prime Exclusive Discounts. Evaluate deal ROI, timing, and strategy for maximum sales impact.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Install

```bash
npx skills add nexscope-ai/eCommerce-Skills --skill amazon-deal-finder -g
```

## Usage

```
Should I run a Lightning Deal for my product? It costs $150 fee, my product is $29.99 with 40% margin. I sell about 10 units/day normally.
```

## Capabilities

- Deal type selection (Lightning Deal, Best Deal, Coupon, Prime Exclusive)
- Deal ROI calculator (fee vs incremental sales)
- Optimal timing and seasonality planning
- Inventory preparation for deal volume
- Deal stacking strategy (coupon + deal + PPC)
- Post-deal momentum capture plan

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Deal Type Comparison and Selection Framework

- **Lightning Deals:** Highest visibility on Deal page and product detail. Runs 4-12 hours, requires application weeks in advance, fixed fee (~$150-$500). Best for: new product ranking boost, inventory clearance, peak season traffic competition. Short duration, high cost, strict eligibility requirements.
- **7-Day Deals (Best Deals):** Similar to Lightning Deals but runs 7 days. Lower cost. Best for: sustained ranking push, large inventory clearance.
- **Coupons:** Self-service discount with green "Coupon" badge. Per-redemption fee ($0.60) + discount amount. High flexibility, can be set anytime. Best for: daily promotions, A/B testing.
- **Prime Exclusive Discounts:** Prime members only, requires at least 20% off. Strong "struck-through" price psychological effect.

### Deal ROI Calculation Model

**ROI = (Incremental profit from extra sales + Long-term ranking benefit) / Total deal cost**

**Cost Components:**
- Discount given (difference between original and deal price)
- Deal application fee
- Coupon redemption fees
- Potential ad spend increase during deal

**Incremental Sales Calculation:**
- Not all deal-period sales are "incremental" — some would have happened anyway
- Only sales ABOVE normal baseline = true deal contribution
- Key input: historical daily sales data for accurate baseline

### Stacking Strategy Framework

- **Definition:** Using multiple promotion types simultaneously for deeper discount effect.
- **Example:** Coupon + Prime Exclusive Discount + Ads → final price far below original.
- **Risk:** Over-stacking can lead to unprofitable deals.
- **Prevention:** Calculate final "floor price" before launch — ensure above break-even point.
- **Sequential Stacking:** Set member discount first, then add coupon after Deal ends for phased effect.

### Post-Deal Momentum Strategy

- **Ranking Benefit:** After deal ends, product typically gets ranking boost from increased sales velocity.
- **Conversion to Sustained Growth Depends On:**
  - Deal sales volume large enough to meaningfully improve BSR ranking
  - Post-deal inventory, ad spend, and review accumulation maintained to capture new traffic
- **Risk:** Stockout or ad budget cut after deal = rapid ranking decline.

### Timing and Seasonality Framework

- **Peak Seasons:** Prime Day (July), Black Friday/Cyber Monday (November), Christmas (December).
- **Competitive Calendar:** Avoid overlapping with major competitor promotions when possible.
- **Inventory Planning:** Align deal timing with inventory turnover cycle.

### Data Sources

- web_fetch scrapes Lightning Deals, Best Deals, Coupon activities from Amazon.
- Fee structure from Amazon Seller official policies (public information).
- User provides: current price, cost structure, normal daily sales, inventory, deal budget, specific goals (ranking boost, clearance, new product launch).

### Limitations

- Deal approval not guaranteed even with complete eligibility. Amazon reviews based on category saturation, deal calendar, competition.
- Incremental sales estimates inherently uncertain — affected by market competition, consumer demand fluctuations.
- Deal price cannot be modified once live — cannot adapt if competitors launch promotions.
- Frequent deep discounts may train consumers to wait for sales, damaging full-price sales.
- Deal-period new buyers may leave negative reviews if disappointed, harming long-term competitiveness.
- Cross-marketplace deals need separate planning — each marketplace has different Prime Day timing.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps