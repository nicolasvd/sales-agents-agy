---
name: sales-icp
description: >-
  Ideal Customer Profile (ICP) builder. Explores a new target segment or refines the buyer profile without overwriting product positioning, saving ICP-FRAMEWORK.md.
---

# Skill: sales-icp

**Role:** Explore a new target segment or refine buyer personas and scoring rubrics without overwriting overall product positioning.  
**Mandatory Rules:** `customer-context.md` (mandatory), `scoring.md` (mandatory), `fact-checking.md` (mandatory), `output-formatting.md`.  
**Deliverables:** `reports/my-company/ICP-FRAMEWORK.html` and `reports/my-company/markdown/ICP-FRAMEWORK.md`.

> [!IMPORTANT]
> **Language Governance:** Internal market analysis, scoring matrices, and logic operate in English. Deliverable content adapts to the primary business language of the target market.

## Trigger

Invoked via `icp [segment]*`. Used to explore a new target segment or refine the buyer profile without overwriting the rest of the product positioning. Mandatorily inspect `.agents/rules/customer-context.md` as the baseline for deep sector analysis and ICP refinement. The `[segment]` argument is an optional description of the target market, vertical, or buyer persona provided by the user.

## Workflow (3 Sequential Steps)

1. **Market Intelligence & Target Validation:**
   - Execute `search_web` to uncover segment benchmarks, average contract values (ACV), and buying triggers.
   - Run `read_url_content` on representative target customer domains to validate firmographic and technographic baselines.

2. **ICP Architecture (12 Structured Dimensions):**
   1. *Firmographic Criteria:* Sector, headcount brackets, geographic markets, ARR/revenue thresholds.
   2. *Technographic Stack:* Required software, digital maturity level, infrastructure dependencies.
   3. *Behavioral Signals:* Buying catalysts, active recruitment patterns, leadership changes.
   4. *Pain Point Matrix:* Operational bottlenecks ranked by intensity and frequency.
   5. *Budget Qualifiers:* Indicators of purchasing power and commercial viability.
   6. *Channel Strategy:* Most effective engagement channels (LinkedIn, email, partner introductions).
   7. *Negative ICP (Mandatory):* Minimum 3 strict disqualifying criteria (e.g., inadequate size, incompatible stack).
   8. *Scoring Rubric (0–100):* Weighted criteria mechanically compatible with `scoring.md`.
   9. *Buyer Personas:* 2–3 granular profiles (Economic Buyer, Champion, Influencer).
   10. *Prospecting Playbook:* Tactical qualification cues and recommended outreach angles.
   11. *Competitive Positioning:* Incumbent presence and switching barrier dynamics.
   12. *Maintenance Protocol:* Bi-annual review criteria and performance tuning.
   Reference specification: `view_file(".agents/skills/sales-icp/references/icp-sections-detail.md")`.

3. **Workspace Calibration:**
   - Cross-check the formulated rubric against existing reports (`PROSPECT-ANALYSIS.html`, `LEAD-QUALIFICATION.html`) to validate qualification accuracy.

## Strict Guardrails

- All criteria must be derived from verifiable industry benchmarks, never ungrounded assumptions.
- Rubric weights must strictly align with the arithmetic scoring baselines of `scoring.md`.
- Negative ICP is mandatory: a profile without clear exclusion criteria is rejected.

## Mandatory Dual Output

Save both deliverables simultaneously strictly within `reports/my-company/`:
1. **Web HTML (Humans):** `reports/my-company/ICP-FRAMEWORK.html` using `view_file(".agents/rules/references/context-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/my-company/markdown/ICP-FRAMEWORK.md` using `view_file(".agents/skills/sales-icp/references/icp-sections-detail.md")`.

> [!CAUTION]
> **Strict Prohibition:** Never write any file directly at the root of `reports/` (e.g., `reports/IDEAL-CUSTOMER-PROFILE.html` is strictly forbidden).

Display the Executive Briefing Card (Modern Markdown) at the start of your chat response. Conclude your response with the clickable Browser First completion block per `output-formatting.md`.

### Post-Execution Interaction
After providing the completion block, optionally prompt the user:
> *"Would you like to apply these criteria as the active target profile in `.agents/rules/customer-context.md`?"*
