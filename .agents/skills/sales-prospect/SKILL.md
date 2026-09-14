---
name: sales-prospect
description: >-
  Orchestrateur pur d'audit prospect 360°. Délègue l'intégralité de la collecte et de l'analyse à 5 sous-agents en 2 vagues coordonnées via scratchpad JSON, calcule le Prospect Score et génère reports/{slug}/PROSPECT-ANALYSIS.md.
---

# Skill : sales-prospect

**Rôle :** Orchestrateur pur des 5 sous-agents internes — audit 360° d'un prospect B2B.
**Règles requises :** `scoring.md`, `output-formatting.md`.
**Output :** `reports/{slug}/PROSPECT-ANALYSIS.md`
**Sous-agents invoqués :** `sales-sub-company`, `sales-sub-contacts`, `sales-sub-competitive`, `sales-sub-opportunity`, `sales-sub-strategy`

## ⛔ Règle Bloquante (Dé-gating Strict)

> **Tu ne disposes d'aucun outil de navigation ou de recherche.**
> Il t'est FORMELLEMENT INTERDIT d'appeler `read_url_content` ou `search_web`.
> Tu dois OBLIGATOIREMENT déléguer toute collecte de données aux sous-agents via `start_subagent`.

### Outils Autorisés pour l'Orchestrateur
- `create_file` (initialisation du scratchpad, rapport final)
- `view_file` (lecture du scratchpad consolidé, ICP)
- `edit_file` (mise à jour des métadonnées du scratchpad)
- `start_subagent` (lancement des sous-agents)
- ❌ **INTERDITS :** `read_url_content`, `search_web`, `run_command`

## Déclenchement

Invoqué par la commande `prospect <url>`.
Lire si disponible : `reports/IDEAL-CUSTOMER-PROFILE.md` (via `view_file`).

## Workflow — Machine d'État Scratchpad

### 1. Initialisation du Scratchpad
1. Extraire le domaine et normaliser le nom → `{slug}` (ex. `socialsky`).
2. Créer `.agents/.scratchpad/prospect_{slug}.json` via `create_file` avec la structure initiale stricte :
```json
{
  "meta": {
    "url": "<url>",
    "slug": "{slug}",
    "status": "wave1_started"
  },
  "wave1": {
    "company_data": null,
    "contacts_data": null,
    "competitive_data": null
  },
  "wave2": {
    "opportunity_data": null,
    "strategy_data": null
  }
}
```

### 2. Vague 1 — Recherche Factuelle (Délégation Pure)
Lancer successivement les sous-agents de Vague 1 :
```
start_subagent("sales-sub-company")     → écrit wave1.company_data
start_subagent("sales-sub-contacts")    → écrit wave1.contacts_data
start_subagent("sales-sub-competitive") → écrit wave1.competitive_data
```
Lire `.agents/.scratchpad/prospect_{slug}.json` via `view_file` et vérifier que `meta.status == "wave1_complete"`.
**RÈGLE D'ARRÊT :** Ne JAMAIS déclencher la Vague 2 si `meta.status != "wave1_complete"`.

### 3. Vague 2 — Synthèse & Stratégie (Délégation Pure)
Lancer successivement les sous-agents de Vague 2 :
```
start_subagent("sales-sub-opportunity") → écrit wave2.opportunity_data (conditionné à wave1_complete)
start_subagent("sales-sub-strategy")    → écrit wave2.strategy_data
```
Vérifier `meta.status == "wave2_complete"`.

### 4. Rapports Finaux & Restitution (Double Génération MD + HTML)
1. Lire `.agents/.scratchpad/prospect_{slug}.json` via `view_file`.
2. Calculer le Prospect Score composite selon `scoring.md` :
   `Prospect Score = (BANT × 0,50) + (MEDDIC% × 0,30) + (Urgency × 0,20)`
3. **Générer le rapport Markdown :** `create_file("reports/{slug}/PROSPECT-ANALYSIS.md")` selon le template :
   `view_file(".agents/skills/sales-prospect/references/output-template.md")`.
4. **Générer l'Artifact HTML autonome :** `create_file("reports/{slug}/PROSPECT-ANALYSIS.html")` en instanciant le template :
   `view_file(".agents/rules/references/report-template.html")` (remplacer les variables avec les données réelles et les jauges SVG).
5. Afficher le bloc résumé terminal conforme à `output-formatting.md`.

## Contraintes
- Zéro recherche directe : toute information provient exclusivement du scratchpad rempli par les sous-agents.
- Les sous-agents `sales-sub-*` sont des modules internes : ne pas les exposer dans le rapport final.
- Les deux livrables MD et HTML doivent être créés systématiquement sous `reports/{slug}/`.
