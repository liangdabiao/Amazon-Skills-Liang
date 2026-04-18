---
name: amazon-inventory-management
description: "FBA inventory planning — restock timing, safety stock, IPI score optimization, stranded inventory recovery"
metadata:
  nexscope:
    category: amazon
---

# Amazon Inventory Management

FBA inventory planning — restock timing, safety stock, IPI score optimization, stranded inventory recovery

**Supported platforms:** Amazon (US, UK, DE, CA, JP, AU, and all marketplaces).


## Install

```bash
npx skills add nexscope-ai/Amazon-Skills --skill amazon-inventory-management -g
```

## Usage

```
Help me with amazon inventory management for my e-commerce business.
```

## Capabilities

- FBA inventory planning
- restock timing
- safety stock
- IPI score optimization
- stranded inventory recovery

## How This Skill Works

**Step 1:** Collect information from the user's message — product, platform, current situation, and goals.

**Step 2:** Ask one follow-up with all remaining questions using multiple-choice format. Allow shorthand answers (e.g., "1b 2c 3a").

**Step 3:** Research and analyze using the frameworks and methodology below.

### Replenishment Timing Model

**Reorder Point = Average Daily Sales × (Procurement Lead Time + Shipping Time + Amazon Receiving Time + Safety Buffer Days)**

- **Daily Sales:** Based on 30-60 day rolling average to avoid short-term volatility.
- **Procurement Lead Time:** Confirm with supplier (varies by supplier).
- **Shipping Time:** Sea freight 30-45 days, air freight 5-10 days.
- **Amazon Receiving Time:** Typically 5-10 business days, may extend to 2-3 weeks in Q4 peak season.
- **Safety Buffer:** 20-30% of total replenishment cycle to handle uncertainties.

### Safety Stock Calculation Method

**Safety Stock = Service Level Factor × Demand Standard Deviation × √Replenishment Cycle**

Key factors:
- **Demand Standard Deviation:** Reflects sales volatility.
- **Replenishment Cycle:** Reflects supply chain responsiveness.
- **Service Level Target:** 95-98% recommended.
- Stable products = lower safety stock. Seasonal/volatile products = higher safety stock.
- Also consider supplier delivery reliability, logistics uncertainties, Amazon receiving delays.

### IPI Score Optimization Mechanism

IPI (Inventory Performance Index) ranges 0-1000, based on four dimensions:
- **Excess Inventory Score:** Surplus inventory ratio.
- **Sell-through Rate:** Sales volume relative to inventory.
- **Stranded Inventory Percentage:** Inventory without active offer.
- **Inventory Defect Rate:** Inventory without salable information.

**Impact:** Score below 500 threshold = FBA storage limits imposed, cannot restore until next quarterly evaluation.

**Optimization Actions:**
- Reduce excess inventory through promotions or clearance deals.
- Improve sell-through by increasing sales or reducing inventory.
- Fix stranded inventory by resolving listing issues.
- Complete missing product information to reduce inventory defects.

### Stranded Inventory Identification and Recovery

Common stranded inventory causes:
- Listing suppressed or deactivated.
- Incomplete/inaccurate product information.
- Policy violations.
- ASIN merged under wrong parent listing.

**Recovery:** Use Amazon's "Fix Stranded Inventory" tool to identify causes and take targeted corrective action. Stranded inventory continues incurring storage fees while generating no sales.

### Seasonal Inventory Planning

- **Q1-Q2:** Storage capacity relatively ample, IPI pressure lower. Good time to optimize inventory efficiency.
- **Q3-Q4 (Peak Season):** Amazon tightens storage limits, IPI becomes critical. Clear excess inventory and raise IPI before Q4.
- **Q4 Planning:** Inventory for Oct-Dec needs to arrive by Aug-Sep via sea freight to account for potential delays.
- **Q1 (Off-Peak):** Control replenishment pace, clear excess inventory from previous year.

### Data Sources

- No external data dependencies. Based on supply chain management theory (EOQ model, service level theory) and Amazon FBA policy documentation.
- User provides: sales velocity data, shipping times, supplier lead times, current inventory status.

### Limitations

- **Sales Forecasting Uncertainty:** Multiple uncontrollable factors affect Amazon sales — competitor actions, algorithm changes, seasonal demand, disruptions. New products especially hard to forecast.
- **Supply Chain Delay Risk:** Actual delays may exceed calculations. Port congestion, customs inspection, peak season receiving slowdowns can all cause stockouts despite careful planning.
- **IPI Lag:** IPI is a lagging indicator based on historical performance. By the time you see score drop, problems may have existed for weeks. Algorithm weights not fully transparent.
- **Storage Capacity Hard Limits:** Below-threshold IPI = strict FBA capacity limits during peak selling seasons. Appeal process is difficult.
- **Multi-Channel Coordination Complexity:** Sellers across Amazon + other channels need to balance inventory allocation. Lack of coordination may cause stockouts in some channels while others have excess.

**Step 4:** Deliver structured, actionable output with specific recommendations, not vague advice.

## Output Format

- Start with a summary of findings
- Include specific data points and benchmarks where available
- Provide prioritized action items
- Mark estimates with ⚠️ when based on incomplete data
- End with concrete next steps