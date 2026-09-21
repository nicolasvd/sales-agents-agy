# Template — MEETING-PREP.md

## Output Format

Write the complete meeting preparation brief to `reports/{slug}/markdown/MEETING-PREP.md` with the following structure:

```markdown
---
slug: "[slug]"
company: "[Company Name]"
url: "[url or Not publicly available]"
type: "prep"
audit_date: "YYYY-MM-DD"
meeting_date: "[If provided]"
primary_contact: "[Primary Contact Name, Title]"
meeting_goal: "[Core objective]"
---

# Meeting Preparation Brief: [Company Name]

Generated: [Date]
Meeting Date: [If provided]
Meeting Purpose: [If provided]
Prepared By: AI Sales Assistant

---

## CHEAT SHEET

[5 most important things + opening line + key question + trap to avoid]

---

## 1. Company Snapshot

[Paragraph overview + quick-reference table]

---

## 2. Attendee Profiles

[Profile block for each attendee]

---

## 3. Business Situation

[Current state, recent changes, growth trajectory, key challenges, opportunities]

---

## 4. Competitive Context

[Current solutions, switching triggers, what not to say, your differentiation]

---

## 5. Talking Points

[5-7 personalized talking points with context and what they lead to]

---

## 6. Discovery Questions

[10 ordered questions with purpose, expected response, follow-up, listen-for signals]

---

## 7. Objections to Expect

[5 likely objections with Feel-Felt-Found responses and proof points]

---

## 8. Success Metrics

[Minimum, target, and stretch success outcomes]

---

## 9. Competitive Landmines

[Topics to avoid with handling strategies]

---

## 10. Next Steps to Propose

[Bold, standard, and minimum next step options with exact wording]

---

## Suggested Agenda

[Meeting structure template based on duration]

---

## Research Sources

- [List of all URLs fetched and sources consulted]
```

---

## Rules and Constraints

1. **Everything must be specific to THIS prospect.** No generic advice. Every talking point, question, objection, and recommendation must reference specific details from the research.
2. **Evidence-based claims only.** Cite the source for every factual claim (website page, news article, LinkedIn post). Do not speculate without labeling it as inference.
3. **Respect the prospect's intelligence.** Do not include manipulative tactics, NLP tricks, or psychological pressure techniques. This is preparation for a professional business conversation.
4. **Actionable over comprehensive.** A salesperson should be able to read the Cheat Sheet in 60 seconds and walk into the meeting confident. Depth is in the supporting sections.
5. **If attendee names are not provided**, still generate the Attendee Profiles section using likely attendees based on the meeting type and company size. Label these as "Predicted Attendees" and note the confidence level.
6. **If previous analysis files exist** in the workspace (`reports/{slug}/markdown/` including `PROSPECT-ANALYSIS.md`, `COMPANY-RESEARCH.md`, `LEAD-QUALIFICATION.md`, `COMPETITIVE-INTEL.md`, `DECISION-MAKERS.md`), read them and incorporate their findings. Do not re-research what has already been analyzed.
7. **Time-sensitive accuracy.** Use search_web to verify any information that may have changed recently (leadership, funding, product launches). Note the date of each source.
8. **The Cheat Sheet is the most important section.** If the salesperson reads nothing else, the Cheat Sheet alone should make them meaningfully more prepared than walking in blind.
9. **Discovery questions must be genuinely curious.** They should be questions the salesperson actually wants to know the answer to — not leading questions designed to manipulate the prospect into a predetermined conclusion.
10. **Competitor references must be factual.** Never fabricate competitive intelligence. If a competitor's weakness cannot be verified, label it as "commonly reported" or omit it.
