---
name: amazon-one-shot
description: "Deep-dive Amazon product research in one shot. Analyze any ASIN with 9 comprehensive reports: product info extraction, keyword research, competitor analysis, review deep analysis (login required for best results), sales/revenue estimation, listing optimization audit, image strategy, reusable listing templates, and product selection feasibility score. Use this skill whenever the user provides an Amazon ASIN, product URL, or says 'deep research' / 'deep analysis' / '调研' / '深度调研' / 'product research' / '选品分析' about an Amazon product. Also triggers for phrases like 'analyze this product', 'what do you think of this listing', 'competitive analysis', 'review analysis', or any request involving Amazon product intelligence."
---

# Amazon One-Shot Product Research

One-shot comprehensive Amazon product analysis. Generates 9 reports for any ASIN.

## Workflow Overview

**Phase 1: Data Collection** — Scrape target product + competitors via Playwright
**Phase 2: Report Generation** — Write 9 markdown reports to a timestamped directory

## Phase 1: Data Collection

### Step 1: Extract Target Product Info

Navigate to `https://www.amazon.com/dp/{ASIN}` and extract:

```
Use browser_evaluate() to extract:
- Title (document.getElementById('productTitle'))
- Price (.a-price-whole + .a-price-fraction) — NOTE: may display in CNY
- Rating (#acrCustomerReviewText, .a-icon-star .a-icon-alt)
- Review count (#acrCustomerReviewText)
- Brand (#bylineInfo)
- Bullets (#feature-bullets ul li span) — all 5
- Image count (#altImages img count, exclude video thumbnails)
- Has A+ content (querySelector('#aplus') || querySelector('.aplus-v2'))
- A+ text (#aplus_feature_div innerText, first 1500 chars)
- Reviews ([data-hook="review-body"] first 10 reviews, first 200 chars each)
- BSR and category info from product detail tables
- Star distribution (86% 7% 2% 1% 4% pattern from histogram)
- Product details tables (all table.productDetails, table.a-keyvalue)
- Breadcrumb path (#wayfinding-breadcrumbs_container a)
- Important info/warnings (#importantInformation_feature_div)
- Byline/brand store link (#bylineInfo)
```

### Step 2: Keyword Research

For the target product, navigate to Amazon search with 5+ keyword variations:

```
Search keywords to use (derive from product title + category):
1. "{main_keyword} toy" (e.g., "buzz lightyear toy")
2. "{main_keyword} action figure"
3. "{brand} {main_keyword}" (e.g., "disney toy story figure")
4. "{main_keyword} talking toy {size}" 
5. "{brand} {category} interactive toy gift kids"

For each search, record:
- Total search results count (bodyText.match(/共([\d,]+)条/))
- Top 10 product titles with prices (.a-price .a-offscreen)
- This gives competition density and price range data
```

### Step 3: Find Competitors

From the first search results page:

```
Use browser_evaluate() to extract:
- All product links: document.querySelectorAll('a[href*="/dp/"]')
- Extract ASIN from href: href.match(/\/dp\/([A-Z0-9]+)/)
- Match titles to find top 3-4 direct competitors (same category, similar function)
```

Then navigate to each competitor ASIN page and extract the same data as Step 1 (title, price, rating, review count, bullets, BSR, A+ type, product details tables).

### Step 4: Review Analysis (Enhanced with Login)

If logged in, navigate to review pages by star rating:

```
1-star reviews: /product-reviews/{ASIN}?filterByStar=one_star&sortBy=helpful
2-star reviews: /product-reviews/{ASIN}?filterByStar=two_star&sortBy=helpful
3-star reviews: /product-reviews/{ASIN}?filterByStar=three_star&sortBy=recent
Latest reviews: /product-reviews/{ASIN}?sortBy=recent

Extract from each page:
- Review body ([data-hook="review-body"] span)
- Date ([data-hook="review-date"])
- Format/variant ([data-hook="format-strip"]) — CRITICAL: identifies which product variant the review is about
- Verified purchase ([data-hook="avp-badge"])
- Helpful votes ([data-hook="helpful-vote-statement"])

Target: 10 reviews per star level (1-star, 2-star, 3-star) + 10 most recent = 40 total reviews
```

**If NOT logged in:** Extract reviews from the product detail page directly (usually 8-15 reviews visible). Note this limitation in the report.

### Step 5: Image Analysis

```
From the product page:
- Count all images (#altImages img, exclude video thumbnails with .SS40 or .SX in URL)
- Note video presence
- Take screenshots of the product page top section for visual reference
- Record image URLs and alt text
```

## Phase 2: Report Generation

Save all reports to `reports/{YYYY-MM-DD}_{ASIN}/` directory.

### Report 1: Product Overview (`01_product_info.md`)

Structure:
- Basic info table (ASIN, title, brand, price, CNY + USD estimate ÷7.26, rating, review count, BSR, category path)
- 5 bullet points (full text)
- A+ content summary
- Product details tables (material, dimensions, weight, battery, age range, UPC, model number)
- Important warnings
- Image count + video info

### Report 2: Keyword Research (`02_keyword_research.md`)

