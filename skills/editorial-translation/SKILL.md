---
name: editorial-translation
description: Translation of finished nonfiction documents into a target language -- preserving intent, register, tone, and formatting. Default target language is Spanish, but works for any language pair. Use when the user asks to "translate", "translate to Spanish", "translate the manuscript", "localize", or mentions any target language. Runs after editorial-copy (stage 4), before editorial-typesetting (stage 5) -- optional step, not all documents require it. Produces a translated document in an output directory next to the source file. Supports custom glossaries for term consistency and opt-in Codex CLI execution.
---

# Translation

**Check for editorial context first:** If `.agents/editorial-context.md` exists, read it before beginning. Use the audience profile, voice and tone notes, and style guide -- only ask for what's not already there. Do not write to this file -- translation is a production step, not a diagnostic.

## Script Directory

Scripts in `scripts/` subdirectory. `{baseDir}` = this SKILL.md's directory path. Resolve `${BUN_X}` runtime: if `bun` installed -> `bun`; if `npx` available -> `npx -y bun`; else suggest installing bun. Replace `{baseDir}` and `${BUN_X}` with actual values.

| Script | Purpose |
|--------|---------|
| `scripts/main.ts` | CLI entry point for markdown chunking |

## Preferences (EXTEND.md)

Check EXTEND.md existence (priority order):

```bash
# macOS, Linux, WSL, Git Bash
test -f .editorial-skills/editorial-translation/EXTEND.md && echo "project"
test -f "${XDG_CONFIG_HOME:-$HOME/.config}/editorial-skills/editorial-translation/EXTEND.md" && echo "xdg"
test -f "$HOME/.editorial-skills/editorial-translation/EXTEND.md" && echo "user"
```

| Result | Action |
|--------|--------|
| Found | Read, parse, apply settings. On first use in session, briefly remind: "Using preferences from [path]. You can edit EXTEND.md to customize glossary, target language, style, etc." |
| Not found | **MUST** run first-time setup (see below) -- do NOT silently use defaults |

Schema: [references/EXTEND-SCHEMA.md](references/EXTEND-SCHEMA.md)

### First-Time Setup (BLOCKING)

**CRITICAL:** When EXTEND.md is not found, **MUST** run first-time setup before ANY translation. This is a **BLOCKING** operation.

Use `AskUserQuestion` with all questions in ONE call:
1. **Target language** (default: Spanish / `es`)
2. **Source language** (default: auto-detect)
3. **Audience** (default: `general` -- see [references/STYLE-PRESETS.md](references/STYLE-PRESETS.md))
4. **Style** (default: `elegant` -- see [references/STYLE-PRESETS.md](references/STYLE-PRESETS.md))
5. **Where to save EXTEND.md** (project / user home / user XDG)

After user answers: create EXTEND.md at the chosen location, confirm "Preferences saved to [path]", then continue.

## Defaults

All configurable values in one place. EXTEND.md overrides these; CLI flags override EXTEND.md.

| Setting | Default | EXTEND.md key | CLI flag | Description |
|---------|---------|---------------|----------|-------------|
| Target language | `es` | `target_language` | `--to` | Translation target language |
| Source language | auto-detect | `source_language` | `--from` | Source language (auto if omitted) |
| Audience | `general` | `audience` | `--audience` | Target reader profile |
| Style | `elegant` | `style` | `--style` | Translation style preference |
| Chunk threshold | `4000` | `chunk_threshold` | -- | Word count to trigger chunked translation |
| Chunk max words | `5000` | `chunk_max_words` | -- | Max words per chunk |

See [references/STYLE-PRESETS.md](references/STYLE-PRESETS.md) for audience and style preset descriptions.

## Usage

```
/translate [--from <lang>] [--to <lang>] [--audience <audience>] [--style <style>] [--glossary <file>] [--engine codex] <source>
```

- `<source>`: File path, URL, or inline text
- `--from`: Source language (auto-detect if omitted)
- `--to`: Target language (from EXTEND.md or default `es`)
- `--audience`: Target reader profile
- `--style`: Translation style preference
- `--glossary`: Additional glossary file to merge with EXTEND.md glossary
- `--engine codex`: Opt-in Codex CLI execution (see Codex Engine section)

## Workflow

### Step 1: Load Preferences

1. Check EXTEND.md (project -> XDG -> home)
2. If not found: run first-time setup (BLOCKING)
3. Apply settings; merge with CLI flags (CLI overrides EXTEND.md)

