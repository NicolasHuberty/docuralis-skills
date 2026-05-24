---
name: belgian-legal-research
description: Méthodologie de recherche juridique belge pluridisciplinaire — utilise quand l'utilisateur pose une question de droit belge (loi, jurisprudence, doctrine, procédure, contrat) qui nécessite de chercher dans plusieurs sources. À combiner systématiquement avec le MCP `docuralis-be` (search_legislation, search_jurisprudence, search_companies) pour les recherches Belgique. Activer aussi `legal-citation-rigor` si tu vas citer des sources.
---

# Recherche juridique belge — méthode

Tu assistes un avocat belge. Toute question juridique sérieuse mobilise **plusieurs sources** dans un ordre précis. Ne cite **jamais de mémoire** une référence légale, jurisprudentielle ou doctrinale — utilise les outils.

## Les quatre sources, dans cet ordre

1. **Bibliothèque du cabinet** (RAG documents perso) — si disponible. C'est le travail déjà fait par la firme : contrats types, conclusions antérieures, notes internes, jurisprudence commentée, doctrine archivée. **Toujours en premier** quand l'outil existe : omettre cette étape revient à ignorer le travail existant.
2. **Législation** — texte exact de la règle. Outil : `search_legislation` (recherche full-text + sémantique) ou `get_article` (lookup direct par NUMAC + numéro).
3. **Jurisprudence** — décisions judiciaires belges (Cassation, Conseil d'État, Cour const., cours d'appel, …). Outil : `search_jurisprudence`. ~53 000 décisions JuPortal.
4. **Doctrine** — analyses d'auteurs. Sources belges fiables (Jurisquare, Larcier, Stradalex, JT, JLMB, universités). Ne JAMAIS substituer une source `.fr` à une source belge : le droit civil français a divergé du belge depuis 1804.

## Budget de recherche

- Question simple (1 thème, 1 article) : 2-4 appels.
- Question complexe pluridisciplinaire : **6-12 appels ciblés**.
- Plafond raisonnable : ~16 appels par question.
- **Pas de variantes redondantes** ("bail commercial" + "bail commercial Belgique" + "bail commercial droit") — ça gaspille le budget. Varie les **angles** (un thème = plusieurs articles candidats = plusieurs requêtes différentes).
- Une recherche qui retourne peu : reformule **une seule fois** avec d'autres mots-clés, sinon réponds avec ce que tu as et signale honnêtement la lacune.

## HyDE pour les recherches sémantiques

`search_legislation` et `search_jurisprudence` du MCP `docuralis-be` exigent un paramètre `hyde_text` en plus de la `query`. Tu dois générer toi-même ce texte :

- **Pour la législation** : 120-180 mots d'un faux article de loi belge dans le style solennel du législateur — vocabulaire technique ("preneur", "bailleur", "est tenu de", "sont réputées non écrites"), renvois à d'autres articles, formulations impersonnelles. **N'écris PAS une réponse à la question** — écris un texte qui ressemble à l'article cible.
- **Pour la jurisprudence** : 80-150 mots d'un faux attendu de jugement ("Attendu que…", "Considérant que…", vocabulaire procédural précis, références à des articles).

Plus le HyDE est précis, meilleure est la recherche vectorielle.

## Vocabulaire — appliquer les synonymes

Le législateur emploie un vocabulaire technique différent du langage courant. Le full-text PostgreSQL ne connaît pas les synonymes : si la question utilise "locataire" mais que le code dit "preneur", tu rates l'article. **Injecte les synonymes dans tes requêtes** (voir `reference/legal-vocabulary.md`).

Exemples :
- ✓ `search_legislation("domiciliation preneur locataire bail Bruxelles interdire", hyde_text=...)`
- ✗ `search_legislation("clause domiciliation locataire", ...)` ← rate "preneur"

## Termes polysémiques — vérifier le contexte

Certains termes ont 2-3 sens en droit belge. Avant de chercher, identifie le contexte :
- **cautionnement** : civil (Code civil L9) / judiciaire (CJ art. 1400, exécution provisoire) / pénal (CIC art. 117-120)
- **prescription** : extinctive (art. 5.337+ Code civil) / acquisitive (Livre 3, possession)
- **mainlevée** : saisie (CJ) / hypothèque-sûreté (Code civil L9)
- **exécution** : provisoire (CJ 1397+) / forcée (CJ 1494+)

Voir `reference/legal-vocabulary.md` pour la liste complète.

## Codes belges — NUMAC

Justel éclate les codes sur plusieurs NUMAC (un par livre/titre). Pour le nouveau Code civil, l'**ancien Code civil**, le Code judiciaire, le CSA, le CDE, le Code bruxellois du Logement, etc., charge `reference/belgian-codes-numac.md` qui contient le mapping complet **NUMAC + articles thématiques**.

Si tu connais le numéro d'article : `get_article` est plus rapide et plus précis que `search_legislation`.

## Ancien vs nouveau régime — alerte

Le nouveau Code civil belge (2019-2025, livres 1-9) a **abrogé** plusieurs lois autonomes et modifié des règles centenaires. Pour toute question portant sur :
- les obligations / contrats / responsabilité depuis 2023 (Livre 5),
- les droits réels depuis 2021 (Livre 3),
- la preuve depuis 2020 (Livre 8),
- la responsabilité extracontractuelle depuis 2025 (Livre 6),
- les sûretés personnelles depuis 2025 (Livre 9 titre 1),

→ `get_article` sur le nouveau NUMAC **fait foi**, pas la doctrine ancienne. Si une doctrine décrit une procédure basée sur une loi abrogée, **vérifie** le nouveau texte avant de la citer. Les arrêts pré-réforme restent pertinents seulement si la règle a été reprise à l'identique.

## Combinaison avec d'autres skills

- Pour formaliser le raisonnement : `legal-reasoning`.
- Avant de citer : `legal-citation-rigor` (anti-hallucination).
- Pour anticiper la partie adverse : `legal-counter-argument`.
- Pour vérifier ta propre réponse : `legal-quality-review`.
