# Docuralis — Skills juridiques belges pour Claude

Cinq **skills Anthropic** modulaires qui transforment Claude (Desktop, Code, claude.ai, API) en un assistant juridique belge sérieux. À utiliser **en combinaison avec le MCP server `docuralis-be`** (`https://api.docuralis.huberty.pro/mcp/`) qui fournit les outils de recherche dans la législation, la jurisprudence et la BCE.

| Skill                         | Quand l'activer                                                                            |
| ----------------------------- | ------------------------------------------------------------------------------------------ |
| `belgian-legal-research`      | Toute question juridique belge qui demande de chercher dans plusieurs sources              |
| `legal-reasoning`             | Quand tu produis un avis, une analyse, une consultation — impose le syllogisme             |
| `legal-counter-argument`      | Quand tu veux anticiper la position de la partie adverse / red team d'une thèse            |
| `legal-quality-review`        | Avant de livrer — détecte hallucinations, articles abrogés, jurisprudence morte            |
| `legal-contract-review`       | Audit d'un contrat avant signature (clauses dangereuses, B2B abusives, manquantes, RGPD)   |

Chaque skill peut être chargé seul ou combiné. Les références détaillées (NUMAC des codes belges, synonymes juridiques) sont dans des sous-fichiers chargés à la demande (progressive disclosure).

## Architecture des skills

```
skills/
├── belgian-legal-research/
│   ├── SKILL.md
│   └── reference/
│       ├── belgian-codes-numac.md      # Mapping NUMAC + articles thématiques
│       └── legal-vocabulary.md         # Synonymes + termes polysémiques
├── legal-reasoning/
│   └── SKILL.md
├── legal-counter-argument/
│   └── SKILL.md
├── legal-quality-review/
│   └── SKILL.md
└── legal-contract-review/
    └── SKILL.md
```

Le frontmatter de chaque `SKILL.md` (`name`, `description`) suit la spec Anthropic Skills. La `description` explique **quand** activer le skill — Claude la lit pour décider seul de charger ou non.

## Installation et utilisation

### Option 1 — Claude Code (CLI)

Les skills se déposent dans le dossier `.claude/skills/` du projet (ou globalement `~/.claude/skills/`).

```bash
# Skills projet (visibles seulement dans ce repo)
mkdir -p .claude/skills
cp -r /chemin/vers/docuralis_v2/skills/* .claude/skills/

# OU skills globaux (visibles dans tous les projets de cet utilisateur)
mkdir -p ~/.claude/skills
cp -r /chemin/vers/docuralis_v2/skills/* ~/.claude/skills/
```

Branche aussi le MCP `docuralis-be` dans `~/.claude.json` :

```json
{
  "mcpServers": {
    "docuralis-be": {
      "type": "streamable-http",
      "url": "https://api.docuralis.huberty.pro/mcp/",
      "headers": {
        "Authorization": "Bearer sk_docuralis_<ta_clé>"
      }
    }
  }
}
```

Au prochain lancement de `claude`, Claude Code listera les skills disponibles et appellera automatiquement le bon en fonction de ta question.

### Option 2 — Claude Desktop

1. Ouvre Claude Desktop → Settings → Skills (ou équivalent selon ta version).
2. "Add skill folder" → pointe vers le dossier `skills/` de ce repo.
3. Settings → Connectors → "Add MCP server" → URL `https://api.docuralis.huberty.pro/mcp/` + header Authorization Bearer.

### Option 3 — claude.ai (web)

1. Settings → Capabilities → Skills → Upload (formats `.zip` du dossier d'un skill, un upload par skill).
2. Settings → Connectors → "Add custom MCP server" → URL + Bearer.
3. Active les skills voulus dans le sélecteur de chat.

### Option 4 — API Anthropic / Agent SDK

Charge les skills via le paramètre `skills` (ou équivalent selon SDK). Branche le MCP via `mcp_servers` :

```python
client.messages.create(
    model="claude-sonnet-4-6",
    skills=[
        {"path": "skills/belgian-legal-research"},
        {"path": "skills/legal-reasoning"},
        {"path": "skills/legal-quality-review"},
    ],
    mcp_servers=[{
        "type": "url",
        "url": "https://api.docuralis.huberty.pro/mcp/",
        "name": "docuralis-be",
        "authorization_token": "sk_docuralis_...",
    }],
    messages=[...],
)
```

## Comment Claude utilise les skills

Anthropic Skills fonctionnent en **progressive disclosure** :

1. Au démarrage, Claude lit le frontmatter (`name` + `description`) de chaque skill.
2. Quand ta question matche la `description`, Claude charge automatiquement le `SKILL.md` complet.
3. Si le skill mentionne un fichier dans `reference/`, Claude le charge **à la demande** (par exemple : `belgian-codes-numac.md` quand il a besoin du NUMAC d'un livre du Code civil).

Pas besoin d'instructions manuelles. Tu poses ta question, les skills s'activent tout seuls.

## Combinaisons typiques

### Question de droit ("Mon client peut-il invoquer l'imprévision pour son bail commercial ?")
→ `belgian-legal-research` (cherche les sources) + `legal-reasoning` (structure l'avis) + `legal-quality-review` (vérifie avant de livrer).

### Préparation de mémoire / conclusions
→ `belgian-legal-research` + `legal-reasoning` (thèse) + `legal-counter-argument` (red team) + `legal-quality-review` (audit final).

### Audit d'un contrat envoyé par la partie adverse
→ `legal-contract-review` (principal) + `belgian-legal-research` (sourcer les clauses problématiques) + `legal-quality-review` (audit du rapport).

### Veille / question rapide ("Quel est le délai de prescription pour un loyer impayé ?")
→ `belgian-legal-research` seul suffit. Charge `reference/belgian-codes-numac.md` automatiquement.

## Pré-requis pour les outils MCP

Les skills `belgian-legal-research` et `legal-contract-review` mentionnent les outils du MCP `docuralis-be` :

- `search_legislation(query, hyde_text, limit?)` — recherche hybride dans Justel
- `get_article(numac, article_number)` — lookup exact
- `search_jurisprudence(query, hyde_text, court?, lang?, date_from?, date_to?, limit?)` — JuPortal 53k décisions
- `search_companies(query, zipcode?, nace?, ...)` — BCE/KBO 2M entités

Sans ce MCP branché, les skills restent utiles (méthode + références NUMAC en local), mais Claude ne pourra pas valider en temps réel les citations. **Branche le MCP** pour profiter pleinement.

Voir `../backend/mcp_server/README.md` pour la doc complète du serveur MCP et la gestion des clés API.

## Licence et redistribution

Ces skills sont conçus pour les abonnés du service Docuralis. Le contenu (NUMAC, mapping thématique, méthodologie) est issu de l'expertise du cabinet et de l'analyse du droit belge — il s'apprécie en combinaison avec les outils MCP.

Pour obtenir une clé API du MCP `docuralis-be` (qui débloque les outils de recherche), contacter Docuralis.
