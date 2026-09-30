---
name: sales-radar
description: >-
  Temporal trigger and event-driven prospect discovery engine. Surfaces high-readiness target accounts based on forward catalysts (J+15..90) and retrospective acceleration signals (J-60..0), strictly filtered against customer-context.md.
---

# Skill: sales-radar

**Role:** Autonomous temporal prospect discovery engine. Identifies and qualifies high-readiness B2B accounts driven by real-world events, trade shows, regulatory deadlines, and executive appointments.  
**Mode:** One-shot direct execution (non-interactive, zero conversational questions).  
**Mandatory Context:** `.agents/context/customer-context.md` (mandatory), `.agents/context/product-context.md` (mandatory), `.agents/context/output-formatting.md`.  
**Mandatory Rules:** `.agents/rules/fact-checking.md` (mandatory).  
**Deliverables:** `reports/radar/RADAR-DISCOVERY.html` and `reports/radar/markdown/RADAR-DISCOVERY.md`.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, search queries, and analytical notes operate strictly in English. Customer-facing summaries and deliverable content adapt to the user's primary operating language.

## Triggers & Arguments

- **Bare Command (`radar`):**  
  Automatically extracts default target sectors and primary geographic footprint from `.agents/context/customer-context.md`.
- **Targeted Argument (`radar <sector / event / temporal anchor>`):**  
  Accepts specific industry topics, event types, or explicit temporal markers (e.g., `radar fintech`, `radar trade fair autumn 2026`, `radar AI Act compliance`). The argument sets the primary search anchor while `.agents/context/customer-context.md` remains the mandatory band-pass filter.

---

## Workflow (4 Sequential Steps)

> [!IMPORTANT]
> **Re-run & Refresh Policy:** When explicitly invoked with a target prospect URL or topic, systematically execute a fresh web exploration. Overwrite existing local reports with updated findings and today's date (`audit_date`). Never use existing local markdown files as a substitute for an explicit user re-run.

### Step 1: Context Ingestion & Workspace Guardrail Verification
1. **Demo Profile Check:** Inspect `.agents/rules/fact-checking.md`. If the demo marker (`Acme AI Automation Inc.` or default Acme profile) is active, prepend the canonical warning banner in chat.
2. **ICP Band-Pass Filter Loading:** Read `.agents/context/customer-context.md`:
   - Geographic Scope (e.g., France, Belgium, Western Europe, North America).
   - Headcount & Revenue sweet spots and strict disqualification thresholds (< 10 or > 1,500 employees).
   - Target Buying Committee personas (COO, VP Ops, VP Engineering, Champion).
3. **Offering Alignment:** Read `.agents/context/product-context.md` to map solution pillars (workflow automation, team enablement, agent integration) to upcoming triggers.

### Step 2: Dual-Window Temporal Signal Scouting (`search_web`)
Execute targeted search queries covering both temporal horizons:
1. **Forward Horizon (J+15 to J+90 / Upcoming 2026 Catalysts):**
   - Trade fairs, expos, and summits: query registered exhibitors, conference speakers, or sponsors.
   - Regulatory milestones: compliance deadlines (e.g., CSRD reporting, NIS2 cybersecurity, EU AI Act enforcement).
2. **Retrospective Horizon (J-60 to J-0 / Recent Acceleration Signals):**
   - Executive appointments: recent hires of COO, VP Ops, VP Engineering, or Head of AI/Transformation.
   - Capital injection: Seed, Series A/B funding rounds or major expansion announcements.
   - Operational expansion: public initiatives modernizing business workflows or open engineering/ops roles.

### Step 3: Anti-Hallucination & Account Validation
1. **Strict 5-Account Cap:** Select exactly 5 high-readiness accounts.
2. **Reachable Public URL Verification:** Validate domain accessibility using `read_url_content` (verify homepage resolves with legitimate business content). Zero hallucinated URLs or dummy names.
3. **ICP Disqualification Filter:** Filter out any company violating criteria in `.agents/context/customer-context.md` (insufficient size, legacy on-prem lock-in, pure B2C).
4. **Strategic Entry Angle:** For each account, craft a concise hook connecting the verified trigger to a specific value proposition pillar from `.agents/context/product-context.md`.
5. **Instant Action Hook:** Pre-format the direct command `prospect <url>` for each account.

### Step 4: Dual Output Generation & Hub Sync
1. **Web HTML (Humans):** Write `reports/radar/RADAR-DISCOVERY.html` using `.agents/skills/sales-radar/references/radar-template.html` (Light SaaS theme, responsive cards, direct action commands).
2. **Raw Markdown (AI Memory):** Write `reports/radar/markdown/RADAR-DISCOVERY.md` using `.agents/skills/sales-radar/references/output-template.md`.
3. **Portal Navigation Check:** Ensure `reports/index.html` links to `radar/RADAR-DISCOVERY.html` via the top header button `📡 Opportunity Radar`. NEVER inject Opportunity Radar as a company card into `companyGrid`.
4. Conclude with the executive summary and deliverable completion block per `.agents/context/output-formatting.md`.

---

## Output & Completion Standard

Deliver the executive synthesis and the list of surfaced opportunities directly in fluid Markdown per `.agents/context/output-formatting.md`. Conclude your response with the standard deliverables completion block:

### 📦 Deliverables Generated
- **Web:** `reports/radar/RADAR-DISCOVERY.html`
- **AI Data:** `reports/radar/markdown/RADAR-DISCOVERY.md`
- **Portal Updated:** `reports/index.html`
