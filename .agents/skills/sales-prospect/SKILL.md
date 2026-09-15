---
name: sales-prospect
description: >-
  Comprehensive 360-degree prospect audit launching 5 parallel analytical agents (Company Fit, Contacts, Opportunity, Competitive, Outreach Strategy) to calculate a composite Prospect Score (0-100) and save PROSPECT-ANALYSIS.md.
---


# Skill : sales-prospect

**Rôle :** Orchestrateur des 5 sous-agents internes — audit 360° d'un prospect B2B.
**Règles requises :** `fact-checking.md`, `scoring.md`, `output-formatting.md`.
**Output :** `PROSPECT-ANALYSIS.md`
**Sous-agents invoqués :** `sales-sub-company`, `sales-sub-contacts`, `sales-sub-competitive`,
`sales-sub-opportunity`, `sales-sub-strategy`

## Déclenchement

Invoqué par la commande `prospect <url>`.
Lire si disponible : `IDEAL-CUSTOMER-PROFILE.md`

## Workflow — Machine d'État Scratchpad

### Initialisation
1. Normaliser le nom d'entreprise → `{slug}` (minuscules, sans espaces).
2. `create_file(".agents/.scratchpad/prospect_{slug}.json")` avec structure initiale :
```json
{
  "meta": {"url": "...", "company_name": "...", "slug": "...", "status": "wave1_started"},
  "wave1": {"company_data": null, "contacts_data": null, "competitive_data": null},
  "wave2": {"opportunity_data": null, "strategy_data": null}
}
```
3. `read_url_content(url)` → snapshot homepage initial.

### Vague 1 — Recherche Indépendante (3 sous-agents)
```
start_subagent("sales-sub-company")    → écrit wave1.company_data
start_subagent("sales-sub-contacts")   → écrit wave1.contacts_data
start_subagent("sales-sub-competitive")→ écrit wave1.competitive_data
```
Vérifier `meta.status == "wave1_complete"` avant de passer à la Vague 2.

### Vague 2 — Synthèse (2 sous-agents, dépendent de la Vague 1)
```
start_subagent("sales-sub-opportunity")→ écrit wave2.opportunity_data
start_subagent("sales-sub-strategy")   → écrit wave2.strategy_data
```

### Rapport Final
1. `view_file(".agents/.scratchpad/prospect_{slug}.json")` → lire le contexte consolidé.
2. Calculer le Prospect Score composite (formule dans `scoring.md`).
3. Créer `PROSPECT-ANALYSIS.md` selon le template :
   `view_file(".agents/skills/sales-prospect/references/output-template.md")`
4. Afficher le bloc résumé terminal.
5. Optionnel : supprimer le scratchpad (ou le conserver pour debug).

## Contraintes

- Ne jamais lancer la Vague 2 si `meta.status != "wave1_complete"`.
- Les `sales-sub-*` sont des composants internes — ne pas les documenter dans le rapport final.
- Prospect Score = `BANT × 0,50 + MEDDIC% × 0,30 + Urgency × 0,20` (cf. `scoring.md`).
