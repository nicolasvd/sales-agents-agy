---
name: sales-contacts
description: >-
  Decision maker and buying committee identification. Maps economic buyers, champions, influencers, gatekeepers, finds public contact info and personalization anchors, saving DECISION-MAKERS.md.
---


# Skill : sales-contacts

**Rôle :** Cartographier le comité d'achat et identifier les décideurs clés.
**Règles requises :** `fact-checking.md`, `scoring.md`, `output-formatting.md`.
**Output :** `DECISION-MAKERS.md`

## Déclenchement

Invoqué par la commande `contacts <url>`. Lire si disponible :
- `COMPANY-RESEARCH.md` · `IDEAL-CUSTOMER-PROFILE.md`

## Workflow (4 étapes)

1. **Identification des contacts** — `read_url_content` : `/team`, `/about`, `/leadership`.
   `search_web` : `"[NOM]" CEO OR CTO OR VP site:linkedin.com` + variantes titres.
   Protocole exhaustif → `view_file(".agents/skills/sales-contacts/references/contact-protocol.md")`

2. **Classification du comité d'achat** — Rôle de chaque contact :
   - **Economic Buyer** : autorité budgétaire finale
   - **Champion** : utilisateur-clé qui bénéficiera du produit
   - **Influencer** : prescripteur technique ou métier
   - **Gatekeeper** : filtre administratif

3. **Ancrages de personnalisation** — Pour chaque contact prioritaire :
   Publications LinkedIn récentes · Conférences · Articles · Posts

4. **Scoring Contact Access (0–25 pts)** — Appliquer le barème Authority de `scoring.md`.

## Contraintes

- Email non trouvé = `Non disponible publiquement` (jamais inventé, jamais deviné).
- Pattern d'email = `Estimé` si déduit des conventions de domaine.
- Ne jamais scraper directement un profil LinkedIn — passer par `search_web`.

## Output

Créer `DECISION-MAKERS.md` selon le template :
`view_file(".agents/skills/sales-contacts/references/output-template.md")`

Afficher le bloc résumé terminal (format `output-formatting.md`) avant de créer le fichier.
