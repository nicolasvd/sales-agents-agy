# Antigravity Scratchpad Specification & Canonical Schema

Transient inter-agent buffer for multi-agent workflows orchestrated by `sales-prospect`.

> [!IMPORTANT]
> **Ephemeral Storage:** Files (`prospect_{slug}.json`) are ephemeral session buffers ignored by Git. Coordination metadata, reasoning, and JSON schemas operate strictly in English.

## Canonical JSON Schema

```json
{
  "meta": {
    "url": "https://target-company.com",
    "slug": "target-company",
    "status": "wave1_started | wave1_complete | opportunity_done | wave2_complete",
    "created_at": "ISO-8601 UTC timestamp",
    "updated_at": "ISO-8601 UTC timestamp"
  },
  "wave1": {
    "company_data": {
      "company_name": "string", "hq_location": "string", "employee_count": "string",
      "founded": "string", "business_model": "string", "revenue_signals": "string",
      "funding": { "stage": "string", "amount": "string", "date": "string" },
      "tech_stack": [], "growth_signals": [], "sources": []
    },
    "contacts_data": {
      "buying_committee": [{
        "name": "string", "title": "string", "role": "Economic Buyer | Champion | Influencer | Gatekeeper",
        "email": "string", "linkedin": "string", "personalization_anchor": "string"
      }],
      "email_pattern": "string", "decision_process_signals": "string", "sources": []
    },
    "competitive_data": {
      "current_tools": [], "switching_cost": "Low | Medium | High",
      "switching_cost_rationale": "string", "competitive_gaps": [], "sources": []
    }
  },
  "wave2": {
    "opportunity_data": {
      "bant": {
        "budget": { "score": 0, "signals": [], "rationale": "" },
        "authority": { "score": 0, "signals": [], "rationale": "" },
        "need": { "score": 0, "signals": [], "rationale": "" },
        "timeline": { "score": 0, "signals": [], "rationale": "" }
      },
      "bant_total": 0,
      "meddic": {
        "metrics": "Identified | Absent", "economic_buyer": "Identified | Absent",
        "decision_criteria": "Identified | Absent", "decision_process": "Identified | Absent",
        "identify_pain": "Identified | Absent", "champion": "Identified | Absent",
        "completeness_pct": 0
      },
      "opportunity_quality_score": 0
    },
    "strategy_data": {
      "primary_channel": "LinkedIn | Email | Phone | Warm intro",
      "primary_contact": { "name": "", "title": "", "rationale": "" },
      "top_triggers": [], "message_angle": { "hook": "", "pain_to_value_bridge": "", "cta": "" },
      "likely_objections": [], "outreach_readiness_score": 0
    }
  }
}
```

## Lifecycle State Machine (`meta.status`)

1. `wave1_started`: Set by `sales-prospect`. Wave 1 subagents launched.
2. `wave1_complete`: Set when Wave 1 data is populated. **Barrier:** Required before Wave 2 starts.
3. `opportunity_done`: Set by `sales-sub-opportunity` after deterministic BANT/MEDDIC scoring.
4. `wave2_complete`: Set by `sales-sub-strategy`. Triggers final report rendering by `sales-prospect`.