### Step 2: Read Context

Read `.agents/editorial-context.md` if it exists.
Load: audience profile, voice and tone notes, style guide preferences.
Do not ask for what is already there. Do not write to this file.

### Step 3: Materialize Source and Create Output Directory

| Input Type | Action |
|------------|--------|
| File | Use as-is |
| Inline text | Save to `translate/{slug}.md` |
| URL | Fetch content, save to `translate/{slug}.md` |

`{slug}`: 2-4 word kebab-case slug derived from content topic.

Output directory: `{source-dir}/{source-basename}-{target-lang}/`

If directory exists: rename to `{name}.backup-YYYYMMDD-HHMMSS/` before creating new one. Never overwrite existing results.

### Step 4: Assess Content Length

Estimate word count:
- Below chunk threshold (default 4000): translate as single unit
- At or above chunk threshold: chunked translation (Step 4.1)

### Step 4.1: Long Content Preparation (chunked only)

1. Extract terminology: scan entire document for proper nouns, technical terms, recurring phrases
2. Build session glossary: merge extracted terms + EXTEND.md glossary + `--glossary` file
3. Split into chunks:
   ```
   ${BUN_X} {baseDir}/scripts/main.ts <file> [--max-words <chunk_max_words>] [--output-dir <output-dir>]
   ```
4. Save chunks to `{output-dir}/chunks/`

### Step 5: Analyze

Analyze full source content per [references/ANALYSIS-WORKFLOW.md](references/ANALYSIS-WORKFLOW.md) Step 1 (sections 1.1-1.8):
- Quick summary, core content, background context
- Terminology extraction
- Tone and register assessment
- Reader comprehension challenges
- Figurative language and metaphor mapping
- Structural and creative challenges

Save to `{output-dir}/01-analysis.md`.

### Step 6: Assemble Translation Prompt

Read `01-analysis.md`. Inline: style preset, content background, merged glossary, comprehension challenges.
Save to `{output-dir}/02-prompt.md`.

Template in [references/ANALYSIS-WORKFLOW.md](references/ANALYSIS-WORKFLOW.md) Step 2 (Subagent Prompt Templates Part 1).

### Step 7: Translate

**If Agent tool available and content is chunked:**
- Spawn one subagent per chunk in parallel (template in [references/ANALYSIS-WORKFLOW.md](references/ANALYSIS-WORKFLOW.md) Step 2, Part 2)
- Each reads `02-prompt.md` and translates its chunk -> saves to `chunks/chunk-NN-draft.md`
- Merge all chunks in order; prepend `chunks/frontmatter.md` if it exists
- Save merged result to `translation.md`

**If not chunked or Agent tool unavailable:**
- Translate source following `02-prompt.md` -> save to `translation.md`

Invoke `stop-slop` when drafting translated prose if available -- production prose warrants a slop check.

### Step 8: Output Summary

Display after translation is complete:

```
Translation complete

Source: {source-path}
Languages: {from} -> {to}
Output dir: {output-dir}/
Final: {output-dir}/translation.md
Glossary terms applied: {count}
```

Image-language pass: collect image references from the translated document, identify text-heavy images (covers, diagrams, screenshots), and remind the user if any likely contain source-language text that has not been localized.

## Translation Principles

Apply to all translations:

- **Accuracy first**: Facts, data, and logic must match the original exactly
- **Meaning over words**: Translate what the author means, not just what the words say. When a literal translation sounds unnatural, restructure freely to express the same meaning in idiomatic target language
- **Figurative language**: Interpret metaphors, idioms, and figurative expressions by their intended meaning rather than word-for-word. Replace source-language images with target-language equivalents when the original image does not carry the same connotation
- **Emotional fidelity**: Preserve the emotional connotations of word choices, not just their dictionary meanings. Words carrying subjective feelings ("alarming", "haunting") should evoke the same response in the target language
- **Natural flow**: Use idiomatic target-language word order and sentence patterns; break or restructure sentences freely when the source structure does not work naturally in the target language
- **Terminology**: Use glossary translations consistently; annotate with original term in parentheses on first occurrence
- **Preserve format**: Keep all markdown formatting (headings, bold, italic, images, links, code blocks)
- **Frontmatter transformation**: If source has YAML frontmatter, rename origin-metadata fields with `source` prefix (`url`->`sourceUrl`, `title`->`sourceTitle`, etc.); translate values and add as new top-level fields; keep other fields as-is
- **Respect original**: Maintain original meaning and intent; do not add, remove, or editorialize -- sentence structure and imagery may be adapted freely to serve the meaning
- **Translator's notes**: For terms, concepts, or cultural references that target readers may not recognize, add a concise explanatory note in parentheses immediately after the term. Format: `[target text] ([source term] -- [brief explanation])`. Calibrate annotation depth to the target audience -- general readers need more notes than technical readers. Only annotate where genuinely needed; do not over-annotate obvious terms.

