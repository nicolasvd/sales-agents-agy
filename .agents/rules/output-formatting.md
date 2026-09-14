# Règle : Format des Sorties & Double Livrable (Markdown + HTML)

## Bloc Résumé Terminal (Obligatoire en début de réponse)

Ce bloc apparaît EN PREMIER dans la réponse textuelle, avant tout développement :

```
=== [NOM DU SKILL EN MAJUSCULES] : [NOM ENTREPRISE] ===

[SCORE PRINCIPAL] : [X]/100  Grade : [A/B/C/D]
[Sous-scores si applicable, ex: Budget: 18/25  Authority: 20/25]

Top Signaux :
  1. [Signal le plus fort — preuve factuelle entre parenthèses]
  2. [Signal 2 — source]
  3. [Signal 3 — source]

Red Flags :
  1. [Point de vigilance principal]
  2. [Point de vigilance secondaire si pertinent]

Action recommandée : [Phrase d'action concrète, une seule ligne]
```

## Règle du Double Livrable (Dual Output MD + HTML)

Tout skill produisant un livrable dans `reports/{slug}/` ou `reports/` doit **OBLIGATOIREMENT** générer simultanément deux versions du livrable :
1. **La version Markdown brute :** `reports/{slug}/{LIVRABLE}.md` (pour indexation, grep et historique VCS).
2. **La version HTML autonome :** `reports/{slug}/{LIVRABLE}.html` (CSS inline moderne, typographie système, composants visuels, @media print A4 sans dépendance externe).

### Répertoire des Livrables & Templates Associés

| Skill | Livrable Markdown | Livrable HTML Autonome | Template de Référence |
|---|---|---|---|
| `sales-prospect` | `PROSPECT-ANALYSIS.md` | `PROSPECT-ANALYSIS.html` | `.agents/rules/references/report-template.html` |
| `sales-outreach` | `OUTREACH-SEQUENCE.md` | `OUTREACH-SEQUENCE.html` | `.agents/rules/references/outreach-template.html` |
| `sales-prep` | `MEETING-PREP.md` | `MEETING-PREP.html` | `.agents/rules/references/meeting-prep-template.html` |
| `sales-proposal` | `CLIENT-PROPOSAL.md` | `CLIENT-PROPOSAL.html` | `.agents/rules/references/proposal-template.html` |
| `sales-qualify` | `LEAD-QUALIFICATION.md` | `LEAD-QUALIFICATION.html` | `.agents/rules/references/report-template.html` |
| `sales-research` | `COMPANY-RESEARCH.md` | `COMPANY-RESEARCH.html` | `.agents/rules/references/report-template.html` |
| `sales-contacts` | `DECISION-MAKERS.md` | `DECISION-MAKERS.html` | `.agents/rules/references/report-template.html` |
| `sales-competitors` | `COMPETITIVE-INTEL.md` | `COMPETITIVE-INTEL.html` | `.agents/rules/references/report-template.html` |
| `sales-followup` | `FOLLOWUP-SEQUENCE.md` | `FOLLOWUP-SEQUENCE.html` | `.agents/rules/references/outreach-template.html` |
| `sales-report` | `PIPELINE-SUMMARY.md` | `PIPELINE-SUMMARY.html` | `.agents/rules/references/report-template.html` |
| `sales-icp` | `IDEAL-CUSTOMER-PROFILE.md` | `IDEAL-CUSTOMER-PROFILE.html` | `.agents/rules/references/report-template.html` |
| `sales-objections` | `OBJECTION-PLAYBOOK.md` | `OBJECTION-PLAYBOOK.html` | `.agents/rules/references/report-template.html` |

## Standard du Bloc de Clôture (Liens Cliquables Obligatoires)

Chaque réponse d'un skill doit **IMPÉRATIVEMENT se terminer** par un bloc de clôture clair contenant les liens absolus directs cliquables vers les deux fichiers générés :

```markdown
---
### 📁 Livrables Générés
- 📄 **Markdown :** [NOM-DU-FICHIER.md](file://{ABSOLUTE_WORKSPACE_PATH}/reports/{slug}/NOM-DU-FICHIER.md)
- 🌐 **Version Web / Print :** [NOM-DU-FICHIER.html](file://{ABSOLUTE_WORKSPACE_PATH}/reports/{slug}/NOM-DU-FICHIER.html)
```

*(Remplacer `{ABSOLUTE_WORKSPACE_PATH}` par le chemin absolu du workspace actif, par exemple `/Users/nicolasvd/antigravity/sales-agents-agy`)*.

## Règles de Mise en Forme HTML & Print
- **CSS Inline & Autonomie :** Zéro dépendance à des CDN externes (Google Fonts, Tailwind CDN, FontAwesome). Tout le style réside dans la balise `<style>` du document.
- **Typographie Système :** `-apple-system, BlinkMacSystemFont, "Inter", "Segoe UI", Roboto, sans-serif`.
- **Export PDF / Impression A4 :** `@page { margin: 12mm 15mm; size: A4; }`, `print-color-adjust: exact;`, cartes protégées contre les coupures (`break-inside: avoid;`).
