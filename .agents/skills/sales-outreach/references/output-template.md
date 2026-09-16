# Output Template — OUTREACH-SEQUENCE.md

Utiliser ce template pour structurer le fichier de sortie.

Phase 1: Personalization Research (Before Writing Any Email)

**CRITICAL RULE:** Never write a single email before completing personalization research. Generic outreach is worse than no outreach. Every email must contain at least one specific, verifiable reference to the prospect or contact.

### 1.1 Company Trigger Research

Use `search_web` to find recent company triggers. These create natural, timely reasons to reach out.

**Search queries to execute:**
```
"[company name] funding"
"[company name] product launch"
"[company name] hiring"
"[company name] partnership announcement"
"[company name] expansion"
"[company name] news"
"[company name] CEO interview"
```

**Trigger event categories:**

| Trigger Category | Detection Signals | Outreach Angle | Freshness Requirement |
|-----------------|-------------------|----------------|----------------------|
| **Recent Funding** | Press release, Crunchbase, news articles | "Congrats on the raise — growth usually means [problem you solve]" | Last 6 months |
| **Product Launch** | Blog post, Product Hunt, press release | "Saw you launched [product] — we help companies like yours [benefit]" | Last 3 months |
| **Hiring Spree** | 10+ open roles, new departments, leadership hires | "Your team is growing fast — that usually creates [challenge]" | Last 3 months |
| **Leadership Change** | New CEO/CTO/VP announcement, LinkedIn updates | "Congrats on the new role — new leaders often reassess [area]" | Last 3 months |
| **Expansion** | New office, new market, international move | "Saw you're expanding into [market] — we've helped others navigate [challenge]" | Last 6 months |
| **Partnership** | Integration announcement, channel partnership | "Your partnership with [company] is interesting — we integrate with them too" | Last 6 months |
| **Award/Recognition** | Industry award, ranking, media feature | "Congrats on [award] — well-deserved given your work on [area]" | Last 6 months |

**Trigger quality rating:**
- **Hot trigger (use immediately):** Happened in the last 30 days. Directly relevant to your solution.
- **Warm trigger (use within a week):** Happened in the last 90 days. Related to your solution area.
- **Cool trigger (use as context):** Happened 3-6 months ago. Provides background but not urgency.

### 1.2 Personal Trigger Research

Research the specific person you are targeting. Use `search_web` for each priority contact:

```
"[contact name] [company name] LinkedIn"
"[contact name] [company name] interview"
"[contact name] [company name] presentation"
"[contact name] [company name] article"
```

**Personal trigger categories:**

| Trigger | Detection | Outreach Angle |
|---------|-----------|----------------|
| **New Role** | LinkedIn profile shows recent start date | "Congrats on joining [company] — first 90 days are a great time to [action]" |
| **Promotion** | LinkedIn update, press release | "Congrats on the promotion — with the new scope, [problem] might be on your radar" |
| **Recent Post/Article** | LinkedIn post, Medium article, blog | "Your post about [topic] resonated — especially the point about [specific detail]" |
| **Speaking Engagement** | Conference website, YouTube, podcast directory | "Caught your talk at [event] on [topic] — your take on [point] was refreshing" |
| **Career Milestone** | Anniversary post, LinkedIn milestone | "10 years in [industry] is impressive — I imagine you've seen [evolution]" |
| **Published Content** | Articles, whitepapers, ebooks, newsletter | "Your piece on [topic] in [publication] was great — particularly [specific insight]" |

### 1.3 Industry Trigger Research

Identify broader industry dynamics that create urgency:

```
"[industry] trends 2025 2026"
"[industry] challenges"
"[industry] new regulation"
"[industry] technology disruption"
"[industry] market shift"
```

**Industry trigger categories:**

| Trigger | Outreach Angle |
|---------|----------------|
| **New Regulation** | "With [regulation] taking effect, companies like yours need to [action]" |
| **Market Shift** | "The shift toward [trend] is creating [challenge] for [industry] companies" |
| **Competitor Move** | "Now that [competitor] has [action], the market is moving toward [direction]" |
| **Technology Disruption** | "[New technology] is changing how [industry] companies handle [process]" |
| **Economic Conditions** | "In the current [economic condition], [industry] leaders are prioritizing [area]" |

### 1.4 Personalization Research Summary

Before writing emails, compile a research summary:

