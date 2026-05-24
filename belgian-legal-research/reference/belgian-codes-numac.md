# Codes belges — NUMAC + mapping thématique

Justel (la base de données législative officielle belge) attribue un **NUMAC** (numéro de Moniteur belge) par acte. Les grands codes sont éclatés sur **plusieurs NUMAC** — un par livre ou titre. Cette carte permet d'appeler `get_article` directement sans passer par `search_legislation` quand tu connais le thème.

## NUMAC racine des codes principaux

| Code | NUMAC | Notes |
|------|-------|-------|
| **ANCIEN Code civil** (1804) | `1804032150` | Articles 1 à 2281. Régime antérieur au 01-09-2021. |
| **NOUVEAU Code civil — Livre 1** (Dispositions générales) | `2022032057` | |
| **Livres 2 (titre 3+4)** (Relations patrimoniales + Successions) | `2022030600` | |
| **Livre 3** (Les biens) | `2020020347` | Vigueur 01-09-2021. |
| **Livre 5** (Les obligations) | `2022032058` | Vigueur 01-01-2023. |
| **Livre 6** (Responsabilité extracontractuelle) | `2024001600` | Vigueur 01-01-2025. |
| **Livre 8** (La preuve) | `2019012168` | |
| **Livre 9 titre 1** (Sûretés personnelles) | `2025005089` | |
| **Code judiciaire** | `1967101052` | Racine, éclaté en sous-NUMAC (ex. art. 584 référé = `1967101054`). |
| **Code pénal** | `1867060850` | |
| **Constitution** | `1994021048` | |
| **Code des sociétés et associations (CSA)** | `2019A40655` | |
| **Code de droit économique (CDE)** | (éclaté) | Cherche le bon NUMAC avec `search_legislation("Code droit économique livre IV")` etc. |

## Mapping thématique — Nouveau Code civil

### Livre 5 — Obligations (NUMAC `2022032058`)

| Thème | Articles |
|-------|----------|
| Vices du consentement (erreur, dol, violence) | 5.33 à 5.40 |
| Cause / contenu du contrat | 5.51 à 5.56 |
| Nullité absolue / relative | 5.57 à 5.65 |
| Bonne foi, abus de droit contractuel | 5.73 |
| **Imprévision / hardship / changement de circonstances** | 5.74 |
| Contrat à durée indéterminée, résiliation unilatérale | 5.75 |
| Astreinte (effet utile) | 5.84 |
| Résolution pour inexécution | 5.90 à 5.97 |
| Bail de droit commun | 5.215 à 5.234 |
| **Force majeure (régime général)** | 5.226 |
| Inexécution, exception d'inexécution | 5.235 à 5.245 |
| Cession de créance | 5.252 à 5.261 |
| Subrogation | 5.270 à 5.275 |
| Compensation | 5.318 à 5.327 |
| Prescription extinctive | 5.337 à 5.349 |

### Livre 3 — Biens (NUMAC `2020020347`)

| Thème | Articles |
|-------|----------|
| Possession | 3.16 à 3.23 |
| Propriété (attributs, démembrements) | 3.50 à 3.59 |
| **Objets abandonnés** (remplace loi 21/02/1983) | 3.58 à 3.60 |
| Troubles de voisinage | 3.101 à 3.110 |
| Servitudes | 3.114 à 3.135 |
| Usufruit | 3.138 à 3.165 |
| Emphytéose / superficie | 3.167 à 3.197 |

### Livre 8 — Preuve (NUMAC `2019012168`)

| Thème | Articles |
|-------|----------|
| Charge de la preuve | 8.4 |
| Modes de preuve, écrit, témoignage | 8.8 à 8.31 |
| Aveu, serment | 8.32 à 8.42 |

### Livre 6 — Responsabilité extracontractuelle (NUMAC `2024001600`)

| Thème | Articles |
|-------|----------|
| Concours / cumul resp. contractuelle et extracontractuelle | 6.3 |
| Faute | 6.4 à 6.10 |
| Responsabilité du fait d'autrui (parents, commettants) | 6.13 à 6.20 |
| Causalité | 6.21 à 6.27 |
| Dommage réparable | 6.28 à 6.55 |

## Code de droit économique (CDE) — relations B2B et concurrence

