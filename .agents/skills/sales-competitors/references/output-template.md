# Template — COMPETITIVE-INTEL.md

## Output Format

Write the complete competitive intelligence report to **COMPETITIVE-INTEL.md** in the current working directory with the following structure:

```markdown
# Competitive Intelligence: [Prospect Company Name]

Generated: [Date]
Prospect: [Company Name]
Website: [URL]
Analysis Focus: Sales competitive positioning

---

## Executive Summary

[2-3 sentence summary: What the prospect currently uses, your strongest competitive position, and the recommended strategy]

---

## Current Solutions Detected

| Category | Solution | Confidence | Evidence Source |
|----------|----------|-----------|----------------|
| [Category] | [Tool] | High/Med/Low | [Source URL or signal] |
| ... | ... | ... | ... |

---

## Battle Cards

### [Competitor 1 Name]
[Full battle card]

### [Competitor 2 Name]
[Full battle card]

[Continue for each detected competitor]

---

## Feature Gap Analysis

[Side-by-side comparison table]

---

## Win/Loss Patterns

### Win Patterns
[Common reasons you win]

### Loss Patterns
[Common reasons you lose]

### Deal Qualification Signals
[Early indicators of win/loss likelihood]

---

## Competitive Positioning Statements

| Competitor | Positioning Statement |
|------------|----------------------|
| [Competitor 1] | "[Statement]" |
| [Competitor 2] | "[Statement]" |
| ... | ... |

---

## Switching Cost Assessment

| Factor | [Competitor 1] | [Competitor 2] | [Competitor 3] |
|--------|----------------|----------------|----------------|
| Technical migration | [Assessment] | [Assessment] | [Assessment] |
| Financial impact | [Assessment] | [Assessment] | [Assessment] |
| Organizational change | [Assessment] | [Assessment] | [Assessment] |
| Data portability | [Assessment] | [Assessment] | [Assessment] |
| Estimated timeline | [Timeline] | [Timeline] | [Timeline] |

---

## Recommended Competitive Strategy

[Strategy summary, conversation sequence, what to lead with, what to avoid, displacement timeline]

---

## Detection Sources

- [List all URLs fetched, searches performed, and sources consulted with dates]
```

---

## Rules and Constraints

1. **Honest about competitor strengths.** Every battle card must include genuine competitor strengths. If you portray every competitor as terrible, the salesperson loses credibility the moment the prospect pushes back.
2. **Never fabricate intelligence.** If a competitor's pricing, feature, or capability cannot be verified, label it as "Reported" or "Unverified." Sales credibility depends on accuracy.
3. **Specific over generic.** "Better customer support" is useless. "Dedicated account manager for all plans, with average response time of 2 hours vs. their 24-hour SLA" is actionable.
4. **Detection confidence matters.** Always label confidence levels on detected technologies. A High confidence detection (explicit badge on their website) carries different weight than a Low confidence inference (common tool in their industry).
5. **Never recommend bashing competitors.** The battle cards should help the salesperson position and differentiate, not attack. Negative selling backfires.
6. **Focus on what matters to THIS prospect.** Not every feature gap or competitive advantage is relevant to every deal. Prioritize the battle card content based on the prospect's likely priorities and pain points.
7. **Switching costs must be realistic.** Underestimating switching costs makes you look naive. Overestimating them makes the deal feel impossible. Be accurate.
8. **If previous analysis files exist** (PROSPECT-ANALYSIS.md, COMPANY-RESEARCH.md, LEAD-QUALIFICATION.md), incorporate findings about the prospect's priorities, pain points, and evaluation criteria into the competitive positioning.
9. **Landmine questions must be genuinely curious.** They should be questions any smart buyer would ask — not transparent traps designed to make the competitor look bad.
10. **Update frequency.** Competitive intelligence has a shelf life. Note the date of each source and recommend a refresh timeline (typically every 3-6 months or before a major competitive deal).
