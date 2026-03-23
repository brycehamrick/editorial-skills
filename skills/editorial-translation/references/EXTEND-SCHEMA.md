# EXTEND.md Schema for editorial-translation

## Format

EXTEND.md uses YAML format:

```yaml
# Default target language (ISO code or common name)
target_language: es

# Target audience (affects annotation depth and register)
audience: general  # general | technical | academic | business | or custom string

# Translation style preference
style: elegant  # storytelling | formal | technical | literal | academic | business | humorous | conversational | elegant | or custom string

# Word count threshold to trigger chunked translation
chunk_threshold: 4000

# Max words per chunk
chunk_max_words: 5000

# Custom glossary (merged with built-in glossary)
# CLI --glossary flag overrides these
# Supports inline entries and/or file paths
glossary:
  - from: "Reinforcement Learning"
    to: "Aprendizaje por refuerzo"
  - from: "Transformer"
    to: "Transformer"
    note: "Keep English"

# Load glossary from external file(s)
# Supports absolute path or relative to EXTEND.md location
# File format: markdown table with | from | to | note | columns,
# or YAML list of {from, to, note} entries
glossary_files:
  - ./my-glossary.md
  - /path/to/shared-glossary.yaml

# Language-pair specific glossaries
glossaries:
  en-es:
    - from: "AI Agent"
      to: "Agente de IA"
```

## Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `target_language` | string | `es` | Default target language code |
| `audience` | string | `general` | Target reader profile (`general` / `technical` / `academic` / `business` / custom) |
| `style` | string | `elegant` | Translation style (`storytelling` / `formal` / `technical` / `literal` / `academic` / `business` / `humorous` / `conversational` / `elegant` / custom) |
| `chunk_threshold` | number | `4000` | Word count threshold to trigger chunked translation |
| `chunk_max_words` | number | `5000` | Max words per chunk |
| `glossary` | array | `[]` | Universal glossary entries (inline) |
| `glossary_files` | array | `[]` | External glossary file paths (absolute or relative to EXTEND.md) |
| `glossaries` | object | `{}` | Language-pair specific glossary entries |

## Glossary Entry

| Field | Required | Description |
|-------|----------|-------------|
| `from` | yes | Source term |
| `to` | yes | Target translation |
| `note` | no | Usage note (e.g., "Keep English", "Only in tech context") |

## Glossary File Format

External glossary files (`glossary_files`) support two formats:

**Markdown table** (`.md`):
```markdown
| from | to | note |
|------|----|------|
| Reinforcement Learning | Aprendizaje por refuerzo | |
| Transformer | Transformer | Keep English |
```

**YAML list** (`.yaml` / `.yml`):
```yaml
- from: "Reinforcement Learning"
  to: "Aprendizaje por refuerzo"
- from: "Transformer"
  to: "Transformer"
  note: "Keep English"
```

Paths can be absolute or relative to the EXTEND.md file location.

## Priority

1. CLI `--glossary` file entries
2. EXTEND.md `glossaries[pair]` entries
3. EXTEND.md `glossary` entries (inline)
4. EXTEND.md `glossary_files` entries (in listed order, later files override earlier)
5. Built-in glossary (if any for the language pair)

Later entries override earlier ones for the same source term.

## Lookup Paths

EXTEND.md is searched in priority order:

```bash
# 1. Project-level
test -f .editorial-skills/editorial-translation/EXTEND.md && echo "project"
# 2. User-level XDG
test -f "${XDG_CONFIG_HOME:-$HOME/.config}/editorial-skills/editorial-translation/EXTEND.md" && echo "xdg"
# 3. User home
test -f "$HOME/.editorial-skills/editorial-translation/EXTEND.md" && echo "user"
```

The first path found is used. If no EXTEND.md is found, the first-time setup runs (blocking) to create one before translation begins.
