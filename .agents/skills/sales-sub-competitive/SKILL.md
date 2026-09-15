---
name: sales-sub-competitive
description: >-
  Sous-agent interne de sales-prospect. Identifie les outils actuels du prospect, les coûts de migration et les angles concurrentiels exploitables. Invoqué par start_subagent en Vague 1.
---

# Sous-Agent : Competitive Positioning (`sales-sub-competitive`)

**Rôle :** Outils actuels, coûts de migration, gaps exploitables, angles concurrentiels.
**Poids dans le Prospect Score :** Competitive Position = 15%.
**Règles requises :** `fact-checking.md`, `output-formatting.md`.
**Invocateur :** `sales-prospect` (Vague 1).

## Input Reçu (Pattern Scratchpad)

**Avant toute action**, lire le scratchpad :
```
view_file(".agents/.scratchpad/prospect_{slug}.json")
```
Extraire : `meta.url`, `meta.company_name`, `wave1.company_data.tech_stack`.
Si absent, continuer avec le snapshot homepage.

## Protocole d'Exécution

### Étape 1 — Détection des Outils Actuels (read_url_content)
1. `{url}/integrations` ou `/partners` → Stack explicite
2. `{url}/careers` → Outils requis dans les JDs (ex: "Salesforce experience required")
3. `{url}/blog` → Mentions d'outils dans les articles techniques

### Étape 2 — Intelligence Externe (search_web)
1. `"[NOM]" site:stackshare.io OR site:builtwith.com`
2. `"[NOM]" uses OR "powered by" OR "built with"`
3. `"[NOM]" "[CATÉGORIE PRODUIT]" review OR alternative`
4. `"[OUTIL CONCURRENT PRINCIPAL]" vs "[NOTRE PRODUIT]"` (signaux de comparaison)

### Étape 3 — Évaluation du Switching Cost

| Facteur | Impact |
|---|---|
| Outil actuel < 12 mois → faible adoption | Switching cost : Faible |
| Outil actuel > 2 ans + intégrations multiples | Switching cost : Élevé |
| Avis négatifs récents sur l'outil actuel | Switching cost : Réduit |
| Aucun outil actuel détecté (greenfield) | Opportunité : Forte |

### Étape 4 — Scoring Competitive Position (0–15 pts)
Évaluer sur la base du switching cost et des gaps détectés.

## Output — Écriture dans le Scratchpad

Écrire via `edit_file` dans `.agents/.scratchpad/prospect_{slug}.json` :
Champ : `wave1.competitive_data` + mettre à jour `meta.status` → `"wave1_complete"`

```json
{
  "current_tools": ["Outil A (Confirmé)", "Outil B (Estimé)"],
  "switching_cost": "Faible|Moyen|Élevé",
  "competitive_gaps": ["Gap 1 exploitable", "Gap 2"],
  "positioning_angle": "...",
  "competitive_score": 0,
  "sources": ["url1", "query1"]
}
```
