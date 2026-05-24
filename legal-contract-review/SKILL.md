---
name: legal-contract-review
description: Audit d'un contrat sous droit belge — utilise quand l'utilisateur soumet un contrat (vente, services, distribution, bail, travail, NDA, SaaS, licence, partenariat) à relire avant signature ou pour évaluer le risque côté client. Détecte les clauses dangereuses, les clauses abusives B2B (CDE livre VI), les clauses manquantes critiques (force majeure, hardship 5.74, juridiction, loi applicable), les non-conformités (RGPD, droit conso, droit travail), les incohérences internes, et chiffre l'exposition financière. À combiner avec `belgian-legal-research` (sourcer les clauses), `legal-citation-rigor` (citer les articles) et `legal-quality-review` (passer ta propre review au crible).
---

# Audit de contrat — méthode

Tu reviews un contrat **pour le compte d'une des parties** — pas en arbitre neutre. Identifie d'abord pour qui tu travailles (le client est-il la partie « forte » ou « faible » du contrat ?), puis passe le texte au peigne en cherchant **ce qui peut faire mal au client**.

## Préambule — toujours demander

Avant de plonger, **identifie** :

- **Le client** : quelle partie représente-t-il (acheteur, vendeur, donneur d'ordre, prestataire, employeur, travailleur, bailleur, preneur) ?
- **Le type de contrat** : qualification juridique (vente, louage d'ouvrage, service, distribution, contrat de travail, bail, licence, NDA, partenariat) — détermine le régime applicable.
- **Le rapport B2B / B2C / B2G** : un consommateur a la protection du livre VI CDE ; une PME face à un dominant peut invoquer le régime des clauses abusives B2B (VI.91/3 et s.) ; un travailleur a la loi du 03/07/1978.
- **Le contexte international** : présence d'une partie étrangère, prestations à l'étranger, données traitées hors UE — modifie les règles de loi applicable, juridiction, RGPD.
- **L'enjeu financier** : ordre de grandeur de la transaction et de l'exposition (pour calibrer la gravité des risques).

Si une de ces infos manque, demande-la avant l'audit. La gravité d'une clause dépend du contexte.

## La grille en 8 catégories

Pour chaque clause problématique : **citation littérale** + **diagnostic** + **risque** (bloquant / sérieux / mineur) + **suggestion de réécriture**.

### 1. Clauses dangereuses pour le client

Les classiques à toujours débusquer :

- **Résolution unilatérale** sans préavis ni manquement grave — déséquilibre majeur si le client est la partie faible.
- **Clauses pénales / dommages-intérêts forfaitaires** disproportionnées (réductibles par le juge si manifestement excessives, art. 5.88 CC).
- **Clauses de non-concurrence** : durée, périmètre géographique, activités couvertes. Contre un salarié, la loi du 03/07/1978 impose des conditions strictes (durée max 12 mois, indemnité compensatoire). Contre un commerçant : raisonnabilité (durée, géographie, indemnité éventuelle).
- **Exclusion ou limitation de responsabilité** : impossible pour la faute lourde, le dol, le dommage corporel, l'obligation essentielle (jurisprudence constante). Limites de plafond très basses = clause à challenger.
- **Cession unilatérale** du contrat par l'autre partie (laisse le client subir un nouveau cocontractant choisi sans son accord).
- **Modification unilatérale** des conditions / des prix (clause "le prestataire se réserve le droit de modifier…"). Souvent abusive en B2B et toujours en B2C.
- **Tacite reconduction** longue + obligation de dénoncer dans une fenêtre étroite — vraie trappe à abonnement.
- **Solidarité** : un cocontractant solidaire pour les dettes d'un tiers ? Vérifie le périmètre.
- **Clauses pénales en cascade** (clause de résolution + clause pénale + intérêts de retard + frais de recouvrement) qui se cumulent abusivement.

### 2. Clauses abusives B2B — Code de droit économique

Depuis la loi du 04/04/2019, le CDE prohibe les clauses abusives entre entreprises (art. **VI.91/3** à **VI.91/6**, NUMAC à vérifier via `get_article`).

- **Principe (VI.91/3)** : toute clause qui crée un **déséquilibre manifeste** entre les droits et obligations des parties est abusive et réputée non écrite.
- **Liste noire (VI.91/4)** : 4 clauses **toujours** abusives — clause potestative pour le rédacteur, droit unilatéral d'interpréter le contrat, renonciation à tout recours, renonciation à toute preuve.
- **Liste grise (VI.91/5)** : 8 clauses **présumées** abusives sauf preuve contraire — modification unilatérale prix/clauses, tacite reconduction sans fenêtre raisonnable, transfert unilatéral des risques, limitation excessive de responsabilité, clauses pénales disproportionnées, etc.

Pour chaque clause suspecte, **vérifie via `get_article`** dans quelle liste elle tombe.

### 3. Clauses manquantes critiques

Une absence est parfois plus dangereuse qu'une présence. Vérifie systématiquement :

| Clause | Pourquoi |
|--------|----------|
| **Force majeure** (art. 5.226 CC nouveau) | À défaut, le régime supplétif s'applique — peut être défavorable. Mieux : définir, lister, prévoir la procédure de notification et les effets (suspension, résiliation après X jours). |
| **Hardship / Imprévision** (art. 5.74 CC nouveau) | Depuis 2023, le juge peut **réviser** un contrat en cas de changement imprévisible et grave des circonstances. Les parties peuvent y déroger ; à vérifier. |
| **Loi applicable** | Indispensable si élément international. Par défaut, Rome I (commercial) ou règles de protection (conso, travail). |
| **Juridiction compétente** | Belgique = quel tribunal ? Étranger ? Arbitrage ? Si rien : règles de droit commun (siège du défendeur). |
| **Mode de résolution amiable** préalable | Médiation, conciliation, expertise — peut être imposé par décret régional dans certaines matières. |
| **Indemnité de procédure / frais de recouvrement** | À chiffrer, surtout en B2B (loi du 02/08/2002, intérêts de retard automatiques). |
| **Indexation des prix** | Sinon, prix fixe. Définir l'indice (santé, IPC), la périodicité, le plafond. |
| **Cession et sous-traitance** | Autorisée ? Sous conditions ? Avec quelles garanties ? |
| **Confidentialité** | Durée, périmètre, sanctions, exceptions (informations publiques, ordre judiciaire). |
| **Propriété intellectuelle** | Si création/livraison de contenu : qui en est titulaire ? Droits cédés ou concédés ? Étendue (monde, durée, supports) ? Droit moral préservé ? |

### 4. Conformité légale — RGPD, droit conso, droit travail

- **RGPD** : si traitement de données personnelles, vérifier
  - finalité explicite + base légale (consentement, contrat, intérêt légitime…)
  - durées de conservation
  - droits des personnes (accès, rectification, effacement, portabilité, opposition)
  - transferts hors UE (clauses contractuelles types, décision d'adéquation)
  - sous-traitance encadrée (art. 28 RGPD : contrat écrit obligatoire)
  - DPO si requis ; analyse d'impact (AIPD) si traitement à risque.
- **B2C — Livre VI CDE** : clauses abusives B2C (art. VI.83), obligations d'information précontractuelle, droit de rétractation (vente à distance, hors établissement), garantie légale de conformité 2 ans.
- **Contrat de travail** : loi du 03/07/1978 — préavis (calculé selon ancienneté), motif grave (faute grave + procédure), période d'essai supprimée, clauses pénales sur la non-concurrence très encadrées.
- **Lutte contre le blanchiment** : si client soumis à la loi du 18/09/2017, KYC obligatoire.

### 5. Cohérence interne

- **Définitions** : chaque terme défini est-il utilisé conformément à sa définition ? Sont-elles toutes utilisées (sinon, à supprimer) ?
- **Références croisées** : "article 5.3 ci-dessus" pointe-t-il vraiment vers la bonne clause ? Un renvoi à un article inexistant signale une révision bâclée.
- **Annexes** : citées dans le corps, jointes en pratique ? Ordre de priorité défini (en cas de conflit entre annexe et corps) ?
- **Numérotation** : pas de saut, pas de doublon.
- **Langues** : si bilingue (FR/NL pour la Belgique, ou FR/EN), version qui prime en cas de conflit ?

### 6. Chiffrage du risque

Pour chaque risque sérieux identifié, **chiffre l'exposition** quand c'est possible :

- Clause pénale max : montant.
- Indemnité de fin de contrat : montant ou formule.
- Pénalités de retard : taux × période plausible.
- Exposition responsabilité : plafond contractuel vs exposition réelle si plafond inopposable.

Le client doit voir un ordre de grandeur, pas seulement une liste de "défauts".

### 7. Procédure et exécution

- **Mise en demeure** : forme imposée (recommandé avec AR, email avec preuve, courrier d'huissier) ?
- **Résolution / résiliation** : conditions formelles, délai de grâce, mise en demeure préalable, intervention judiciaire requise ?
- **Tribunal compétent** : matériel + territorial, cohérent avec la nature du contrat et des parties.
- **Exécution forcée** : clause de réserve de propriété, gage, sûretés réelles ou personnelles présentes ?

### 8. Posture commerciale

Pas juridique stricto sensu mais important pour le client :

- La balance des concessions est-elle équilibrée ? Si tout penche dans un sens, c'est exploitable en négociation.
- Y a-t-il des clauses **inhabituelles** que le client n'a pas négociées explicitement (pratique des "clauses prises dans un standard fourni par l'autre partie") ? Les signaler — l'art. 5.23 nouveau Code civil les soumet à des règles spéciales (clauses inhabituelles dans des conditions générales).

## Format du rapport

```
## Identification
- Client : ...
- Type de contrat : ...
- B2B / B2C / B2G : ...
- International : ...
- Exposition estimée : ...

## Risques bloquants (à ne pas signer en l'état)
1. **[Catégorie 2 — Clause abusive B2B]** Clause X : « ... »
   Diagnostic : tombe sous VI.91/5 (présumée abusive).
   Risque : ... €
   Réécriture proposée : ...

## Risques sérieux (à négocier)
...

## Risques mineurs (à mentionner)
...

## Clauses manquantes critiques
- Force majeure (5.226)
- Hardship (5.74)
- ...

## Conformité
- RGPD : ✅ / ⚠️ / ❌
- B2C : ...

## Recommandation
- Signer en l'état : NON / OUI sous réserves
- Négocier en priorité : [liste ordonnée]
```

## Posture

- Tu travailles **pour ton client** : pas de neutralité de façade. Signale les défauts qui le pénalisent ; mentionne les défauts dans l'autre sens **seulement** s'ils peuvent se retourner (ex : une clause pénale très haute contre le client peut être jugée disproportionnée et donc inopposable).
- **Ne réécris pas tout** : propose les réécritures uniquement sur les risques sérieux et bloquants. Le mineur, on note, on ne reformule pas.
- Si le contrat est **propre**, dis-le. Un audit qui invente des défauts coûte la crédibilité du conseil.

## Skills à combiner

- **Avant** : `belgian-legal-research` pour sourcer les clauses légales obligatoires et les régimes applicables (CDE, droit conso, RGPD, droit travail).
- **Pendant** : `legal-citation-rigor` pour citer correctement les articles (NUMAC + numéro, jamais de mémoire).
- **Après** : passe ton propre rapport à `legal-quality-review` pour vérifier que tu n'as pas inventé une référence ou une catégorie de clause abusive.
- **Si négociation à mener** : `legal-counter-argument` pour anticiper la réponse de la contrepartie aux réécritures proposées.
