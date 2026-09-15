---
name: sales
description: >-
  Main orchestrator for the AI Sales Team. Coordinates all 13 specialized sales workflows including prospect auditing, lead qualification, contacts mapping, outreach sequences, and pipeline reporting.
---

# AI Sales Team — Main Orchestrator

Plateforme d'intelligence commerciale B2B 100 % déclarative pour Google Antigravity.
Orchestre 13 compétences de prospection et 5 sous-agents internes, sans aucun script ni dépendance externe.

## Répertoire des Commandes

| Commande | Description | Output |
|---|---|---|
| `qualify <url>` | Qualification BANT (0-100) + MEDDIC | `reports/{slug}/LEAD-QUALIFICATION.md` |
| `research <url>` | Analyse firmographique sur 8 dimensions | `reports/{slug}/COMPANY-RESEARCH.md` |
| `contacts <url>` | Cartographie du comité d'achat & décideurs | `reports/{slug}/DECISION-MAKERS.md` |
| `prospect <url>` | Audit 360° complet (5 sous-agents en 2 vagues) | `reports/{slug}/PROSPECT-ANALYSIS.md` |
| `outreach <prospect>` | Séquence cold 5 touches + LinkedIn | `reports/{slug}/OUTREACH-SEQUENCE.md` |
| `followup <prospect>` | Séquence de relance multi-scénarios | `reports/{slug}/FOLLOWUP-SEQUENCE.md` |
| `prep <url>` | Brief de préparation de réunion (10 points) | `reports/{slug}/MEETING-PREP.md` |
| `proposal <client>` | Proposition commerciale personnalisée | `reports/{slug}/CLIENT-PROPOSAL.md` |
| `competitors <url>` | Détection de stack & Battle Cards | `reports/{slug}/COMPETITIVE-INTEL.md` |
| `icp <description>` | Définition ICP + grille de scoring | `reports/IDEAL-CUSTOMER-PROFILE.md` |
| `objections <topic>` | Playbook de traitement d'objections (A-R-C) | `reports/OBJECTION-PLAYBOOK.md` |
| `report` | Rapport pipeline agrégé | `reports/PIPELINE-SUMMARY.md` |

## Logique d'Aiguillage

Lors de l'appel d'une commande, charger le skill correspondant dans `.agents/skills/<skill>/SKILL.md`.

### Audit Complet (`prospect <url>`)
Orchestré par `sales-prospect` via un scratchpad sur disque (`.agents/.scratchpad/prospect_{slug}.json`) en 2 vagues :
- **Vague 1 (Recherche) :** `sales-sub-company`, `sales-sub-contacts`, `sales-sub-competitive`
- **Vague 2 (Synthèse) :** `sales-sub-opportunity` (BANT/MEDDIC), `sales-sub-strategy` (Outreach)

### Règles Transversales Obligatoires
Toute exécution doit respecter :
- `AGENTS.md` (point d'entrée, passivité absolue, zéro hallucination)
- `.agents/rules/fact-checking.md` (sources primaires, citations)
- `.agents/rules/scoring.md` (barèmes BANT/MEDDIC déterministes)
- `.agents/rules/product-context.md` (offre produit, prix, personas)
- `.agents/rules/output-formatting.md` (bloc terminal + formats Markdown)
