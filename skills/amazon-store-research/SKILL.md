---
name: amazon-store-research
description: >
  Perform comprehensive deep-dive research on any Amazon seller store. Use this skill whenever the user
  wants to research an Amazon store, analyze a seller's storefront, investigate a brand on Amazon,
  study a competitor's store, or provides an Amazon stores URL (amazon.com/stores/...). Also triggers on
  requests like "调研这个亚马逊店铺", "分析这个Amazon卖家", "深度调研Amazon店铺", "分析亚马逊品牌店铺",
  "Amazon店铺调研", "调研这个卖家", "分析竞争对手店铺", or any request to study/analyze/research an Amazon
  seller store or brand storefront.
---

# Amazon Store Deep Research

Autonomous end-to-end research workflow for any Amazon seller store. The user provides a store URL;
the skill collects data from the storefront, runs parallel analyses, and produces a comprehensive
Chinese-language report package.

## Prerequisites

- **Playwright MCP server** must be available (browser_navigate, browser_evaluate, browser_snapshot, browser_close)
- **Agent tool** for launching parallel analysis subagents
- Reports are saved to `{project_root}/reports/{store-slug}/` (e.g., `reports/jmbricklayer/`).
  Create the subdirectory at the start of each run.

## Workflow Overview

The skill runs in three phases: Data Collection, Parallel Analysis, and Report Synthesis. Track progress with
TaskCreate/TaskUpdate throughout.

**Important**: All file outputs (JSON data, analysis reports, comprehensive report) must go into the store-specific
subfolder under `reports/`. Extract a human-readable slug from the store name (e.g., "JMBricklayer" → `jmbricklayer`).
Create the directory before saving any files.

---

## Phase 1: Data Collection

### Step 1.1 — Parse User Input

Extract from the user's message:
- **Store URL** (required) — the Amazon stores URL, e.g. `https://www.amazon.com/stores/JMBricklayer/page/3CACFA02-74C5-4F9D-81DB-0BF560B7BA47`
- **Store name** — extract from the URL or page title
- **Report language** (optional, default: 简体中文)

### Step 1.2 — Scrape Store Home Page

Navigate to the store URL using `mcp__playwright__browser_navigate`. Wait for the page to fully load.

First, extract the store navigation structure using `mcp__playwright__browser_evaluate`:

```javascript
() => {
  const storeInfo = {};
  const navItems = Array.from(document.querySelectorAll('nav a, nav button'));
  storeInfo.navigation = navItems.map(item => ({
    text: item.textContent?.trim(),
    url: item.href || '',
    type: item.tagName === 'BUTTON' ? 'dropdown' : 'link'
  })).filter(item => item.text && item.text.length > 0 && item.text !== 'Back');

  const productLinks = Array.from(document.querySelectorAll('a[href*="/dp/"]'));
  storeInfo.productLinks = productLinks.map(a => ({
    asin: a.href.match(/\/dp\/([A-Z0-9]+)/)?.[1],
    text: a.textContent?.trim()?.substring(0, 200)
  }));

  const collectionLinks = Array.from(document.querySelectorAll('a[href*="/stores/page/"]'));
  storeInfo.collections = collectionLinks.map(a => ({
    text: a.textContent?.trim(),
    url: a.href,
    id: a.href.match(/page\/([A-F0-9-]+)/)?.[1]
  })).filter(c => c.text && c.text.length > 0);

  return storeInfo;
}
```

This reveals:
- Store navigation items (Home, Best Sellers, New Releases, collections, dropdowns)
- All collection/category page URLs
- Product links visible on the home page

### Step 1.3 — Extract Products from Home Page

Use `mcp__playwright__browser_evaluate` with this product extraction script:

