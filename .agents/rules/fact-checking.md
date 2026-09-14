# Règle : Vérification des Faits & Navigation Web

## Hiérarchie des Sources (ordre décroissant de fiabilité)

1. Pages officielles de l'entreprise (navigation web — toujours en premier)
2. Registres officiels : BCE Belgique, SIRENE France, Companies House UK
3. Presse spécialisée : TechCrunch, Forbes, Les Échos, PUB.be, Trends-Tendances
4. Bases de données SaaS : Crunchbase, G2, Capterra, Glassdoor (via search_web)
5. LinkedIn : via search_web uniquement (pas de scraping direct de profils)

## Protocole de Navigation & Stratégie de Fallback Chrome

### Priorité 1 : Extraction Rapide (`read_url_content`)
- Méthode par défaut sur l'ensemble des pages web cibles (exécution ultra-rapide).
- Valide si le contenu extrait est structuré, intelligible et supérieur à **200 caractères de contenu utile**.

### Priorité 2 (Fallback) : Sous-Agent Chrome (`/browser`)
Déléguer impérativement l'accès au sous-agent Chrome (`/browser`) dans les cas suivants :
1. **Rendu dynamique requis :** Applications monopages (SPA React, Vue, Next.js, Angular) dont le contenu n'est pas pré-rendu.
2. **Protection & Blocage :** Pages protégées par Cloudflare, antibot, challenges JavaScript ou renvoyant des erreurs HTTP 403/429.
3. **Contenu utile insuffisant :** Si `read_url_content` renvoie **moins de 200 caractères de texte utile** (ex. "Please enable JavaScript" ou loader vide).
- **Objectif :** Extraire le DOM hydraté après exécution du JavaScript pour garantir une vérité terrain complète.

## Pages à Explorer Systématiquement

Pour chaque prospect, tenter dans cet ordre (ignorer les 404) :
1. `/` — Homepage (obligatoire)
2. `/about` ou `/about-us` — Équipe, mission, fondateurs
3. `/pricing` ou `/plans` — Signaux budget et segment de marché
4. `/careers` ou `/jobs` — Signaux de croissance et besoins techniques ouverts
5. `/blog` — Maturité marketing et défis traités
6. `/integrations` ou `/partners` — Écosystème logiciel et stack SaaS
7. `/customers` ou `/case-studies` — Preuves sociales et typologie client

## 5 Requêtes search_web Systématiques

Exécuter pour chaque prospect (remplacer `[NOM]` par le nom officiel) :
1. `"[NOM]" funding OR raised OR revenue OR valuation`
2. `"[NOM]" employees OR headcount OR hiring site:linkedin.com`
3. `"[NOM]" news OR announcement` (filtrer sur les 12 derniers mois)
4. `"[NOM]" review OR reviews site:g2.com OR site:capterra.com`
5. `"[NOM]" alternative OR competitor OR "vs "`

## Standards de Citation Obligatoires

Chaque donnée factuelle DOIT être suivie de sa source :
- **Confirmé :** Mention explicite dans une source primaire
  → `3,4 M€ de CA (Source : Forbes Belgique, juin 2026)`
- **Estimé :** Triangulation de sources indirectes
  → `~40 employés (Estimé d'après LinkedIn + offres d'emploi, sept. 2026)`
- **Non disponible publiquement :** Si l'information est absente — jamais inventer

## Fraîcheur des Données

| Type de donnée | Fenêtre de validité |
|---|---|
| Données de scoring (Budget, Need) | ≤ 18 mois |
| Trigger events (funding, M&A, recrutement exécutif) | ≤ 90 jours |
| Données historiques (contexte uniquement) | > 18 mois → étiqueter "historique" |