Structure:
- Keyword search volume table (keyword, result count, competition density, our ranking)
- High commercial intent keywords
- Long-tail opportunity keywords (low results = high opportunity)
- Competition landscape (brand distribution, price range analysis)
- Seasonal trends (Q4 peak 55-65%, Prime Day, Black Friday)
- Market opportunity score (1-10, explain reasoning)
- Selection recommendation

### Report 3: Competitor Analysis (`03_competitor_analysis.md`)

Structure:
- Competitor overview table (ASIN, brand, price, size, reviews, rating, BSR, weight, battery, material)
- Listing quality comparison (title, bullets, images, A+)
- BSR ranking comparison with visual bar chart
- Review volume and market share estimation
- Price positioning map
- Review sentiment comparison
- Differentiation strategy summary
- Competitive landscape conclusion (pyramid)
- Selection recommendation

### Report 4: Review Deep Analysis (`04_review_analysis.md`)

Structure:
- Star distribution (86/7/2/1/4) with calculation verification
- Positive theme word frequency ranking
- Negative theme word frequency ranking
- 1-star review root cause analysis (with direct quotes)
- 2-star review root cause analysis
- 3-star review root cause analysis
- Product variant quality breakdown (which variant has most issues)
- Buyer persona analysis (identity %, use cases, geography)
- Recent trend analysis (2026 latest reviews)
- UGC mining (marketing copy extracted from real reviews)
- Product improvement priority matrix (P0/P1/P2)
- Shared review pool discovery (if detected)

### Report 5: Sales & Revenue Estimation (`05_sales_revenue.md`)

Structure:
- FBA fee calculation (size tier, fulfillment fee, commission, storage, total Amazon fees)
- Profit analysis (gross profit, net profit, margin %, ROI)
- Monthly sales estimation based on BSR (conservative/medium/optimistic)
- Single product vs series breakdown (if shared review pool detected)
- Annual revenue estimation
- Comment growth verification method
- Seasonal sales distribution (Q1-Q4)
- Key sales events (Prime Day, Black Friday, Christmas)
- Selection financial feasibility summary

### Report 6: Listing Optimization Audit (`06_listing_optimization.md`)

Structure:
- 8-dimension audit score table (title/15, bullets/15, images/15, A+/10, description/10, pricing/10, reviews/15, SEO/10)
- Title analysis (keyword coverage, length optimization, missing terms)
- Bullet analysis (structure assessment, keyword embedding, improvement suggestions)
- Image assessment (current count, missing types, competitor comparison)
- A+ content evaluation (custom vs template, narrative style)
- SEO keyword coverage matrix (which keywords appear where, gaps)
- Gap analysis (before/after optimization suggestions)
- Reusable strategies extracted

### Report 7: Image Strategy (`07_image_strategy.md`)

Structure:
- Current image configuration summary
- Per-image evaluation (content, quality, score, what's missing)
- Video evaluation
- 8-dimension image scoring
- Missing image types identified (size comparison, infographic, lifestyle, what's-in-box, interaction demo, competitor comparison)
- Shooting checklist (7 images + 2 videos recommended, with specific requirements)
- Photography notes based on common review complaints

### Report 8: Listing Templates (`08_listing_templates.md`)

Structure:
- Title template extraction (formula from Disney's title structure)
- Bullet template extraction (functional progression structure)
- A+ Content template extraction (first-person narrative structure)
- Backend search terms suggestion
- Universal template (can be adapted for any interactive toy/product)
- Writing rules summary

### Report 9: Final Assessment (`09_final_assessment.md`)

Structure:
- Market attractiveness matrix (8 dimensions scored 1-10)
- SWOT analysis (strengths, weaknesses, opportunities, threats)
- Product selection scoring card for 3 strategies:
  - Same-IP competitor (usually not feasible)
  - Non-IP interactive product
  - Accessories/peripherals
- Each strategy: feasibility, expected monthly profit, entry cost, recommendation score
- Top 5 learnings from this product (regardless of whether you enter this market)
- MVP suggestion if entering
- Risk warnings
- Report index (all 9 reports listed)

## Important Implementation Notes

1. **CNY Pricing:** Amazon may display prices in CNY. Divide by ~7.26 for USD estimate. Always note both values.

2. **Shared Review Pool:** Disney/publisher products may share reviews across variants. Check if review count and BSR are nearly identical across ASINs. Check `format: 样式:` tag in reviews to identify which variant each review is about.

3. **Browser Limitations:** 
   - If product details tables don't load on first try, scroll down and wait 3 seconds, then retry
   - Review pages require login — if not logged in, extract from product page only and note the limitation
   - Amazon may redirect to login/captcha — wait and retry
   - Google Trends may not be accessible — use general knowledge for seasonal trends

4. **Error Recovery:**
   - If page returns empty product data, wait 3 seconds and retry
   - If navigation is blocked by captcha, close browser, reopen, and continue
   - If review pages redirect to login, try the product page reviews section instead

5. **Language:** The skill works on Chinese locale Amazon pages (text in Chinese). All report output should be in Chinese.

6. **Output:** Save all 9 reports as markdown files to `reports/{YYYY-MM-DD}_{ASIN}/` directory. Use the session's working directory as the base for the `reports/` path.

7. **Tone:** Objective, data-driven analysis. Present facts and numbers clearly. Use tables extensively. Include direct review quotes where relevant. Mark estimates with ⚠️.