```javascript
() => {
  const products = [];
  const seen = new Set();
  const allLinks = Array.from(document.querySelectorAll('a[href*="/dp/"]'));

  allLinks.forEach(a => {
    const href = a.href;
    const asinMatch = href.match(/\/dp\/([A-Z0-9]+)/);
    if (!asinMatch) return;
    const asin = asinMatch[1];
    if (seen.has(asin)) return;

    const title = a.textContent?.trim();
    if (title && title.length > 20 && !title.includes('Amazon Business') && !title.includes('Reload Your')) {
      seen.add(asin);
      const container = a.closest('li') || a.parentElement?.parentElement?.parentElement || document.body;
      const containerText = container?.innerText || '';
      const priceMatch = containerText.match(/\$[\d,.]+/);
      const reviewMatch = containerText.match(/\(([\d,K]+)\)/);
      const ratingMatch = containerText.match(/([\d.]+) out of 5/);

      products.push({
        asin,
        title: title.substring(0, 200),
        price: priceMatch?.[0] || null,
        reviews: reviewMatch?.[1] || null,
        rating: ratingMatch?.[1] || null,
        url: href.split('?')[0]
      });
    }
  });
  return products;
}
```

### Step 1.4 — Scrape Key Store Pages

Navigate to each key page using the collection URLs discovered in Step 1.2. The standard store pages are:

1. **Best Sellers** — Look for navigation item with text "Best Sellers"
2. **New Releases** — Look for navigation item with text "New Releases"
3. **About us** — Look for navigation item with text "About us"

For each page, use the same product extraction script from Step 1.3.

### Step 1.5 — Scrape Collection/Category Pages

Navigate to each theme collection page discovered from the navigation. Use the same product extraction script.

Common collection patterns:
- "Shop By Theme" dropdown → contains theme categories
- "By Difficulty" dropdown → contains difficulty levels
- Standalone collection links (Occasion, etc.)

**Important**: Identify dropdown menus in the navigation. The dropdown items (indicated by `type: 'dropdown'` or nested links) contain
the actual collection sub-pages. Scrape each sub-collection page.

### Step 1.6 — Close Browser

Run `mcp__playwright__browser_close` when all scraping is complete.

### Step 1.7 — Save Raw Data

Consolidate all scraped data into a single JSON file at `reports/{store-slug}/{store-slug}_store_data.json` with this structure:

```json
{
  "storeInfo": {
    "brandName": "...",
    "storeUrl": "...",
    "storefrontId": "...",
    "scrapeDate": "...",
    "navigation": [...],
    "totalUniqueASINs": 0,
    "priceRange": "..."
  },
  "homePage": { "products": [...] },
  "bestSellers": { "products": [...] },
  "newReleases": { "products": [...] },
  "collections": {
    "Collection Name": { "productCount": 0, "products": [...] }
  }
}
```

Deduplicate ASINs across all pages and count unique products.

---

## Phase 2: Parallel Analysis

Launch **4 analysis agents simultaneously** using the Agent tool with `run_in_background: true` and `subagent_type: "general-purpose"`.
Each agent receives the full raw data and writes its report to `reports/{store-slug}/`.

### Agent 1 — Product Portfolio Analysis

File: `reports/{store-slug}/{store-slug}_portfolio_analysis.md`

Prompt the agent to analyze:
1. **Store overview** — brand positioning, category coverage, total ASIN count, price range
2. **Product matrix** — distribution across collections/categories, cross-category overlaps
3. **Product numbering system** — identify any patterns in product codes/numbers
4. **Price strategy** — price bands, average price per collection, pricing tiers
5. **Rating & review analysis** — average rating per collection, review distribution, review thresholds
6. **Top product profiles** — Top 10 products by review count with characteristics
7. **New release cadence** — product launch speed, innovation direction, recent themes
8. **SKU strategy** — product line expansion, series development, size/piece-count gradients

### Agent 2 — Competitive Positioning Analysis

File: `reports/{store-slug}/{store-slug}_competitive_analysis.md`

Prompt the agent to analyze:
1. **Competitive landscape** — brand positioning (e.g., LEGO alternative, niche player, Chinese export brand)
2. **SWOT analysis** — strengths, weaknesses, opportunities, threats with specific evidence
3. **Direct competitor comparison** — vs major brands (LEGO, and any notable alternative brands relevant to the category)
4. **Differentiation strategy** — unique features (LED lights, licensing, themes, price advantage)
5. **Target customer segments** — who buys these products (collectors, gift buyers, hobbyists, etc.)
6. **Listing strategy** — title keyword patterns, common phrases, optimization observations
7. **Review quality analysis** — cross-collection rating comparison, identifying weak/strong collections

### Agent 3 — Revenue Estimation Analysis