```
PERSONALIZATION RESEARCH
========================
Company: [name]
Primary Contact: [name, title]

Company Triggers Found:
  1. [Trigger] — [date] — Quality: [Hot/Warm/Cool]
  2. [Trigger] — [date] — Quality: [Hot/Warm/Cool]

Personal Triggers Found:
  1. [Trigger] — [date] — Quality: [Hot/Warm/Cool]
  2. [Trigger] — [date] — Quality: [Hot/Warm/Cool]

Industry Triggers Found:
  1. [Trigger] — [date] — Quality: [Hot/Warm/Cool]

Best Opening Angle: [which trigger to lead with and why]
Secondary Angle: [backup approach for follow-up emails]
```

---

## Phase 6: Sending Best Practices

### 6.1 Email Deliverability

| Practice | Recommendation |
|----------|---------------|
| **Send volume** | Start with 10-20 emails/day per inbox, warm up gradually to 50/day |
| **Email warmup** | Warm new email addresses for 2-3 weeks before cold outreach |
| **Domain setup** | Use a separate sending domain (e.g., mail.company.com) to protect primary domain reputation |
| **Authentication** | Ensure SPF, DKIM, and DMARC are configured |
| **Unsubscribe** | Include an unsubscribe option (CAN-SPAM compliance) |
| **Bounce handling** | Remove bounced addresses immediately |
| **Spam testing** | Test emails through mail-tester.com before sending |

### 6.2 Send Timing

| Audience | Best Days | Best Times | Avoid |
|----------|-----------|-----------|-------|
| **C-suite / VP** | Tuesday, Wednesday, Thursday | 7-8 AM or 5-6 PM (before/after meetings) | Monday AM, Friday PM |
| **Directors / Managers** | Tuesday, Wednesday, Thursday | 9-11 AM | Monday AM, Friday PM |
| **Technical / IC** | Tuesday, Wednesday | 10 AM - 12 PM | Monday, Friday |
| **Founders / Startup** | Any weekday, Saturday morning | 7-9 AM or 8-10 PM (they work odd hours) | Sunday |

### 6.3 Follow-Up Rules

| Scenario | Action |
|----------|--------|
| **No response to all 5 emails** | Wait 30 days, then re-approach with a completely new angle or trigger event |
| **Out-of-office reply** | Note their return date and re-send Email 1 the day after they return |
| **"Not interested" reply** | Respond graciously. Ask if there's someone else who might benefit. Remove from sequence. |
| **"Not now" reply** | Ask when would be better. Set a reminder. Send a value-add resource in the meantime. |
| **Positive reply** | Respond within 1 hour. Propose specific meeting times (2-3 options). Keep momentum. |
| **Question reply** | Answer the question directly and concisely. Then redirect to a meeting. |

---

## Output Format: OUTREACH-SEQUENCE.md

Write the full output to `OUTREACH-SEQUENCE.md` in the current directory:

