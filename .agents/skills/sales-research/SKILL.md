---
name: sales-research
description: >-
  In-depth company research and firmographics analysis. Evaluates business models, team size, financial signals, technology stack, and recent news, saving COMPANY-RESEARCH.md.
---

# Skill: sales-research

**Role:** In-depth firmographic and growth signal analysis of target B2B accounts across 8 standardized dimensions.  
**Mandatory Rules:** `customer-context.md` (mandatory), `fact-checking.md` (mandatory), `scoring.md`, `output-formatting.md`.  
**Deliverables:** `reports/{slug}/COMPANY-RESEARCH.html` and `reports/{slug}/markdown/COMPANY-RESEARCH.md`.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, web queries, and analytical notes operate in English. The final deliverable automatically adapts to the primary language of the audited prospect.

## Contextual Resolution Gateway (Mandatory Step 0)

Before generating any output, resolve the target prospect:
1. **Explicit argument provided:** Extract the domain and prospect slug (`reports/{slug}/`).
2. **Omitted argument (`*`):** Analyze the recent conversation history. If a prospect account is already active in the exchange, deduce and reuse its slug without prompting for confirmation.
3. **Complete absence of context:** STOP IMMEDIATELY. Write NO files to disk. Prompt the user clearly for clarification:
   > *"Which prospect account or URL would you like to analyze? (e.g., `research https://example.com`)"*

> [!CAUTION]
> **Strict Prohibition:** Never create any deliverable directly at the root of `reports/`.

## Trigger

Invoked via `research <url>`. Apply the **Contextual Resolution Gateway** first. Mandatorily inspect `.agents/rules/customer-context.md` to benchmark prospect firmographics and filter relevant signals against target sweet spots. If available, inspect also:
- `reports/my-company/markdown/ICP-FRAMEWORK.md` (or `.html` version).

## Workflow (4 Sequential Steps)

> [!IMPORTANT]
> **Re-run & Refresh Policy:** When explicitly invoked with a target prospect URL or topic, systematically execute a fresh web exploration. Overwrite existing local reports with updated findings and today's date (`audit_date`). Never use existing local markdown files as a substitute for an explicit user re-run.

1. **Official Web Intelligence Gathering:**
   - Run `read_url_content` across 7 target pages: `/` → `/about` → `/pricing` → `/careers` → `/blog` → `/integrations` → `/customers`.

2. **Multi-Source External Research:**
   - Execute 5 systematic `search_web` queries per `fact-checking.md`:
     - Funding, valuation, and verified revenue statements
     - Headcount trajectory and active hiring roles
     - Press releases and business updates (< 12 months)
     - Customer reviews on G2 / Capterra / Trustpilot
     - Core alternatives and named competitors

3. **8-Dimensional Firmographic Synthesis:**
   1. *Company Overview:* Sector, founded year, HQ location, core mission.
   2. *Business Model & Monetization:* Pricing model, customer segments, ACV signals.
   3. *Product Architecture & Tech:* Core software stack, delivery model, integration maturity.
   4. *Leadership & Organization:* Founders, key executive tenure, team structure.
   5. *Funding & Financial Health:* Capital raised, lead investors, growth trajectory.
   6. *Market Position & Competitors:* Direct rival landscape, differentiators.
   7. *Culture & Employer Brand:* Hiring velocity, engineering culture, employee sentiment.
   8. *Recent Developments:* New product launches, executive hires, corporate expansions.
   Specification reference: `view_file(".agents/skills/sales-research/references/research-dimensions.md")`.

4. **Synthesis & Company Fit Score:**
   - Mechanically derive the Company Fit Score (0–25) using the Budget scorecard in `scoring.md`.

## Strict Guardrails

- Every documented data point must cite its verified source in parentheses (Confirmed / Estimated / Not publicly available).
- Data older than 18 months must be explicitly flagged as `[Historical]`.
- Never guess or extrapolate unstated financial figures. Unverifiable revenue = `Not publicly available`.

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/COMPANY-RESEARCH.html` using `view_file(".agents/rules/references/report-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/COMPANY-RESEARCH.md` using `view_file(".agents/skills/sales-research/references/output-template.md")`.

Display the Executive Briefing Card (Modern Markdown) at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
