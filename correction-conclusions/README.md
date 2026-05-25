# correction-conclusions

Skill Anthropic pour auditer et améliorer des **projets de conclusions ou d'avis en droit belge** selon la méthodologie « escalier » de Roland Huberty (Iuxta Legal).

## Quand ce skill s'active

Tout message où l'utilisateur soumet un projet de conclusions ou d'avis (`.docx`, texte) et demande une relecture, un audit méthodologique, ou des suggestions d'amélioration. Le frontmatter `description` indique à Claude de charger automatiquement ce skill dans ces cas-là.

## Ce qu'il vérifie

Sur six dimensions :

1. **Structure obligatoire** — en-tête, faits, objet des demandes, discussion, dispositif, inventaire des pièces.
2. **Chronologie des faits** — strictement croissante, paragraphes numérotés, citations littérales avec renvoi à la pièce.
3. **Méthodologie « escalier » dans la discussion** — plan annoncé, chaque chapitre = principes (général) → application (particulier) → conclusion synthétique.
4. **Citations et renvois** — italique + guillemets pour les pièces, références complètes pour la jurisprudence/doctrine, anti-répétition par « cfr supra ».
5. **Dispositif structuré** — demande principale (A) séparée des demandes reconventionnelles (B.1, B.2, …) et accessoires (C).
6. **Inventaire** — numérotation continue, correspondance bidirectionnelle avec les renvois du corps.

Cas particuliers couverts : **conclusions de synthèse (art. 748bis C. jud.)**, **pluralité de parties**, **demandes reconventionnelles multiples**.

## Inférence automatique de la posture

Au démarrage, le skill identifie pour quelle partie Roland Huberty / Iuxta Legal plaide (demandeur, défendeur, intervenant…) en cherchant le bloc « ayant pour conseil … » dans l'en-tête. La méthodologie s'adapte ensuite (construction de thèse vs déconstruction).

## Sortie

- **`{nom}_relu.docx`** : copie du projet avec **track changes** (auteur : *Docuralis — Correction conclusions*) que l'avocat ouvre dans Word et accepte/rejette en un clic.
- **Compte-rendu chat** : posture détectée, défauts bloquants / sérieux / mineurs, vérifications de sources si MCP `docuralis-be` disponible.

## Workflow en deux phases

1. **Phase 1 — audit complet** : par défaut au premier appel.
2. **Phase 2 — réécriture ciblée** : sur demande explicite (« réécris le chapitre B.2 », « restructure les faits »). Génère un second `.docx` avec les insertions complètes en track changes.

## Scripts inclus (Claude Code uniquement)

Sous `scripts/` :

- **`extract_structure.py`** — parse le `.docx`, retourne JSON (sections, numérotation, dates des faits avec vérif chronologique, références aux pièces, italiques-guillemets, inventaire, cohérence renvois ↔ inventaire).
- **`apply_track_changes.py`** — applique les modifications suggérées en track changes Word (auteur signé) à partir d'un fichier JSON d'opérations (`replace`, `delete`, `insert_after`, `insert_paragraph_after`).
- **`requirements.txt`** — dépendance `python-docx>=1.1.0`.
- **`example_operations.json`** — schéma type d'opérations.

Sur claude.ai et Claude Desktop, ces scripts ne s'exécutent pas : Claude livre alors l'audit en chat structuré et l'avocat applique manuellement les corrections dans Word.

## Référence détaillée

`reference/methodologie-detaillee.md` — checklist exhaustive en 42 points + modèles de réécriture + formulations canoniques + barème de gravité. Chargé à la demande par progressive disclosure.

## À combiner avec

- **`belgian-legal-research`** — pour trouver les sources à citer
- **`legal-reasoning`** — pour structurer la thèse
- **`legal-counter-argument`** — pour stress-tester chaque chapitre de discussion
- **`legal-quality-review`** — pour l'audit final du fond avant dépôt