## Codex Engine (opt-in)

Triggered by `--engine codex` flag. Claude translates by default -- this is an optional execution path.

When selected, codex handles **both** the analysis pass and the translation.

**Check installation:**
```bash
codex --version 2>/dev/null
```
If non-zero exit: fall back to Claude, notify user: "Codex not available -- translating with Claude instead."

**Model:** `gpt-5.4-mini` at `medium` reasoning effort. Note: gpt-5.4-mini is the latest mini model as of this skill's creation. This overrides the codex skill's auto-selection table. Check current codex model options if this model is unavailable.

**Analysis pass (read-only sandbox):**
```bash
codex exec \
  -m gpt-5.4-mini \
  --config model_reasoning_effort="medium" \
  --sandbox read-only \
  --skip-git-repo-check \
  -- "$(cat .tmp/analysis-prompt.md)" 2>/dev/null
```

**Translation pass (workspace-write sandbox, full-auto):**
```bash
codex exec \
  -m gpt-5.4-mini \
  --config model_reasoning_effort="medium" \
  --sandbox workspace-write \
  --full-auto \
  --skip-git-repo-check \
  -- "$(cat .tmp/translate-prompt.md)" 2>/dev/null
```

Write prompts to `.tmp/analysis-prompt.md` and `.tmp/translate-prompt.md` before running. On any non-zero exit: fall back to Claude, notify user. After completion (success or failure): remove `.tmp/analysis-prompt.md` and `.tmp/translate-prompt.md`.

## Output Directory Structure

**Non-chunked translation:**
```
{source-dir}/{source-basename}-{target-lang}/
├── 01-analysis.md         # Content analysis
├── 02-prompt.md           # Assembled translation prompt
└── translation.md         # Final translated document
```

**Chunked translation:**
```
{source-dir}/{source-basename}-{target-lang}/
├── 01-analysis.md
├── 02-prompt.md
├── chunks/
│   ├── frontmatter.md     # Extracted YAML frontmatter (if any)
│   ├── chunk-01.md        # Source chunk 1
│   ├── chunk-01-draft.md  # Translated chunk 1
│   ├── chunk-02.md
│   ├── chunk-02-draft.md
│   └── ...
└── translation.md         # Final merged translation
```

**Codex path temp files (removed after run):**
```
.tmp/
├── analysis-prompt.md     # Prompt for codex analysis pass
└── translate-prompt.md    # Prompt for codex translation pass
```

## What This Stage Is Not

- Not an editorial diagnostic -- this skill does not write issue logs or `T#` entries to `.agents/editorial-context.md`. It reads the context file for audience and voice data only.
- Not a localization service for UI strings or marketing copy -- this skill is for nonfiction prose (books, essays, white papers, long-form articles)
- Not a substitute for a human translator for legally binding or safety-critical documents
- Does not modify the source document

## References

- [ANALYSIS-WORKFLOW.md](references/ANALYSIS-WORKFLOW.md) -- Detailed content analysis, translation workflow steps, and subagent prompt template
- [EXTEND-SCHEMA.md](references/EXTEND-SCHEMA.md) -- EXTEND.md preferences file schema
- [STYLE-PRESETS.md](references/STYLE-PRESETS.md) -- Audience and style preset tables

## Workflow Position

The editorial workflow has six main stages:
1. **editorial-structural** -- Logic, argument soundness, data accuracy
2. **editorial-development** -- Big-picture structure, organization, tone
3. **editorial-line** -- Sentence-level craft, word choice, rhythm
4. **editorial-copy** -- Grammar, punctuation, style guide adherence
5. **editorial-typesetting** -- Markdown to print-ready LaTeX
6. **editorial-proof** -- Final check of the typeset output

**editorial-translation is an optional step between stages 4 and 5.**
Not all documents go through translation. When it applies, run it after
`editorial-copy` is complete and before `editorial-typesetting` begins.