```markdown
# Cold Outreach Sequence: [Company Name]
**Target Contact:** [Name, Title]
**Company:** [Company Name]
**Date:** [current date]
**Outreach Readiness Score: [X]/100**
**Selected Framework:** [framework name]

---

## Prospect Summary

| Field | Value |
|-------|-------|
| **Company** | [name] |
| **Industry** | [vertical] |
| **Company Size** | [employees] |
| **Target Contact** | [name, title] |
| **Buying Role** | [role] |
| **Email (estimated)** | [email based on pattern] |
| **LinkedIn** | [profile URL or search] |

---

## Personalization Research

### Company Triggers
1. **[Trigger]** — [date] — Quality: [Hot/Warm/Cool]
   *Outreach angle:* [how to use this]
2. **[Trigger]** — [date] — Quality: [Hot/Warm/Cool]
   *Outreach angle:* [how to use this]

### Personal Triggers
1. **[Trigger]** — [date] — Quality: [Hot/Warm/Cool]
   *Outreach angle:* [how to use this]
2. **[Trigger]** — [date] — Quality: [Hot/Warm/Cool]
   *Outreach angle:* [how to use this]

### Industry Triggers
1. **[Trigger]** — Quality: [Hot/Warm/Cool]
   *Outreach angle:* [how to use this]

---

## Selected Framework: [Framework Name]

**Reasoning:** [2-3 sentences on why this framework was selected
based on the available personalization data and prospect context]

---

## Full 5-Email Sequence

### Email 1: The Hook (Day 1)

**Subject Line A:** [subject]
**Subject Line B:** [subject]

---

[Full email body — copy-paste ready]

---

**CTA:** [specific ask]
**LinkedIn Touchpoint:** Day 0 — Connection request: "[custom note text]"

#### A/B Variations
**Opening Line A:** [primary opening]
**Opening Line B:** [alternative opening]

---

### Email 2: The Value Add (Day 3)

**Subject Line A:** [subject]
**Subject Line B:** [subject]

---

[Full email body — copy-paste ready]

---

**CTA:** [specific ask or soft close]
**LinkedIn Touchpoint:** Day 5 — Engage with their content (like + comment)

#### A/B Variations
**Opening Line A:** [primary opening]
**Opening Line B:** [alternative opening]

---

### Email 3: The Social Proof (Day 7)

**Subject Line A:** [subject]
**Subject Line B:** [subject]

---

[Full email body — copy-paste ready]

---

**CTA:** [specific ask]
**LinkedIn Touchpoint:** Day 10 — LinkedIn message: "[message text]"

#### A/B Variations
**Opening Line A:** [primary opening]
**Opening Line B:** [alternative opening]

---

### Email 4: The Different Angle (Day 14)

**Subject Line A:** [subject]
**Subject Line B:** [subject]

---

[Full email body — copy-paste ready]

---

**CTA:** [specific ask]
**LinkedIn Touchpoint:** Day 18 — Share relevant content

#### A/B Variations
**Opening Line A:** [primary opening]
**Opening Line B:** [alternative opening]

---

### Email 5: The Breakup (Day 21)

**Subject Line A:** [subject]
**Subject Line B:** [subject]

---

[Full email body — copy-paste ready, under 75 words]

---

**CTA:** [soft close]

#### A/B Variations
**Opening Line A:** [primary opening]
**Opening Line B:** [alternative opening]

---

## LinkedIn Touchpoint Summary

| Day | Action | Content |
|-----|--------|---------|
| 0 | Connection request | [custom note text] |
| 5 | Engage with content | Like + comment on recent post about [topic] |
| 10 | LinkedIn message | [message text] |
| 18 | Share content | [content to share and why] |

---

## Sending Best Practices

- **Best send time for this contact:** [day/time based on their role]
- **Send from:** [recommended — personal email, not marketing]
- **Format:** Plain text (no HTML, no images, no tracking pixels for first email)
- **Follow-up if no response to sequence:** Wait 30 days, then re-approach with [new angle]

---

## Objection Preparation

| Likely Objection | Response |
|-----------------|----------|
| "[Objection 1]" | [2-3 sentence response] |
| "[Objection 2]" | [2-3 sentence response] |
| "[Objection 3]" | [2-3 sentence response] |

---

*Generated by AI Sales Team — `/sales outreach`*
```

---

## Terminal Output

Display a condensed summary in the terminal:

```
=== OUTREACH SEQUENCE GENERATED ===

Prospect:  [company name]
Contact:   [name], [title]
Framework: [selected framework]

Outreach Readiness Score: [X]/100
  Personalization:    [XX]/25 ████████░░
  Trigger Events:     [XX]/25 ██████░░░░
  Channel Strategy:   [XX]/25 ███████░░░
  Message-Market Fit: [XX]/25 █████░░░░░

Sequence Overview:
  Email 1 (Day 1):  The Hook — [subject line A]
  Email 2 (Day 3):  The Value Add — [subject line A]
  Email 3 (Day 7):  The Social Proof — [subject line A]
  Email 4 (Day 14): The Different Angle — [subject line A]
  Email 5 (Day 21): The Breakup — [subject line A]

LinkedIn Touchpoints: 4 (Day 0, 5, 10, 18)

Best Send Time: [day/time recommendation]
Email Pattern: [detected pattern]

Full sequence saved to: OUTREACH-SEQUENCE.md
```

---

## Error Handling

- If no personalization data is found, note the limitation and use industry-level personalization (weakest approach)
- If the contact's LinkedIn profile is not found, proceed with company-level personalization only
- If no case study or proof point is available for Email 3, use an industry benchmark or third-party data
- If the prospect company has very limited online presence, focus on industry triggers and general pain points
- Always generate a complete 5-email sequence regardless of personalization quality, but clearly note when emails rely on weak personalization
- If running as subagent and time is limited, prioritize Email 1 quality over completeness of emails 4-5

## Cross-Skill Integration

- If `COMPANY-RESEARCH.md` exists, use company data for personalization and context
- If `DECISION-MAKERS.md` exists, use contact profiles and personalization anchors
- If `LEAD-QUALIFICATION.md` exists, use pain points and buying signals for messaging
- If `COMPETITIVE-INTEL.md` exists, use competitive positioning for differentiation angles
- Suggest follow-up: `/sales prep` for meeting preparation after getting a response, `/sales followup` for post-meeting sequence, `/sales objections` for deeper objection handling
