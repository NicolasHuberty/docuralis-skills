# Vocabulaire juridique belge — synonymes et termes polysémiques

Le législateur belge emploie un vocabulaire technique différent du langage courant. La recherche full-text PostgreSQL stemme indépendamment chaque mot et **ne connaît pas les synonymes** : si tu cherches "locataire" mais que le code dit "preneur", tu rates l'article.

## Règle d'injection

Quand tu rédiges une requête `search_legislation` ou `search_jurisprudence`, **inclus à la fois** le terme courant et le terme légal (ou les variantes) **dans la même requête**.

✓ `search_legislation("domiciliation preneur locataire bail Bruxelles interdire", hyde_text=...)`
✗ `search_legislation("clause domiciliation locataire")` ← rate les articles utilisant "preneur"

## Table des synonymes

### Baux et logement
- **locataire** ↔ **preneur**
- **bailleur** ↔ **propriétaire** ↔ **loueur**
- **logement** ↔ **bien loué** ↔ **immeuble loué** ↔ **habitation**
- **bail** ↔ **contrat de location** ↔ **louage**
- **indexation** ↔ **révision du loyer**
- **garantie locative** ↔ **caution locative** ↔ **dépôt de garantie**
- **domiciliation** ↔ **se domicilier** ↔ **inscription registre population** ↔ **résidence principale**

### Sortie de relation
- **congé** ↔ **renon** ↔ **résiliation**
- **licenciement** ↔ **congédiement** ↔ **rupture du contrat de travail**

### Travail
- **employé** ↔ **travailleur** ↔ **salarié**

### Responsabilité
- **dommage** ↔ **préjudice**
- **faute** ↔ **négligence** ↔ **imprudence**

### Sûretés et garanties
- **caution** ↔ **cautionnement** ↔ **garantie**

### Procédure et exécution
- **saisie** ↔ **exécution forcée**

## Termes polysémiques — vérifier le contexte AVANT de choisir la source

Certains mots couvrent 2-3 régimes juridiques distincts. **Identifie le contexte** dans la question (indices : "jugement", "pénal", "garant", "instruction", etc.) avant de chercher.

### `cautionnement` — 3 sens distincts

| Indices dans la question | Régime | Localisation |
|--------------------------|--------|--------------|
| "jugement", "exécution provisoire", "exécutoire par provision" | **Cautionnement judiciaire** | Code judiciaire art. 1400 — garantie financière imposée par le juge pour conditionner l'exécution provisoire |
| "caution", "garant", "engagement personnel", "sûreté personnelle" | **Cautionnement civil** | Code civil Livre 9 titre 1 (NUMAC `2025005089`) |
| "pénal", "inculpé", "liberté provisoire", "instruction" | **Cautionnement pénal** | Code d'instruction criminelle art. 117-120 |

### `cantonnement` — 1 seul sens (ne pas confondre avec cautionnement)

Code judiciaire art. 1403-1406. Faculté du débiteur de consigner une somme pour libérer une saisie ou neutraliser les effets d'une exécution provisoire pendant un recours.

### `exécution` — distinguer

- **Exécution provisoire** (jugement frappé d'opposition / appel) → Code judiciaire art. 1397 et s.
- **Exécution forcée** (saisies, voies d'exécution) → Code judiciaire art. 1494 et s.

### `mainlevée`

- **Saisie** → Code judiciaire (chapitres saisie-exécution, saisie-arrêt).
- **Hypothèque / sûreté réelle** → Code civil Livre 9 / loi hypothécaire.

### `prescription`

- **Extinctive** (créance qui s'éteint par l'écoulement du temps) → Code civil art. 5.337+.
- **Acquisitive** (acquisition de propriété par possession prolongée) → Code civil Livre 3.

### `nullité`

- **Absolue** (intérêt général, imprescriptible, soulevable par tout intéressé) ↔ **Relative** (intérêt particulier, prescriptible, soulevable par la partie protégée).
- Cadre : Code civil art. 5.57 à 5.65.

## Règle d'or — disambiguation

Quand la question contient les indices d'une matière procédurale ("jugement", "code judiciaire", "exécutoire", "saisie", "huissier"), **le Code judiciaire prime sur le Code civil**.

Ne cite **pas** le Livre 9 "sûretés personnelles" dans une question manifestement procédurale, même si le mot "cautionnement" apparaît : il s'agit alors du cautionnement **judiciaire** ou **pénal**.

## Bonnes vs mauvaises requêtes — exemples

| ✗ Mauvaise | ✓ Bonne | Pourquoi |
|------------|---------|----------|
| `"clause domiciliation locataire"` | `"domiciliation preneur locataire bail Bruxelles interdire"` | Inclut le synonyme légal "preneur" + contexte régional |
| `"résiliation bail"` | `"congé renon bail résidence principale Bruxelles"` | Couvre "congé" et "renon" + contexte |
| `"licenciement abusif"` | `"licenciement congédiement rupture contrat travail manifestement déraisonnable"` | Couvre synonyme + qualification légale |
| `"cautionnement bail"` | `"garantie locative dépôt cautionnement caution bail"` | Évite la confusion avec cautionnement civil/judiciaire |
