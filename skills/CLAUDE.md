# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Amazon Skills — a collection of 52 free AI agent skills for Amazon sellers. Each skill is self-contained and follows the [Skills format](https://skills.sh), compatible with OpenClaw, Claude Code, Cursor, Windsurf, and Codex.

No API keys required. Skills use Amazon's public autocomplete endpoints and web data.

## Skill Anatomy

Each skill directory follows this structure:

```
amazon-[skill-name]/
├── SKILL.md          # Frontmatter (name, version, description) + usage docs
├── _meta.json        # Metadata (ownerId, slug, version) — optional
└── scripts/          # Implementation scripts — optional
    ├── *.py          # Python for calculations (FBA fees, tariffs)
    └── *.sh          # Bash for web scraping (autocomplete, data collection)
```

Not all skills have scripts — some are purely prompt-driven (SKILL.md instructions only). Skills with scripts (`calculator.py`, `research.sh`, `hs_lookup.py`) provide data-gathering capabilities that the AI agent invokes.

## Running Scripts

Scripts are standalone with no external dependencies (beyond Python 3 stdlib + curl):

```bash
# Keyword research - fetches autocomplete suggestions
bash amazon-keyword-research/scripts/research.sh "<keyword>" [marketplace]
# marketplaces: us (default), uk, de, fr, it, es, jp, ca, au, in, mx, br

# FBA calculator - run directly with python3
python3 amazon-fba-calculator/scripts/calculator.py

# Tariff calculator
python3 tariff-calculator-amazon/scripts/calculator.py
python3 tariff-calculator-amazon/scripts/hs_lookup.py
```

## Installation (for users)

```bash
npx skills add nexscope-ai/Amazon-Skills -g                          # all skills
npx skills add nexscope-ai/Amazon-Skills --skill <skill-name> -g     # single skill
```

## Architecture Notes

- **Skills are independent** — no shared code, no package manager, no build step
- **Python scripts** use only stdlib (`json`, `dataclasses`, `enum`, `urllib`, `sys`) and target Python 3
- **Bash scripts** depend on `curl` and `python3` (for JSON parsing via inline one-liners)
- **12 Amazon marketplaces** supported, each mapped to a domain and market ID in scripts
- **SKILL.md frontmatter** drives skill discovery — the `description` field in frontmatter is what triggers the skill for AI agents
- Production-ready skills (6 total): `amazon-keyword-research`, `amazon-listing-optimization`, `amazon-fba-calculator`, `amazon-ppc-campaign`, `amazon-sales-estimator`, `tariff-calculator-amazon`

## No Build/Test/Lint

This project has no build system, test suite, or linter. Changes are verified by running the affected script directly.
