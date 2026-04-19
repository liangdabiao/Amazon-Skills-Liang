---
name: amazon-category-research
description: >
  Perform comprehensive deep-dive research on any Amazon Best Sellers category. Use this skill whenever the user
  wants to research an Amazon product category, analyze Amazon bestsellers, investigate a niche on Amazon,
  do market research for Amazon selling, or provides an Amazon bestsellers/gp/bestsellers URL. Also triggers on
  requests like "调研这个亚马逊品类", "分析这个Amazon类目", "深度调研Amazon Best Sellers", "分析亚马逊畅销榜",
  "Amazon品类机会分析", or any request to study/analyze/research an Amazon category or bestsellers page.
---

# Amazon Category Deep Research

Autonomous end-to-end research workflow for any Amazon Best Sellers category. The user provides a category URL;
the skill collects data, runs parallel analyses, and produces a comprehensive Chinese-language report package.

## Prerequisites

- **Playwright MCP server** must be available (browser_navigate, browser_evaluate, browser_snapshot, browser_close)
- **Agent tool** for launching parallel analysis subagents
- Reports are saved to `{project_root}/reports/{category-slug}/` (e.g., `reports/toys-and-games/`, `reports/building-toys/`).
  Create the subdirectory at the start of each run.

## Workflow Overview

The skill runs in three phases: Data Collection, Parallel Analysis, and Report Synthesis. Track progress with
TaskCreate/TaskUpdate throughout.

**Important**: All file outputs (JSON data, analysis reports, comprehensive report) must go into the category-specific
subfolder under `reports/`. Extract a human-readable slug from the category name (e.g., "Building & Construction Toys"
→ `building-toys`, "Toys & Games" → `toys-and-games`). Create the directory before saving any files.

---

## Phase 1: Data Collection

### Step 1.1 — Parse User Input

Extract from the user's message:
- **Category URL** (required) — the Amazon Best Sellers URL, e.g. `https://www.amazon.com/gp/bestsellers/toys-and-games/`
- **Subcategories** (optional) — specific subcategories to deep-dive. If omitted, auto-select the top 5 most relevant
  based on product overlap with the main Top 30 list.
- **Report language** (optional, default: 简体中文)

### Step 1.2 — Scrape Main Category Top 30

Navigate to the category URL using `mcp__playwright__browser_navigate`. Wait for the page to fully load.

Use `mcp__playwright__browser_evaluate` with this extraction script:

```javascript
() => {
  const lines = document.body.innerText.split('\n');
  const products = [];
  let current = null;
  for (let i = 0; i < lines.length; i++) {
    const match = lines[i].match(/^#(\d+)$/);
    if (match) {
      if (current && current.title) products.push(current);
      current = { rank: parseInt(match[1]) };
    } else if (current) {
      if (lines[i].includes('out of 5 stars')) current.stars = lines[i].trim();
      else if (lines[i].includes('offers from') || lines[i].match(/^\$[\d,.]+$/)) current.price = lines[i].trim();
      else if (lines[i].match(/^[\d,]+$/) && current.stars) current.reviews = lines[i].trim();
      else if (lines[i].trim().length > 15 &&
               !lines[i].includes('Movers') && !lines[i].includes('New Releases') &&
               !current.title) {
        current.title = lines[i].trim();
      }
    }
  }
  if (current && current.title) products.push(current);
  const nrIdx = products.findIndex(p => p.title && (p.title.includes('New Releases') || p.title.includes('Movers')));
  const result = nrIdx > 0 ? products.slice(0, nrIdx) : products.filter(p => p.title && p.title.length > 10);
  return result.slice(0, 30);
}
```

Save the result to `reports/{category-slug}/{category-slug}_top30.json` (use a human-readable slug like `building-toys`).

### Step 1.3 — Discover Subcategories

On the same page, use `mcp__playwright__browser_evaluate` to find the subcategory navigation links:

```javascript
() => {
  const allLists = document.querySelectorAll('ul, ol');
  const subcats = [];
  allLists.forEach(list => {
    const items = list.querySelectorAll('li');
    const firstText = items[0]?.textContent?.trim() || '';
    if (firstText.includes('Action & Toy Figures') || firstText.includes('Arts & Crafts') || firstText.includes('Baby & Toddler') || firstText.includes('Building')) {
      list.querySelectorAll('a').forEach(a => {
        subcats.push({ name: a.textContent.trim(), url: a.href });
      });
    }
  });
  return subcats;
}
```

This returns the full list of subcategory links from the left sidebar. If this fails (returns empty), try
alternative selectors: `a[href*="/zgbs/"]`, or extract from the "Any Department" dropdown text.

If the user specified subcategories, match by name. Otherwise, auto-select **5 subcategories** using this logic:
1. Map each Top 30 product to its most likely subcategory
2. Rank subcategories by frequency of appearance in Top 30
3. Select the top 5 (excluding the main category itself)
4. If fewer than 5 subcategories appear, fill with adjacent categories

### Step 1.4 — Scrape Each Subcategory Top 20

For each selected subcategory:
1. Navigate to its URL with `mcp__playwright__browser_navigate`
2. Run the same extraction script as Step 1.2 (but `.slice(0, 20)` instead of 30)
3. Save to `reports/{category-slug}/{subcategory_slug}_top20.json`

Do this sequentially (Playwright uses a single browser tab). Target 5 subcategories max.

### Step 1.5 — Close Browser

Run `mcp__playwright__browser_close` when all scraping is complete.

---

## Phase 2: Parallel Analysis

Launch **4 analysis agents simultaneously** using the Agent tool with `run_in_background: true` and `subagent_type: "general-purpose"`.
Each agent receives the full raw data and writes its report to `reports/`.

