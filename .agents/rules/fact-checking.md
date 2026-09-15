# Règle : Vérification des Faits & Navigation Web

## Hiérarchie des Sources (ordre décroissant de fiabilité)

1. Pages officielles de l'entreprise (read_url_content — toujours en premier)
2. Registres officiels : BCE Belgique, SIRENE France, Companies House UK
3. Presse spécialisée : TechCrunch, Forbes, Les Échos, PUB.be, Trends-Tendances
4. Bases de données SaaS : Crunchbase, G2, Capterra, Glassdoor (via search_web)
5. LinkedIn : via search_web uniquement (pas de scraping de profils directs)

## Pages à Explorer Systématiquement

Pour chaque prospect, tenter dans cet ordre (ignorer les erreurs 404) :
1. `/` — Homepage (obligatoire)
2. `/about` ou `/about-us` — Équipe, mission, histoire
3. `/pricing` ou `/plans` — Signaux budget et segment cible
4. `/careers` ou `/jobs` — Signaux de croissance et besoins ouverts
5. `/blog` — Maturité contenu et pain points documentés
6. `/integrations` ou `/partners` — Tech stack et écosystème
7. `/customers` ou `/case-studies` — Profil client et segments

## 5 Requêtes search_web Systématiques

Exécuter pour chaque prospect (remplacer [NOM] par le nom de l'entreprise) :
1. `"[NOM]" funding OR raised OR revenue OR valuation`
2. `"[NOM]" employees OR headcount OR hiring site:linkedin.com`
3. `"[NOM]" news OR announcement` (filtrer sur les 12 derniers mois)
4. `"[NOM]" review OR reviews site:g2.com OR site:capterra.com`
5. `"[NOM]" alternative OR competitor OR "vs "`

## Standards de Citation Obligatoires

Chaque donnée factuelle DOIT être suivie de sa source :
- **Confirmé** : Mention explicite dans une source primaire
  → `3,4 M€ de CA (Source : Forbes Belgique, juin 2026)`
- **Estimé** : Triangulation de plusieurs sources indirectes
  → `~40 employés (Estimé d'après LinkedIn + offres d'emploi, sept. 2026)`
- **Non disponible publiquement** : Si l'information est absente — jamais inventer

## Fraîcheur des Données

| Type de donnée | Fenêtre de validité |
|---|---|
| Données de scoring (Budget, Need) | ≤ 18 mois |
| Trigger events (funding, M&A, recrutement exécutif) | ≤ 90 jours |
| Données historiques (contexte uniquement) | > 18 mois → étiqueter "historique" |
