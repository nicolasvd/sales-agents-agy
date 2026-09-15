---
name: sales-qualify
description: >-
  Lead qualification engine using BANT (Budget, Authority, Need, Timeline) and MEDDIC frameworks. Analyzes prospects from public web data, scores opportunity quality (0-100), and outputs LEAD-QUALIFICATION.md.
---

# Skill: sales-qualify

**Role:** Qualify prospects using BANT + MEDDIC frameworks exclusively from public web intelligence.  
**Mandatory Rules:** `scoring.md` (mandatory), `fact-checking.md`, `output-formatting.md`.  
**Deliverables:** `reports/{slug}/LEAD-QUALIFICATION.html` and `reports/{slug}/markdown/LEAD-QUALIFICATION.md`.

> [!IMPORTANT]
> **Language Governance:** Internal reasoning, search queries, and scoring logs operate in English. The final deliverable automatically adapts to the primary language of the audited company.

## Trigger

Invoked via `qualify <url>`. If available, inspect:
- `reports/IDEAL-CUSTOMER-PROFILE.html` or `reports/markdown/IDEAL-CUSTOMER-PROFILE.md` — to calibrate ICP alignment.

## Workflow (4 Sequential Steps)

1. **Web Intelligence Gathering:**
   - Run `read_url_content` across core pages: `/` → `/about` → `/pricing` → `/careers` → `/blog`.
   - Execute 5 systematic `search_web` queries per `fact-checking.md` (news, leadership, hiring, financials, tech).
   - Detailed signal mapping protocol: `view_file(".agents/skills/sales-qualify/references/scoring-protocol.md")`.

2. **Deterministic BANT Scoring:**
   - Mechanically apply scorecards from `scoring.md`:
     Budget (/25) · Authority (/25) · Need (/25) · Timeline (/25) = BANT Score (/100).

3. **MEDDIC Completeness Assessment:**
   - Assess 6 core dimensions (Metrics, Economic Buyer, Decision Criteria, Decision Process, Identify Pain, Champion).
   - Calculate `MEDDIC Completeness = (confirmed elements / 6) × 100%`.

4. **Composite Prospect Score Calculation:**
   - Compute formula: `Score = (BANT × 0.50) + (MEDDIC% × 0.30) + (Urgency × 0.20)`.
   - Assign tier: Grade A (75–100) · Grade B (50–74) · Grade C (25–49) · Grade D (0–24).

## Strict Guardrails

- Every awarded point must reference a verified public source in parentheses.
- Zero speculative estimation. Unverifiable signals = `Not publicly available` (0 pts).
- Deterministic integrity: a mediocre prospect mechanically receives a mediocre score.

## Mandatory Dual Output

Save both deliverables simultaneously within `reports/{slug}/`:
1. **Web HTML (Humans):** `reports/{slug}/LEAD-QUALIFICATION.html` using `view_file(".agents/rules/references/report-template.html")`.
2. **Raw Markdown (AI Memory):** `reports/{slug}/markdown/LEAD-QUALIFICATION.md` using `view_file(".agents/skills/sales-qualify/references/output-template.md")`.

Display the Terminal Summary Block at the start of your chat response, and conclude with the mandatory 3-link completion block:

```markdown
---
### 📁 Generated Deliverables
- 🌐 **Web / Print Version (Humans):** [LEAD-QUALIFICATION.html](reports/{slug}/LEAD-QUALIFICATION.html)
- 📄 **Raw Machine Data (AI):** [LEAD-QUALIFICATION.md](reports/{slug}/markdown/LEAD-QUALIFICATION.md)
- 📑 **Global Reports Portal:** [index.html](reports/index.html)
```
