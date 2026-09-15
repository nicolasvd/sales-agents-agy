---
name: sales-outreach
description: >-
  Cold outreach email and LinkedIn sequence generator. Designs highly personalized 5-touch omnichannel outreach sequences based on company triggers and pains, saving OUTREACH-SEQUENCE.md.
---


# Skill : sales-outreach

**Rôle :** Générer une séquence cold 5 touches omnicanal (email + LinkedIn) hautement
personnalisée, ancrée sur des déclencheurs réels vérifiés.
**Règles requises :** `product-context.md`, `fact-checking.md`, `output-formatting.md`.
**Output :** `OUTREACH-SEQUENCE.md`

## Déclenchement

Invoqué par la commande `outreach <nom_prospect>`. Lire d'abord :
- `PROSPECT-ANALYSIS.md` si disponible (audit complet)
- `DECISION-MAKERS.md` si disponible (contacts identifiés)
- `IDEAL-CUSTOMER-PROFILE.md` si disponible (calibration ICP)

## Workflow (6 étapes)

1. **Collecte de contexte** — Lire les fichiers de rapports existants dans le workspace.
2. **Recherche de déclencheurs** — `search_web` : funding, product launch, hiring, news < 90 jours.
   Si besoin de la taxonomie complète → `view_file(".agents/skills/sales-outreach/references/outreach-frameworks.md")`
3. **Sélection du framework** — Choisir parmi 4 frameworks (Observation→Connection→Ask,
   Problème→Preuve→Ask, Trigger Event, Mutual Connection) selon les données collectées.
4. **Rédaction de la séquence 5 touches** — Email J1, LinkedIn J3, Email J7, Email J14, Email J21.
   Chaque message : accroche déclencheur + proposition de valeur (`product-context.md`) + CTA minimal.
5. **Intégration LinkedIn** — Profil engage-first si décideur actif LinkedIn.
6. **Scoring Outreach Readiness** — Sur 100, selon les barèmes de `scoring.md`.

## Contraintes Absolues

- ❌ Ne jamais écrire un email avant d'avoir au moins 1 déclencheur réel et vérifiable.
- ❌ Aucune fonctionnalité produit non documentée dans `product-context.md`.
- ❌ Aucun envoi réel — output = brouillons uniquement.
- ✅ Chaque email < 100 mots, CTA = 1 question ouverte.

## Output

Créer `OUTREACH-SEQUENCE.md` selon le template dans :
`view_file(".agents/skills/sales-outreach/references/output-template.md")`

Afficher le bloc résumé terminal (format `output-formatting.md`) avant de créer le fichier.
