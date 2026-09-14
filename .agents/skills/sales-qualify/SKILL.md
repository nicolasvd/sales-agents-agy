---
name: sales-qualify
description: >-
  Lead qualification engine using BANT (Budget, Authority, Need, Timeline) and MEDDIC frameworks. Analyzes prospects from public web data, scores opportunity quality (0-100), and outputs LEAD-QUALIFICATION.md.
---


# Skill : sales-qualify

**Rôle :** Qualifier un prospect via BANT + MEDDIC depuis des données web publiques.
**Règles requises :** `scoring.md` (obligatoire), `fact-checking.md`, `output-formatting.md`.
**Output :** `LEAD-QUALIFICATION.md`

## Déclenchement

Invoqué par la commande `qualify <url>`. Lire si disponible :
- `IDEAL-CUSTOMER-PROFILE.md` — pour calibrer le scoring ICP

## Workflow (4 étapes)

1. **Collecte de données** — `read_url_content` sur les pages clés :
   `/` → `/about` → `/pricing` → `/careers` → `/blog`
   Puis 5 requêtes `search_web` systématiques (voir `fact-checking.md`).
   Protocole détaillé signal par signal →
   `view_file(".agents/skills/sales-qualify/references/scoring-protocol.md")`

2. **Scoring BANT** — Appliquer mécaniquement les barèmes de `scoring.md` :
   Budget /25 · Authority /25 · Need /25 · Timeline /25 = BANT /100

3. **Complétude MEDDIC** — Évaluer les 6 éléments M-E-D-D-I-C sur les données collectées.
   `Complétude = (éléments confirmés / 6) × 100 %`

4. **Prospect Score composite** :
   `Score = BANT × 0,50 + MEDDIC% × 0,30 + Urgency × 0,20`
   Grade : A (75-100) · B (50-74) · C (25-49) · D (0-24)

## Contraintes

- Chaque point attribué = source documentée entre parenthèses.
- Zéro estimation non étiquetée. Information absente → `Non disponible publiquement`.
- Un prospect médiocre reçoit un score médiocre — pas d'optimisme commercial.

## Output (Double Livrable Obligatoire)

Créer simultanément dans `reports/{slug}/` :
1. **Markdown :** `reports/{slug}/LEAD-QUALIFICATION.md` selon le template :
   `view_file(".agents/skills/sales-qualify/references/output-template.md")`
2. **HTML Autonome :** `reports/{slug}/LEAD-QUALIFICATION.html` selon le template :
   `view_file(".agents/rules/references/report-template.html")`

Afficher le bloc résumé terminal en début de réponse et le **bloc de clôture avec liens cliquables** en fin de réponse (conforme à `output-formatting.md`).