File: `reports/{store-slug}/{store-slug}_revenue_analysis.md`

Prompt the agent to analyze:
1. **Sales estimation methodology** — review-to-sales ratio, comment acceleration, daily review rate
2. **Top 10 product monthly estimates** — monthly unit sales and revenue (conservative/neutral/optimistic)
3. **Store monthly revenue** — tiered model (Top 10 + Tier 2 + Tier 3 long-tail), three scenarios
4. **Collection revenue contribution** — which collections drive the most revenue
5. **Price elasticity analysis** — which price bands accumulate reviews fastest
6. **Product lifecycle analysis** — classify products by lifecycle stage based on review count
7. **New product performance** — assess early-stage products (low review count)
8. **Annual revenue projection** — monthly × 12 with Q4 seasonal weighting

### Agent 4 — Growth Strategy Analysis

File: `reports/{store-slug}/{store-slug}_growth_strategy.md`

Prompt the agent to analyze:
1. **Brand development assessment** — maturity level, market validation, price coverage
2. **Growth opportunities** — which collections to expand, underserved niches, new themes
3. **Product optimization** — fix low-rated products, fill price gaps, bundle opportunities
4. **Operational strategy** — PPC keywords, review building, promotional calendar, inventory
5. **Competitive response** — how to position against big brands and similar alternatives
6. **Market expansion** — international marketplaces, brand website, social media
7. **Risk assessment** — IP risks, quality issues, logistics challenges, seasonal dependency
8. **Action roadmap** — 30/60/90-day plan with specific milestones

**Important**: Pass the actual scraped data (not summaries) to each agent. Include all product ASINs, titles, prices,
ratings, and review counts from the JSON file. The agents need real data to produce meaningful analysis.

---

## Phase 3: Report Synthesis

Wait for all 4 agents to complete (you'll receive task notifications). Then launch one final synthesis agent
(`subagent_type: "general-purpose"`, foreground this time since we need the result) to generate the comprehensive report.

### Final Report

File: `reports/{store-slug}/{store-slug}_comprehensive_report.md`

The synthesis agent should:
1. Read all 4 analysis reports from `reports/`
2. Combine with the raw product data
3. Produce a comprehensive report with this exact structure:

```markdown
# {Store Name} 亚马逊店铺深度调研报告

## 目录
1. 执行摘要
2. 店铺全景概览
3. 产品组合深度分析
4. 竞争定位与差异化策略
5. 收入与销售表现
6. 增长机会与风险评估
7. 运营优化建议
8. 关键发现与行动建议
```

**Key sections must include:**

- **Executive Summary**: 1-page overview with top 5 opportunities table (niche, score, margin, entry difficulty)
  and key metrics dashboard (ASIN count, price range, avg rating, est. monthly revenue)
- **Store Overview**: Brand positioning, navigation structure, product numbering system,
  collection table with product counts
- **Product Portfolio**: Price band distribution, rating by collection, Top 10 products,
  new product pipeline, lifecycle distribution
- **Competitive Positioning**: SWOT matrix, major brand price comparison, differentiation,
  target customer segments with %
- **Revenue & Sales**: Top 10 monthly estimates (3 scenarios), collection revenue %,
  store monthly/annual revenue with seasonality
- **Growth & Risk**: 5 opportunities ranked by potential, 5 risks with mitigation,
  low-score product diagnosis
- **Operations**: PPC strategy, listing optimization, review building, promotional calendar
- **Key Findings**: Top 5 findings, Top 5 action items, 30/60/90-day roadmap

---

## Output Summary

After all phases complete, present the user with:

1. A summary table of all generated reports with file paths
2. The top 5 key findings from the research
3. The top 3 recommended action items

## Error Handling

- If Playwright navigation fails, retry once, then try `mcp__web_reader__webReader` as fallback
- If the extraction script returns empty results, use `browser_snapshot` to inspect the page structure and adapt
- If collection discovery fails, look for alternative URL patterns in the navigation
- If a collection page has no products, skip it and note the empty result
- If any analysis agent fails, regenerate just that one report
- **Data anomaly watch**: Review counts that match product model numbers (e.g., "40102" reviews) are likely
  scraping artifacts — flag these in the analysis
