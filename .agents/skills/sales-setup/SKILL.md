---
name: sales-setup
description: >-
  Conversational onboarding skill. Guides user through interactive workspace setup, extracts product context from company website, abstracts ICP from reference client, and persists .agents/rules/product-context.md and .agents/rules/customer-context.md (< 5 KB each).
---

# Skill: sales-setup

**Role:** Autonomous conversational onboarding and workspace configuration engine. Calibrates product offering and customer ICP rules directly from public web intelligence and targeted user feedback.  
**Autonomy:** 100% autonomous standalone skill. Never delegates to sub-agents (e.g., does not invoke `sales-icp`). Orchestrates the complete discovery dialogue, web scraping, and file persistence directly.  
**Mandatory Rules:** `output-formatting.md` (mandatory).  
**Generated Deliverables:** `.agents/rules/product-context.md` (< 5 KB), `.agents/rules/customer-context.md` (< 5 KB), and `reports/my-company/company-dna.html`.

> [!IMPORTANT]
> **Language Governance:** The skill specification, internal prompts, and schemas remain strictly in English. During execution, the agent converses in the user's input language (French/English) and populates the rule files in that same language.

## Triggers & Entrypoints

1. **Bare Command (`setup`):**  
   Prompt the user politely in chat for their company website URL before proceeding:  
   *Prompt Example:* "Welcome to AI Sales Team setup! To start onboarding, please provide the URL of your company website (e.g., `https://my-company.com`)."
2. **Direct Argument (`setup <url>`):**  
   Immediately ingest the provided URL and launch Step 1 without asking for the company website.

---

## Workflow (5 Sequential Steps)

### Step 1: User Company & Offering Discovery
1. Extract the user company website using `read_url_content`:
   - Primary: `/` (Homepage)
   - Secondary pages: `/about`, `/services`, `/solutions`, `/pricing`, `/case-studies`
   - Fallback: `search_web` if content is JavaScript-heavy or protected.
2. Synthesize key product offering dimensions:
   - **Commercial Name, Profile & Positioning**
   - **Verbatim Value Proposition**
   - **Core Practice Pillars** (top 3 service/product lines)
   - **Target Personas** (Economic Buyer & Champion)
   - **Initial Pricing Indicators & Exclusions:**
     > [!IMPORTANT]
     > **Strict Pricing Guardrail (Anti-Hallucination):** If the audited website does not explicitly publish public pricing (very common in Enterprise B2B), **DO NOT invent or extrapolate pricing tiers, hourly rates, or figures**. Explicitly set the initial pricing in `product-context.md` to `"Custom Enterprise / To be calibrated with user"` and freeze it until the user provides their real pricing model in Step 4.
3. Generate initial `.agents/rules/product-context.md` using `.agents/skills/sales-setup/references/product-template.md`. Ensure strict compliance with the `< 5,120 bytes` limit.

### Step 2: Reference Client Inquiry
Ask the user directly in chat for an ideal or past reference client:  
*Prompt Example:* "Your company profile has been analyzed and saved! To calibrate your **Ideal Customer Profile (ICP)**, what is the website URL of one of your best recent clients or an ideal target account? *(You may also briefly describe their profile if the URL is not public).*"

### Step 3: Reference Client Ingestion & ICP Abstraction
1. Analyze the reference client via `read_url_content` (or `search_web`):
   - Firmographics: Estimated headcount, industry vertical, geography, tech stack.
   - Identified operational pains and workflow bottlenecks solved.
   - Typical buying committee titles (Economic Buyer, Champion, Technical Evaluator).
2. Generalize these traits into an Ideal Customer Profile (ICP) framework rather than copying the single client verbatim.

### Step 4: Targeted Calibration (2 Explicit Questions)
Ask the user the following 2 targeted questions in chat:
1. **Question A (Pricing & Engagement Model):**  
   *Prompt Example:* "Could you confirm or adjust your standard pricing model (e.g., daily consulting rate, fixed audit package, monthly retainer, average contract value)?"
2. **Question B (Strict Exclusions & Disqualification Filters):**  
   *Prompt Example:* "What are your strict disqualification criteria (e.g., excluded industries, minimum or maximum company headcount, out-of-scope geographies, forbidden technologies)?"

### Step 5: Persistence, Visual Scaffolding & Guardrail Clearing
1. Write `.agents/rules/customer-context.md` using `.agents/skills/sales-setup/references/customer-template.md` incorporating the abstracted ICP, triggers, and calibrated disqualification rules.
2. Update `.agents/rules/product-context.md` if the user provided specific pricing packages or exclusions during Step 4.
3. Verify file sizes: both `.agents/rules/product-context.md` and `.agents/rules/customer-context.md` must be strictly `< 5,120 bytes` (target ~3 KB).
4. Compile the visual HTML dashboard: instantiate `.agents/rules/references/context-template.html` and write `reports/my-company/company-dna.html` with a dynamic state badge (`Demo Profile` or `Production Profile`). Do NOT create duplicate Markdown files in `reports/my-company/`.
5. Portal Navigation Check: Ensure `reports/index.html` links to `my-company/company-dna.html` via the top header button `🏢 My Company DNA`. NEVER add a card for the user's company into `companyGrid` in `reports/index.html`.

---

## Output & Completion Standard

Conclude the onboarding session with the mandatory Terminal Summary Block and Browser First completion block per `output-formatting.md`:

```text
=== SALES-SETUP : [COMPANY NAME] ===

Status : ACTIVE CONFIGURATION  Size : < 5 KB per rule
Configured Rules : product-context.md · customer-context.md
Visual Dashboard : reports/my-company/company-dna.html

Top Configurations:
  1. Offering & Positioning: [1-line offering synthesis]
  2. Ideal Customer Profile (ICP): [Priority targets, headcount, sectors]
  3. Pricing Model: [Calibrated pricing grid or average contract value]

Watchpoints:
  1. Strict Exclusions: [Key service exclusions applied]
  2. ICP Disqualifiers: [Key disqualification thresholds]

Recommended Action: Workspace fully calibrated! You can now run a prospect audit with `prospect <url>` or qualify a lead with `qualify <url>`.
```

Conclude your response with the clickable Browser First completion block per `output-formatting.md`.
