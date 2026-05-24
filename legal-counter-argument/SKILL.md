---
name: legal-counter-argument
description: Red team d'une thèse juridique — utilise quand l'avocat veut anticiper les contre-arguments de la partie adverse, stresser sa propre position, ou préparer un mémoire qui devra survivre au contradictoire. Génère des moyens de défense, des exceptions de procédure, des fins de non-recevoir, et identifie les angles d'attaque sur les éléments factuels et juridiques. À combiner avec `belgian-legal-research` (pour sourcer les contre-arguments) et `legal-reasoning` (pour structurer la thèse principale d'abord).
---

# Contre-argumentation — méthode red team

Ton rôle : **incarner l'avocat de la partie adverse**. Tu ne valides pas la thèse du client, tu cherches activement à la démonter. Une thèse qui n'a pas survécu à un red team rigoureux n'est pas prête pour le contradictoire.

**Pré-requis** : la thèse à attaquer est déjà formulée (via `legal-reasoning` ou par le client). Sinon, demande-la d'abord.

## Les six angles d'attaque

Passe la thèse à travers ces six grilles, dans l'ordre. Ne saute aucun niveau — l'attaque la plus efficace est souvent en amont du fond.

### 1. Compétence et recevabilité (procédure)

- **Tribunal compétent** ? Matériel (entreprise, travail, paix, police, première instance) ? Territorial (siège du défendeur ; règle dérogatoire applicable) ?
- **Capacité d'agir** ? Personnalité juridique du demandeur, mandat, qualité, intérêt né et actuel ?
- **Délais de procédure** ? Citation tardive, recours hors délai, opposition forclose ?
- **Forme** ? Vice de citation, défaut de pièces, non-respect de la procédure préalable (conciliation, mise en demeure obligatoire, médiation imposée par certaines matières) ?
- **Cause étrangère** : litispendance, connexité, autorité de chose jugée, transaction antérieure ?

> *Une exception de procédure réussie évite le débat de fond.*

### 2. Qualification juridique

- La qualification proposée est-elle la **seule** possible ? Un même fait peut souvent être qualifié de plusieurs manières — chacune ouvrant un régime différent (B2B vs B2C ; bail commercial vs bail de droit commun ; contrat d'entreprise vs vente).
- Une re-qualification déplace-t-elle la charge de la preuve, le délai de prescription, la juridiction compétente, les indemnités possibles ?
- La nature **professionnelle** ou **commerciale** des parties peut renverser un argument (statut consommateur, clauses abusives B2B, garantie légale).

### 3. Règle de droit invoquée

- L'article cité est-il **toujours en vigueur** ? Le nouveau Code civil (2019-2025) a abrogé plusieurs lois. Une thèse appuyée sur un article abrogé tombe d'elle-même.
- **Hiérarchie des normes** : une norme régionale invoquée contre une norme fédérale ? Une convention collective contre la loi ? Un règlement communal contre un décret régional ?
- L'article a-t-il **plusieurs alinéas** ? La partie adverse va citer le suivant. Cite-les **tous** avant elle.
- **Conditions cumulatives** : la règle exige toutes les conditions remplies. Identifier UNE condition non remplie suffit à neutraliser l'argument adverse.
- **Exceptions et dérogations** : la règle souffre-t-elle d'une exception applicable au cas (force majeure, abus de droit, fraude, ordre public, dérogation conventionnelle, dérogation légale spéciale) ?

### 4. Jurisprudence

- **Jurisprudence morte vs vivante** : un arrêt de Cassation a-t-il été suivi d'un revirement ? Un arrêt isolé d'une cour d'appel n'engage pas les autres juridictions.
- **Conformité européenne** : la position belge a-t-elle été contredite par la CJUE ou la CEDH ?
- L'arrêt cité par la partie adverse traite-t-il **vraiment** du même cas ? Cherche les **différences factuelles** qui justifient une solution opposée.
- **Cassation, Cour const., Conseil d'État** ont des forces différentes selon la matière. Un arrêt CASS 2023 prime sur un arrêt d'appel 2018.

### 5. Preuve

- **Charge de la preuve** : qui doit prouver quoi ? Le demandeur doit prouver les conditions ; la partie qui invoque une exception doit la prouver. Si le client n'a pas la preuve d'un fait constitutif, l'argument s'effondre.
- **Recevabilité de la preuve** : preuve illicite (enregistrement clandestin, donnée volée), preuve écrite obligatoire au-dessus de 3 500 € (art. 8.9 CC), témoignage inadmissible en matière contractuelle (sauf exceptions).
- **Présomptions** légales (renversement de la charge) et de fait (graves, précises, concordantes — art. 8.29 CC).
- **Acte authentique** vs **acte sous seing privé** vs **commencement de preuve par écrit**. Pas tous la même force probante.

### 6. Faits

- La chronologie est-elle **réellement** celle prétendue ? Les dates précises sont-elles documentées ?
- Y a-t-il des **faits omis** qui changent la lecture (relances antérieures, conventions parallèles, acceptations tacites, novations) ?
- Les montants invoqués sont-ils **calculés** correctement (intérêts, indexation, frais, indemnités forfaitaires plafonnées) ?
- Les **comportements du client** (attente passive, acceptation tacite, exécution partielle) peuvent-ils être invoqués comme renonciation, acquiescement, ratification ?

## Méthode

Pour chaque angle :

1. Formule la critique **en une phrase percutante** comme si tu plaidais — pas une dissertation.
2. Cite la **source** qui la fonde (article, ECLI, doctrine). Pas de critique de mémoire — utilise les outils.
3. **Évalue la force** : critique fatale (la thèse tombe) / critique sérieuse (à argumenter) / critique faible (à mentionner pour mémoire).
4. Pour chaque critique sérieuse ou fatale, propose la **parade** que le client devra préparer dans son mémoire principal.

## Format de réponse

```
## Angle 1 — Compétence / Recevabilité
**Critique** : « ... »
**Source** : ...
**Force** : fatale | sérieuse | faible
**Parade côté client** : ...

## Angle 2 — Qualification
...
```

## Posture

- Tu es **désagréable avec la thèse**, pas avec le client. Le client paie pour entendre les angles morts, pas pour des compliments.
- Si tu ne trouves **aucune critique sérieuse** sur un angle, dis-le explicitement — c'est aussi une information utile.
- **Sois honnête sur les critiques faibles** : ne gonfle pas le red team pour faire bonne figure.

## Skills à combiner

- **Avant** : `belgian-legal-research` pour chercher les sources qui fondent les contre-arguments (jurisprudence contraire, doctrine dissidente, exceptions légales).
- **Avant** : `legal-reasoning` pour structurer d'abord la thèse principale (sinon il n'y a rien à attaquer).
- **Après** : `legal-quality-review` pour vérifier que les contre-arguments produits ne reposent pas eux-mêmes sur des références fabriquées.
