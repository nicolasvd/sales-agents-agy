# Radar Discovery Output Template

Use this template to generate `reports/pipeline/markdown/RADAR-DISCOVERY.md`.

```markdown
# Opportunity Radar: Temporal Trigger & Event-Driven Discovery

**Scan Date:** {{SCAN_DATE}}  
**Target Focus:** {{TARGET_FOCUS}}  
**Geographic Scope:** {{GEO_SCOPE}}  
**Audited Horizon:** Dual Window (Forward J+15..90 & Retrospective J-60..0)  
**Configuration Status:** {{STATUS_BADGE}}

---

## Executive Summary

- **Surfaced Accounts:** 5 verified accounts matching ICP criteria.
- **Trigger Distribution:** {{TRIGGER_DISTRIBUTION}} (e.g., 3 Forward Catalysts, 2 Retrospective Accelerations).
- **Core Value Proposition Alignment:** Grounded in `.agents/rules/product-context.md`.

---

## Surfaced High-Readiness Accounts

### 1. {{COMPANY_1_NAME}}
- **Domain:** [{{COMPANY_1_DOMAIN}}]({{COMPANY_1_URL}})
- **Sector & HQ:** {{COMPANY_1_SECTOR}} · {{COMPANY_1_LOCATION}}
- **Temporal Window:** {{COMPANY_1_WINDOW}} (Forward J+15..90 | Retrospective J-60..0)
- **Verified Trigger Event:** {{COMPANY_1_TRIGGER}}
- **Source & Date:** {{COMPANY_1_SOURCE}} ({{COMPANY_1_DATE}})
- **Target Persona:** {{COMPANY_1_PERSONA}}
- **Strategic Entry Hook:** {{COMPANY_1_HOOK}}
- **Instant Next Action:**
  ```bash
  prospect {{COMPANY_1_URL}}
  ```

### 2. {{COMPANY_2_NAME}}
- **Domain:** [{{COMPANY_2_DOMAIN}}]({{COMPANY_2_URL}})
- **Sector & HQ:** {{COMPANY_2_SECTOR}} · {{COMPANY_2_LOCATION}}
- **Temporal Window:** {{COMPANY_2_WINDOW}}
- **Verified Trigger Event:** {{COMPANY_2_TRIGGER}}
- **Source & Date:** {{COMPANY_2_SOURCE}} ({{COMPANY_2_DATE}})
- **Target Persona:** {{COMPANY_2_PERSONA}}
- **Strategic Entry Hook:** {{COMPANY_2_HOOK}}
- **Instant Next Action:**
  ```bash
  prospect {{COMPANY_2_URL}}
  ```

### 3. {{COMPANY_3_NAME}}
- **Domain:** [{{COMPANY_3_DOMAIN}}]({{COMPANY_3_URL}})
- **Sector & HQ:** {{COMPANY_3_SECTOR}} · {{COMPANY_3_LOCATION}}
- **Temporal Window:** {{COMPANY_3_WINDOW}}
- **Verified Trigger Event:** {{COMPANY_3_TRIGGER}}
- **Source & Date:** {{COMPANY_3_SOURCE}} ({{COMPANY_3_DATE}})
- **Target Persona:** {{COMPANY_3_PERSONA}}
- **Strategic Entry Hook:** {{COMPANY_3_HOOK}}
- **Instant Next Action:**
  ```bash
  prospect {{COMPANY_3_URL}}
  ```

### 4. {{COMPANY_4_NAME}}
- **Domain:** [{{COMPANY_4_DOMAIN}}]({{COMPANY_4_URL}})
- **Sector & HQ:** {{COMPANY_4_SECTOR}} · {{COMPANY_4_LOCATION}}
- **Temporal Window:** {{COMPANY_4_WINDOW}}
- **Verified Trigger Event:** {{COMPANY_4_TRIGGER}}
- **Source & Date:** {{COMPANY_4_SOURCE}} ({{COMPANY_4_DATE}})
- **Target Persona:** {{COMPANY_4_PERSONA}}
- **Strategic Entry Hook:** {{COMPANY_4_HOOK}}
- **Instant Next Action:**
  ```bash
  prospect {{COMPANY_4_URL}}
  ```

### 5. {{COMPANY_5_NAME}}
- **Domain:** [{{COMPANY_5_DOMAIN}}]({{COMPANY_5_URL}})
- **Sector & HQ:** {{COMPANY_5_SECTOR}} · {{COMPANY_5_LOCATION}}
- **Temporal Window:** {{COMPANY_5_WINDOW}}
- **Verified Trigger Event:** {{COMPANY_5_TRIGGER}}
- **Source & Date:** {{COMPANY_5_SOURCE}} ({{COMPANY_5_DATE}})
- **Target Persona:** {{COMPANY_5_PERSONA}}
- **Strategic Entry Hook:** {{COMPANY_5_HOOK}}
- **Instant Next Action:**
  ```bash
  prospect {{COMPANY_5_URL}}
  ```

---

## Methodological Guardrails
- All domains verified reachable via web extraction.
- Zero speculative signals: every event is explicitly dated and sourced.
- Strictly filtered against ICP boundaries from `.agents/rules/customer-context.md`.
```
