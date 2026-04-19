---
name: amazon-shipping-calculator
description: "Calculate Amazon shipping and fulfillment costs for FBA and FBM. Dimensional weight, storage fees, removal fees, and long-term storage cost estimation."
metadata:
  nexscope:
    emoji: "📐"
    category: amazon
---

# Amazon Shipping Calculator 📐

Calculate Amazon shipping and fulfillment costs for FBA and FBM. Dimensional weight, storage fees, removal fees, and long-term storage cost estimation.

**Supported platforms:** Amazon, Shopify, WooCommerce, Walmart, TikTok Shop, Etsy, eBay, BigCommerce.


## Usage

```
Calculate all FBA costs for my product: 14 x 10 x 3 inches, weighs 1.8 lbs, selling price $34.99. I expect to sell 300 units/month.
```

## Capabilities

- FBA fee calculation (fulfillment, monthly storage, long-term storage)
- Dimensional weight calculation for FBA size tier assignment
- FBM shipping cost estimation by carrier and method
- Storage cost forecasting (monthly and peak season)
- Removal and disposal fee calculation
- FBA vs FBM cost comparison per product
- Inbound shipping cost estimation (partnered carrier vs own)

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Dimensional Weight and Size Tiering System

Amazon FBA fee structure based on product size and weight:

**Actual vs Dimensional Weight:**
- Dimensional weight = L × W × H / 139 (inches) or L × W × H / 5000 (cm).
- Amazon charges greater of actual weight vs dimensional weight.
- Light but bulky items (e.g., pillows) may be charged at higher dimensional weight.

**Size Tiers:**
- **Standard Small:** Max 15" longest side, max 12 oz.
- **Standard Large:** Max 18" longest side, max 20 lbs.
- **Large 1:** Max 60" longest side.
- **Large 2:** Max 120" longest side.
- **Special Oversize:** Above 120".

**Tier Threshold Effect:** When product dimensions/weight near tier boundaries, small changes cause large fee jumps. E.g., 18.1" item enters Large 1 tier — fees may be dollars higher than 18" Standard item. This skill identifies threshold risks and provides optimization suggestions.

### Complete FBA Fee Structure

**Monthly Storage Fees:**
- Standard size: $0.87/cubic foot (Jan-Sep), $2.40/cubic foot (Oct-Dec peak).
- Large size: higher rates.
- Longer storage = more fees accumulate.

**Long-Term Storage Fees:**
- After 271 days: $6.90/unit or $0.15/cubic foot (whichever is greater).
- After 365 days: doubled rates.
- Long-term storage is "invisible killer" of slow-moving inventory.

**Removal/Disposal Fees:**
- Removal: starts at $0.99/unit (standard).
- Disposal: starts at $0.97/unit.
- Calculate economic comparison between removal fees vs long-term storage.

### FBA vs FBM Cost Comparison Model

**FBA Advantages:**
- Higher Buy Box acquisition rate.
- Faster delivery (Prime badge).
- Lower order processing labor cost.
- Amazon handles returns/refunds.

**FBM Advantages:**
- No monthly/long-term storage fee risk.
- Higher per-unit profit (no FBA fulfillment fees).
- Complete inventory turnover control.
- Better for large/heavy items or slow-moving inventory.

**Decision Key:**
- Fast-moving items (high monthly sales): FBA usually more cost-effective. High turnover avoids long-term storage fees + FBA Buy Box advantage significantly boosts sales.
- Slow-moving items or large/heavy products: FBM may be more economical.

### Data Sources

- FBA fee calculation parameters based on Amazon's official size tier standards and rate tables.
- Dimensional weight formula using Amazon official standard.
- Monthly storage, long-term storage, removal/disposal fees from Amazon FBA fee help pages.
- User provides: product physical specs (including packaging), expected monthly sales, target delivery region.

### Limitations

- Fee calculations depend on user-provided product dimensions/weight. If packaging not included, actual billed dimensions may differ.
- Amazon FBA fees adjusted periodically (usually January). This skill uses last published rates — verify current rates in Seller Central.
- Inbound shipping estimates based on partnered carrier standard rates — actual costs may vary due to fuel surcharges, remote area fees, seasonal fluctuations.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps