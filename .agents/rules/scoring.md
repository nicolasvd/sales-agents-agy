# Rule: Deterministic Scoring Frameworks

> [!IMPORTANT]
> **Language Directive:** Scoring dimensions, grades, and calculation logs operate strictly in English. All point attributions, bonuses, and penalties must be applied mechanically without optimistic bias.

## BANT Framework — 100 Total Points (25 pts per dimension)

### Budget (0–25 pts) — Willingness & Capacity to Spend
| Detected Signal | Points |
|---|---|
| Recent Series C+ / IPO (< 18 months) | +20 |
| Recent Series B (< 18 months) | +16 |
| Recent Series A (< 18 months) | +12 |
| Confirmed recurring revenue (explicit ARR mentioned) | +10 |
| Confirmed multi-tool SaaS stack | +8 |
| Active hiring in relevant product/functional category | +10 |
| Headcount > 200 | +6 |
| Headcount 50–200 | +4 |
| Cost-cutting signals, downsizings, or layoffs | −10 |

### Authority (0–25 pts) — Access to Decision-Makers
| Detected Signal | Points |
|---|---|
| Economic Buyer identified (verified name + title) | +20 |
| C-suite / VP organizational structure publicly visible | +12 |
| Flat structure (founder = sole primary decision-maker) | +15 |
| Multiple complex approval layers detected | +5 |

### Need (0–25 pts) — Intensity of the Problem
| Detected Signal | Points |
|---|---|
| Explicit pain point on website or blog (direct quotation) | +20 |
| Active job posting addressing the exact problem | +15 |
| Negative reviews on incumbent vendor (G2 / Capterra) | +12 |
| Published blog content discussing challenges in our category | +10 |
| No identifiable need signal detected | 0 |

### Timeline (0–25 pts) — Urgency & Trigger Events
| Detected Signal | Points |
|---|---|
| Trigger event < 30 days (funding, M&A, executive hire) | +20 |
| Trigger event 30–90 days | +12 |
| Active hiring surge in category | +15 |
| Confirmed fast growth (> 30%/year) | +10 |
| No urgency signal detected | 0 |

## MEDDIC Framework — Completeness (0–100%)

| Dimension | "Identified" Criterion (Confidence ≥ Medium) |
|---|---|
| **M** etrics | Business KPIs with explicit target values identified |
| **E** conomic Buyer | Name + title of primary budget holder confirmed |
| **D** ecision Criteria | Evaluation criteria explicitly stated or standard |
| **D** ecision Process | Buying evaluation process mapped (formal or informal) |
| **I** dentify Pain | Specific operational pain point documented with source |
| **C** hampion | Potential internal champion identified (name or role) |

$$\text{MEDDIC Completeness (\%)} = \left(\frac{\text{Dimensions with Medium+ Confidence}}{6}\right) \times 100$$

## Composite Formula — Prospect Score

```text
Prospect Score = (BANT × 0.50) + (MEDDIC% × 0.30) + (Urgency × 0.20)
```

**Urgency Modifier (0–100):**
| Situation | Score |
|---|---|
| Active procurement in progress or trigger event < 30 days | 80–100 |
| Trigger event < 90 days | 60–79 |
| Growth trend without immediate catalyst | 40–59 |
| Low urgency | 20–39 |
| No discernible urgency signal | 0–19 |

## Tier Grading Grid

| Score | Grade | Classification | Action Directive |
|---|---|---|---|
| 75–100 | **A — SQL** | Sales Qualified Lead | Immediate outreach, maximum priority |
| 50–74 | **B — MQL** | Marketing Qualified Lead | Standard sequence + discovery focus |
| 25–49 | **C — IQL** | Interest Qualified Lead | Nurture campaign, monitor future triggers |
| 0–24 | **D** | Unqualified | Deprioritize / Archive |
