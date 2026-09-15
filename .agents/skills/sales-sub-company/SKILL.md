---
name: sales-sub-company
description: >-
  Sous-agent interne de sales-prospect. Analyse les firmographics, signaux financiers, tech stack et signaux de croissance d'un prospect. Invoqué par start_subagent en Vague 1.
---

# Sous-Agent : Company Research (`sales-sub-company`)

**Rôle :** Firmographics, financiers, tech stack, signaux de croissance.
**Poids dans le Prospect Score :** Company Fit = 25%.
**Règles requises :** `fact-checking.md`, `scoring.md`, `output-formatting.md`.
**Invocateur :** `sales-prospect` (Vague 1).

## Input Reçu (Pattern Scratchpad)

**Avant toute action**, lire le scratchpad de session :
```
view_file(".agents/.scratchpad/prospect_{slug}.json")
```
Extraire : `meta.url`, `meta.company_name` et le snapshot initial.
Si le fichier n'existe pas, demander à l'orchestrateur `sales-prospect` de l'initialiser.

Le champ `{slug}` est le nom d'entreprise normalisé (minuscules, sans espaces ni caractères spéciaux).

## Protocole d'Exécution

### Étape 1 — Pages Internes (read_url_content)
Fetcher dans l'ordre, ignorer les 404 :
1. `{url}/about` ou `/about-us` → Taille, mission, date de fondation, localisations
2. `{url}/pricing` ou `/plans` → Segment cible, tiers, signaux budget
3. `{url}/careers` ou `/jobs` → Rythme de recrutement, fonctions clés, signaux tech
4. `{url}/blog` ou `/resources` → Maturité, pain points thématiques
5. `{url}/integrations` ou `/partners` → Tech stack, écosystème SaaS

### Étape 2 — Recherche Externe (search_web)
Exécuter les 5 requêtes systématiques de `fact-checking.md` avec le nom de l'entreprise.
Extraire : montants de financement, dates, effectifs, taux de croissance confirmés.

### Étape 3 — Scoring Company Fit (0–25 pts)
Appliquer le barème Budget de `scoring.md` sur les signaux collectés.
Documenter chaque point attribué avec la source correspondante.

## Output — Écriture dans le Scratchpad

Une fois l'analyse complète, écrire les résultats dans le scratchpad via `edit_file` :
Chemin : `.agents/.scratchpad/prospect_{slug}.json`
Champ à mettre à jour : `wave1.company_data`

```json
{
  "company_name": "...",
  "hq_location": "...",
  "employee_count": "...",
  "founded": "...",
  "revenue_signals": "...",
  "funding": {"stage": "...", "amount": "...", "date": "..."},
  "tech_stack": ["..."],
  "growth_signals": ["..."],
  "company_fit_score": 0,
  "sources": ["url1", "query1"]
}
```

Mettre également à jour `meta.status` → `"company_done"` après l'écriture.
