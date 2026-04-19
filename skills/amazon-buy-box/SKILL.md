---
name: amazon-buy-box
description: "Win and maintain the Amazon Buy Box. Analyze Buy Box eligibility factors, competitor pricing dynamics, and develop pricing and fulfillment strategies to maximize your Buy Box percentage."
metadata:
  nexscope:
    emoji: "🏅"
    category: amazon
---

# Amazon Buy Box Strategy 🏅

Win and maintain the Amazon Buy Box. Analyze Buy Box eligibility factors, competitor pricing dynamics, and develop pricing and fulfillment strategies to maximize your Buy Box percentage.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Usage

```
I'm losing the Buy Box on my top product to 3 other sellers. I use FBA, my price is $24.99, competitors are at $23.99-$25.49. How do I win it back?
```

## Capabilities

- Buy Box eligibility factor analysis
- Competitive pricing strategy for Buy Box capture
- FBA vs FBM impact on Buy Box share
- Account health metrics optimization
- Repricing strategy recommendations (manual vs automated)
- Buy Box share tracking and improvement plan

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Buy Box Eligibility Requirements

- **Professional Seller Account:** Must have professional selling plan.
- **Inventory Availability:** Must be in stock, no stockouts.
- **Condition:** Must be "New" condition.
- **Order Defect Rate (ODR):** Must be below 1%.
- **Late Shipment Rate:** Must be below 4%.
- **Valid Tracking Rate:** Must be above 95%.
- **Sales History:** New accounts need time to accumulate history before algorithm gives fair assessment.
- **Failure in any above = complete loss of Buy Box eligibility**, regardless of pricing.

### Buy Box Algorithm Multi-Dimensional Scoring

Amazon's Buy Box is NOT simply lowest price. It's a comprehensive scoring system:

- **Price Competitiveness (Highest Weight):** Includes listing price, shipping cost, and total landed price. Algorithm favors lowest total cost seller.
- **Fulfillment Method:** FBA sellers have structural advantage. FBA can win Buy Box even priced 2-5% higher than FBM — because Amazon trusts its own fulfillment.
- **Seller Performance Metrics:** Feedback rating, ODR, late shipment rate, delivery experience. Better performance = higher Buy Box probability.
- **Inventory and Shipping Speed:** Adequate inventory with fast shipping earns algorithm favor.
- **Sales History and Rank:** Historical sales volume and ranking give sellers higher "trust weight."

### FBA vs FBM Impact Analysis

- **FBA Structural Advantage:** FBA sellers can win Buy Box even at 2-5% price premium. Consumer trust in Amazon fulfillment outweighs price difference.
- **FBM Price Requirement:** FBM sellers typically need to be 3-10% cheaper to compete for Buy Box.
- **Hybrid Strategy:** Consider FBA for core products, FBM for oversized or slow-moving items.

### Multi-Seller Buy Box Rotation Mechanism

- When multiple qualified sellers compete, Amazon typically rotates Buy Box among similar-performing sellers.
- Cannot achieve 100% Buy Box share even with perfect metrics — rotation is inherent.
- **Key to maximize share:** Build advantages across multiple algorithm dimensions simultaneously to earn higher rotation proportion.

### Data Sources

- web_fetch tool scrapes current Buy Box holder, Buy Box price, fulfillment method, competitor pricing from Amazon product pages.
- User provides: ASIN list, current price, fulfillment method, seller metrics (ODR, late shipment rate, feedback score), inventory status, historical Buy Box win rate.
- No direct access to Seller Central or Amazon's internal algorithm parameters.

### Limitations

- Buy Box algorithm weights are Amazon trade secrets. Analysis based on industry experience and observation — may not reflect actual algorithm exactly.
- New products/accounts need weeks to months before algorithm gives fair assessment. Buy Box win rate may be low initially.
- When too many sellers (>10) with similar prices compete, Buy Box rotates rapidly. Single seller ceiling typically 60-70%.
- Special categories (used goods, heavy/bulky items) have different Buy Box rules.
- Performance metric improvements (ODR reduction) take time to reflect in algorithm. Short-term fixes may not show immediate results.
- Prime Day and peak seasons significantly intensify Buy Box competition. Strategies may need major adjustment during promotions.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps