---
name: sales-icp
description: >-
  Ideal Customer Profile (ICP) builder. Establishes firmographic, technographic, behavioral, and negative qualification criteria with a scoring rubric, saving IDEAL-CUSTOMER-PROFILE.md.
---


# Skill : sales-icp

**Rôle :** Définir le Profil Client Idéal (ICP) avec scoring rubric pour ce workspace.
**Règles requises :** `fact-checking.md`, `output-formatting.md`.
**Output :** `IDEAL-CUSTOMER-PROFILE.md`

## Déclenchement

Invoqué par la commande `icp <description>`.
La `<description>` est une description libre du marché cible fournie par l'utilisateur.

## Workflow (3 étapes)

1. **Recherche marché** — Basée sur la description fournie :
   `search_web` : typologies de clients, benchmarks sectoriels, signaux de budget.
   `read_url_content` : sites de clients cibles représentatifs pour valider les critères.

2. **Construction de l'ICP** — 12 dimensions structurées :
   - Critères firmographiques (secteur, taille, géographie, revenus)
   - Profil technographique (stack, maturité digitale)
   - Signaux comportementaux (triggers d'achat, patterns)
   - Carte des pain points (intensité × fréquence)
   - Qualificateurs budget
   - Stratégie de canal préférée
   - ICP négatif (qui éviter absolument)
   - Rubrique de scoring (0–100, critères pondérés)
   - Personas acheteurs (2–3 profils détaillés)
   - Playbook de prospection
   - Contexte concurrentiel
   - Guide de maintenance
   Détail de chaque section :
   `view_file(".agents/skills/sales-icp/references/icp-sections-detail.md")`

3. **Calibration** — Si des rapports `PROSPECT-ANALYSIS.md` ou `LEAD-QUALIFICATION.md`
   existent, les utiliser pour valider et affiner les critères de l'ICP.

## Contraintes

- L'ICP est basé sur des données marché vérifiées, pas des suppositions.
- La rubrique de scoring DOIT être cohérente avec les barèmes de `scoring.md`.
- L'ICP négatif est obligatoire (au moins 3 critères d'exclusion).

## Output

Créer `IDEAL-CUSTOMER-PROFILE.md`. Ce fichier sera lu par les autres skills
pour calibrer leur scoring. Structure exhaustive dans le template de référence.
