---
name: sales-competitors
description: >-
  Competitive intelligence and battle card generator. Identifies direct/indirect competitors, compares features, pricing, and positioning, and creates competitive battle cards in COMPETITIVE-INTEL.md.
---


# Skill : sales-competitors

**Rôle :** Analyser le paysage concurrentiel d'un prospect et générer des battle cards.
**Règles requises :** `fact-checking.md`, `output-formatting.md`.
**Output :** `COMPETITIVE-INTEL.md`

## Déclenchement

Invoqué par la commande `competitors <url>`. Lire :
- `COMPANY-RESEARCH.md` · `PROSPECT-ANALYSIS.md` si disponibles
- `IDEAL-CUSTOMER-PROFILE.md` (technographic profile)

## Workflow (5 étapes)

1. **Détection des outils actuels** — `read_url_content` : `/integrations`, `/partners`.
   `search_web` : `"[NOM]" site:stackshare.io`, `"[NOM]" uses OR "built with"`.

2. **Catégorisation** — Classer chaque outil :
   - Concurrent direct (même catégorie que notre produit)
   - Concurrent indirect (résout le même problème différemment)
   - Outil complémentaire (peut intégrer avec notre produit)
   - Outil à déplacer (notre produit le remplace)

3. **Battle cards** — Une card par concurrent direct (max 4) :
   Notre force · Leur force · Nos angles d'attaque · Leurs angles d'attaque · Script de différenciation.
   Template détaillé : `view_file(".agents/skills/sales-competitors/references/battle-card-template.md")`

4. **Analyse des gaps** — Identifier les fonctionnalités manquantes dans l'outil actuel
   que notre produit adresse (basé sur `product-context.md` et les reviews G2/Capterra).

5. **Évaluation du switching cost** — Faible / Moyen / Élevé selon l'ancienneté et les intégrations.

## Contraintes

- ❌ Ne jamais dénigrer un concurrent nommément sans données sourcées.
- Chaque gap identifié = review ou job posting source entre parenthèses.

## Output

Créer `COMPETITIVE-INTEL.md` selon le template :
`view_file(".agents/skills/sales-competitors/references/output-template.md")`