| Thème | Article |
|-------|---------|
| Abus de position dominante | IV.2 |
| **Abus de dépendance économique** (loi 04/04/2019) | IV.2/1 |
| Pratiques du marché B2B | livre VI titre 3/1 |
| **Clauses abusives B2B — principe (déséquilibre manifeste)** | VI.91/3 |
| Clauses abusives B2B — liste noire (toujours abusives) | VI.91/4 |
| Clauses abusives B2B — liste grise (présumées abusives) | VI.91/5 |
| Sanctions clauses abusives B2B | VI.91/6 |
| Pratiques commerciales déloyales B2B | VI.104 et s. |
| Protection du consommateur (B2C) | livre VI titre 3 (VI.82 et s.) |

## Baux

- **Bail de droit commun** : nouveau Code civil, Livre 5, art. 5.215 à 5.234 (NUMAC `2022032058`).
- **Bail à ferme** : loi spéciale (chercher via `search_legislation("bail à ferme")`).
- **Bail de résidence principale / bail commercial** : législations **régionales** (Flandre / Wallonie / Bruxelles). Chercher avec la région en mot-clé.

## Droit du logement — Région de Bruxelles-Capitale

| Acte | NUMAC | Note |
|------|-------|------|
| **Code bruxellois du Logement consolidé** (17/07/2003) | `2013A31614` | Racine. Justel ne contient parfois que 3 articles racines — vérifie toujours les ordonnances modificatives. |
| Ordonnance 27/07/2017 — Régionalisation du bail d'habitation (titre XI, art. 215 à 250) | `2017040697` | |
| Ordonnance 22/12/2023 — Modifications diverses | `2023048735` | |
| **Ordonnance 04/04/2024 — Concrétisation du droit au logement** (vigueur 01/11/2024) | `2024003465` | **Critique** : insère art. 218 §6 (clauses anti-domiciliation), 218/1 (animaux), 220/1 (assurance), 224/3 (charges), 225/1 (clauses pénales loyer), 233/1 (expulsion sans titre exécutoire). |
| Ordonnance 25/04/2024 — Enregistrement régional des baux | `2024004155` | |

**Règle pratique** : pour toute question post-2024 sur le bail bruxellois (résidence principale, étudiant, colocation, courte durée, congé, indexation, charges, sous-location, expulsion, animaux, domiciliation, assurance), interroge **les ordonnances modificatives 2024** en plus du Code consolidé. Complète par `get_article("2024003465", ...)` pour vérifier les ajouts récents.

## Droit du travail

- **Loi du 3 juillet 1978 sur les contrats de travail** : `search_legislation("contrat travail loi 1978")`.
- **Bien-être au travail** : loi du 4 août 1996.

## Procédure (Code judiciaire)

| Thème | Article |
|-------|---------|
| **Référé** | 584 |
| **Exécution provisoire** | 1397 et s. |
| Cautionnement judiciaire (garantie pour exécution provisoire) | 1400 |
| Cantonnement (consignation pour neutraliser exécution) | 1403 à 1406 |
| Saisie-arrêt | 1539 et s. |
| **Saisie immobilière** | 1560 et s. |
| **Astreinte** | 1385bis et s. |
| Exécution forcée (voies d'exécution) | 1494 et s. |

## Règle d'or — Code judiciaire vs Code civil

Quand la question contient **"jugement"**, **"exécutoire"**, **"exécution provisoire"**, **"saisie"**, **"huissier"**, **"code judiciaire"** → **le Code judiciaire prime** sur le Code civil.

Ne cite **pas** le Livre 9 "sûretés personnelles" (cautionnement civil) dans une question manifestement procédurale, même si le mot "cautionnement" apparaît — il s'agit alors du cautionnement **judiciaire** (CJ art. 1400) ou pénal.

## Stratégie d'appel

1. Tu connais le numéro d'article cible (ex: 5.74, IV.2/1) → `get_article(numac, article_number)` direct.
2. Tu ne connais pas le numéro précis → `search_legislation(query, hyde_text=...)` avec 2-4 mots juridiques précis + synonymes.
3. La première recherche échoue → reformule **une seule fois** avec d'autres mots-clés (ou angle différent), sinon passe au sous-thème suivant.

## Format de citation

Toujours `Code/Loi, article X (NUMAC: <numéro>)` — avec deux-points. Le NUMAC vient des outils, **jamais de mémoire**.