### Agent 1 — Niche Analysis

File: `reports/{category-slug}/{category-slug}_niche_analysis.md`

Prompt the agent to analyze:
1. **Product type distribution** — which categories dominate the Top 30, percentage breakdown
2. **Price band analysis** — $0-7 / $7-15 / $15-30 / $30-50 / $50+ distribution and viability
3. **Star rating patterns** — identify quality gaps (high demand + low ratings = opportunity)
4. **Top 5 niche recommendations** — ranked by: demand level, competition intensity, profit potential, entry difficulty
5. **Supply chain guidance** — sourcing locations (Yiwu, Shantou, Dongguan, etc.), factory types, MOQ expectations
6. **Risk assessment** — compliance, seasonality, IP, competitive risks

### Agent 2 — Competitor Analysis

File: `reports/{category-slug}/{category-slug}_competitor_analysis.md`

Prompt the agent to analyze:
1. **Brand landscape** — identify repeat brands, brand concentration, Chinese vs US seller ratio
2. **Product strategy** — SKU matrix/variant play, bundling, IP licensing, pricing strategies
3. **Review barrier** — estimate review thresholds by price tier for new sellers to compete
4. **Entry difficulty rating** (1-5 stars) for each major subcategory
5. **Top 3 entry recommendations** with target price, differentiation angle, and risk level
6. **Review building strategy** — Vine program, Request a Review, social seeding timeline

### Agent 3 — Keyword Analysis

File: `reports/{category-slug}/{category-slug}_keyword_analysis.md`

Prompt the agent to analyze:
1. **High-frequency keywords** — extract from all product titles, rank by frequency, group by subcategory
2. **Search intent analysis** — by age group (0-2, 2-4, 4-8, 8-12), by scenario (birthday, education, travel, holiday)
3. **Keyword strategy** — high-volume low-competition opportunities, title formula per subcategory, backend keywords template (250 bytes)
4. **PPC keyword matrix** — for the top 4 subcategories: broad/phrase/exact match suggestions + negative keywords
5. **Seasonal keyword calendar** — month-by-month planning for Q2 (summer), Q3 (back-to-school), Q4 (holidays)

### Agent 4 — Profit Analysis

File: `reports/{category-slug}/{category-slug}_profit_analysis.md`

Prompt the agent to analyze:
1. **Price tier profit models** — for each price band ($0-7, $7-15, $15-30, $30-50, $50+): estimate COGS from Alibaba,
   FBA fees (referral 15%, fulfillment, storage), net margin range
2. **Per-category unit economics** — for the top 5 subcategories: estimated COGS, FBA fees, net profit per unit, margin %
3. **FBA optimization** — packaging size tier reduction strategies, storage tips
4. **Startup cost model** — minimum viable launch budget (2 SKUs x 500 units), advertising budget recommendation
5. **Break-even analysis** — monthly unit sales needed to cover fixed costs
6. **ROI ranking** — rank subcategories by estimated return on investment

**Important**: Pass the actual scraped data (not summaries) to each agent. Include all product titles, prices, ratings,
and review counts. The agents need real data to produce meaningful analysis.

---

## Phase 3: Report Synthesis

Wait for all 4 agents to complete (you'll receive task notifications). Then launch one final synthesis agent
(`subagent_type: "general-purpose"`, foreground this time since we need the result) to generate the comprehensive report.

### Final Report

File: `reports/{category-slug}/{category-slug}_comprehensive_report.md`

The synthesis agent should:
1. Read all 4 analysis reports from `reports/`
2. Combine with the raw product data
3. Produce a comprehensive report with this exact structure:

```markdown
# 亚马逊美国站 {Category Name} 品类综合研究报告

## 目录
1. 执行摘要
2. 品类全景概览
3. 子品类深度分析 (Deep dive per subcategory)
4. 市场机会矩阵
5. 新卖家入场策略
6. 运营落地指南
7. 财务模型
8. 风险管控
9. 行动路线图
```

**Key sections must include:**

- **Executive Summary**: 1-page overview with top 5 opportunities table (niche, score, margin, startup cost, payback period)
- **Category Landscape**: Top 30 product type distribution table, price band analysis with FBA fee ratios
- **Subcategory Deep Dives**: For each scraped subcategory: market characteristics, competitive landscape, pricing analysis,
  key players, entry difficulty rating (1-5 stars)
- **Market Opportunity Matrix**: Rate 8-12 niches on 4 dimensions (demand, competition, profit, difficulty),
  assign S/A/B/C grades
- **Entry Strategy**: 3 phases — Validation (month 1-2), Expansion (month 3-6), Brand Building (month 6-12)
- **Operational Playbook**: Listing title formula, keyword strategy, PPC phased plan, review building, seasonal calendar
- **Financial Model**: Two startup budgets (lean $3-5K, standard $8-15K), unit economics for top 3 products,
  break-even analysis, 6-month P&L projection
- **Risk Management**: Compliance checklist (CPC/CPSIA/ASTM/FCC as applicable), IP protection, seasonal inventory, competitive defense
- **Action Roadmap**: Detailed 30/60/90 day plan with milestones

---

## Output Summary

After all phases complete, present the user with:

1. A summary table of all generated reports with file paths
2. The top 5 key findings from the research
3. The top 3 recommended action items

## Error Handling

- If Playwright navigation fails, retry once, then try `mcp__web_reader__webReader` as fallback
- If the extraction script returns empty results, the page structure may differ — use `browser_snapshot` to inspect
  the page structure and adapt the selectors
- If subcategory discovery fails, ask the user to provide subcategory URLs manually
- If any analysis agent fails, regenerate just that one report
