---
name: sales-icp
description: >-
  Ideal Customer Profile (ICP) builder. Establishes firmographic, technographic, behavioral, and negative qualification criteria with a scoring rubric, saving IDEAL-CUSTOMER-PROFILE.md.
---

# Skill: sales-icp

**Role:** Define and calibrate the Ideal Customer Profile (ICP), negative disqualification rules, and deterministic scoring rubrics for the workspace.  
**Mandatory Rules:** `scoring.md` (mandatory), `fact-checking.md`, `output-formatting.md`.  
**Deliverables:** `reports/IDEAL-CUSTOMER-PROFILE.html` and `reports/markdown/IDEAL-CUSTOMER-PROFILE.md`.

> [!IMPORTANT]
> **Language Governance:** Internal market analysis, scoring matrices, and logic operate in English. Deliverable content adapts to the primary business language of the target market.

## Trigger

Invoked via `icp <description>`. The `<description>` argument is a freeform summary of the target market or solution focus provided by the user.

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

Save both deliverables simultaneously within `reports/`:
1. **Web HTML (Humans):** `reports/IDEAL-CUSTOMER-PROFILE.html` using `view_file(".agents/rules/references/report-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/markdown/IDEAL-CUSTOMER-PROFILE.md` using `view_file(".agents/skills/sales-icp/references/icp-sections-detail.md")`.

Display the Terminal Summary Block at the start of your chat response, and conclude with the mandatory Browser First completion block per `output-formatting.md`:

```text
=== LIVRABLES GÉNÉRÉS ===
📄 Fichier Web : reports/IDEAL-CUSTOMER-PROFILE.html
🤖 Données IA  : reports/markdown/IDEAL-CUSTOMER-PROFILE.md

🚀 Ouvrir dans le navigateur :
open reports/IDEAL-CUSTOMER-PROFILE.html
```
