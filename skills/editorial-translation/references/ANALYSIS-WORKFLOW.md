# Analysis Workflow and Translation Prompt Templates

This file provides detailed guidelines for each translation workflow step and the subagent prompt templates used to assemble consistent translations across chunks.

All intermediate results are saved as files in the output directory.

## Step 1: Content Analysis

Before translating, deeply analyze the source material. Save analysis to `01-analysis.md` in the output directory. Focus on dimensions that directly inform translation quality.

### 1.1 Quick Summary

3-5 sentences capturing:
- What is this content about?
- What is the core argument?
- What is the most valuable point?

### 1.2 Core Content

- **Core argument**: One sentence summary
- **Key concepts**: What key concepts does the author use? How are they defined?
- **Structure**: How is the argument developed? How do sections connect?
- **Evidence**: What specific examples, data, or authoritative citations are used?

### 1.3 Background Context

- **Author**: Who is the author? What is their background and stance?
- **Writing context**: What phenomenon, trend, or debate is this responding to?
- **Purpose**: What problem is the author trying to solve? Who are they trying to influence?
- **Implicit assumptions**: What unstated premises underlie the argument?

### 1.4 Terminology Extraction

- List all technical terms, proper nouns, brand names, acronyms
- Cross-reference with loaded glossaries
- For terms not in glossary, research standard translations
- Record decisions in a working terminology table

### 1.5 Tone & Style

- Is the original formal or conversational?
- Does it use humor, metaphor, or cultural references?
- What register is appropriate for the translation given the target audience?

### 1.6 Reader Comprehension Challenges

Identify points where target readers may struggle, calibrated to the target audience:

- **Domain jargon**: Technical terms that lack widely-known translations or are meaningless when translated literally
- **Cultural references**: Idioms, historical events, pop culture, social norms specific to the source culture
- **Implicit knowledge**: Background context the original author assumes but target readers may lack
- **Wordplay & metaphors**: Figurative language that doesn't carry over across languages
- **Named concepts**: Theories, effects, or phenomena with coined names (e.g., "comb-over effect", "Dunning-Kruger effect")
- **Cognitive gaps**: Counterintuitive claims or expectations vs. reality that need framing for target readers

For each identified challenge, note:
1. The original term/passage
2. Why it may confuse target readers
3. A concise plain-language explanation to use as a translator's note

### 1.7 Figurative Language & Metaphor Mapping

Identify all metaphors, similes, idioms, and figurative expressions in the source. For each:

1. **Original expression**: The exact phrase
2. **Intended meaning**: What the author is actually communicating (the idea behind the image)
3. **Literal translation risk**: Would a word-for-word translation sound unnatural, lose the connotation, or confuse target readers?
4. **Target-language approach**: One of:
   - **Interpret**: Discard the source image entirely, express the intended meaning directly in natural target language
   - **Substitute**: Replace with a target-language idiom or image that conveys the same idea and emotional effect
   - **Retain**: Keep the original image if it works equally well in the target language

Also flag:
- **Emotional connotations carried by word choice**: Words like "alarming" that convey subjective feeling, not just objective description — note the emotional effect to preserve
- **Implied meanings**: Sentences where the surface meaning is simple but the implication is richer — note what the author really means so the translator can convey the full intent

### 1.8 Structural & Creative Challenges

- Complex sentence patterns (long subordinate clauses, nested modifiers, participial phrases) that need restructuring for natural target-language flow
- Structural challenges (wordplay, ambiguity, puns that don't translate)
- Content where the author's voice or humor requires creative adaptation

**Save `01-analysis.md`** with:
```
## Quick Summary
[3-5 sentences]

## Core Content
Core argument: [one sentence]
Key concepts: [list]
Structure: [outline]

## Background Context
Author: [who, background, stance]
Writing context: [what this responds to]
Purpose: [goal and target audience]
Implicit assumptions: [unstated premises]

## Terminology
[term → translation, ...]

## Tone & Style
[assessment]

## Comprehension Challenges
- [term/passage] → [why confusing] → [proposed note]
- ...

## Figurative Language & Metaphor Mapping
- [original expression] → [intended meaning] → [approach: interpret/substitute/retain] → [suggested rendering]
- ...

## Structural & Creative Challenges
[sentence restructuring needs, wordplay, creative adaptation needs]
```

## Step 2: Assemble Translation Prompt

Main agent reads `01-analysis.md` and assembles a complete translation prompt using the Part 1 template below. Inline the resolved style preset (from `--style` flag, EXTEND.md `style` setting, or default `elegant`), content background, merged glossary, and comprehension challenges into the prompt. Save to `02-prompt.md`.

This prompt is used by the subagent (chunked) or by the main agent itself (non-chunked).

## Step 3: Translate

Save to `translation.md` in the output directory.

For chunked content, subagents each produce their chunk draft (saved to `chunks/chunk-NN-draft.md`); the main agent merges them. For non-chunked content, the main agent translates directly.

Translate the full content following `02-prompt.md`. Apply all translation principles, plus:

- Use the terminology decisions from Step 1 consistently
- Match the identified tone and register
- Follow the metaphor mapping from Step 1 for figurative language handling
- Add translator's notes for comprehension challenges identified in Step 1

## Step 4: Critical Review

The main agent critically reviews the translation against the source. Save review findings to `04-critique.md` (if the user requests a review pass). This step produces **diagnosis only** — no rewriting yet.

### 4.1 Accuracy & Completeness

- Compare each paragraph against the original, sentence by sentence
- Verify all facts, numbers, dates, and proper nouns
- Flag any content accidentally added, removed, or altered
- Check that technical terms match glossary consistently throughout
- Verify no paragraphs or sections were skipped

### Non-Europeanization Check (for any target language)

Flag translations that carry the structural fingerprint of English rather than natural target-language expression:

- **Unnatural calques**: Phrases translated word-for-word that produce unnatural constructions in the target language
- **Literal idiom translation**: English idioms rendered literally rather than substituted with a target-language equivalent
- **Awkward subordination**: English-style stacked subordinate clauses that should be broken into shorter sentences in the target language
- **Over-formalization**: Translating informal English prose into register-shifted formal target language (common in English to Spanish where there are multiple register options)
- **Register inconsistency**: Mixing formal and informal register (tu vs. usted in Spanish) within a single document

### 4.3 Figurative Language & Emotional Fidelity

- Cross-check against the metaphor mapping in `01-analysis.md`: were all flagged metaphors/idioms handled per the recommended approach (interpret/substitute/retain)?
- Flag any metaphors or figurative expressions that were translated literally and sound unnatural or lose the intended meaning in the target language
- Check emotional connotations: do words that carry subjective feelings in the source (e.g., "alarming", "haunting", "striking") evoke the same response in the translation, or were they flattened into neutral/objective descriptions?
- Flag implied meanings that were lost: sentences where the author's deeper intent was not conveyed because the translator stayed too close to the surface meaning

### 4.4 Strategy Execution

- Were the translation strategies from `02-prompt.md` actually followed?
- Did the translator apply the tone and register identified in analysis?
- Were comprehension challenges from `01-analysis.md` addressed with appropriate notes?
- Were glossary terms used consistently?

### 4.5 Expression & Logic

- Flag sentences that read like "translationese" — unnatural word order, calques, stiff phrasing
- Check logical flow between sentences and paragraphs
- Identify where sentence restructuring would improve readability
- Note where the target language idiom was missed

### 4.6 Translator's Notes Quality

- Are notes accurate, concise, and genuinely helpful?
- Identify missed comprehension challenges that need notes
- Flag over-annotations on terms obvious to the target audience
- Check that cultural references are explained where needed

### 4.7 Cultural Adaptation

- Do metaphors and idioms work in the target language?
- Are any references potentially confusing or offensive in the target culture?
- Could any passage be misinterpreted due to cultural context differences?

---

## Subagent Prompt Templates

### Part 1: `02-prompt.md` (shared context, saved as file)

```markdown
You are a professional translator. Your task is to translate markdown content from {source_lang} to {target_lang}.

## Target Audience

{audience description}

## Translation Style

{style description — e.g., "elegant: literary, polished prose; aesthetically refined, rhythmic, carefully crafted word choices" or custom style from user}

Apply this style consistently: it determines the voice, tone, and sentence-level choices throughout the translation. Style is independent of audience — a technical audience can still get an elegant-style translation, or a general audience can get a formal one.

## Content Background

{Inlined from 01-analysis.md: quick summary, core argument, author background, writing context, tone assessment, figurative language & metaphor mapping.}

## Glossary

Apply these term translations consistently throughout. First occurrence of each term: include the original in parentheses after the translation.

{Merged glossary — combine built-in glossary + EXTEND.md glossary + terms extracted in analysis. One per line: source term → translation}

## Comprehension Challenges

The following terms or references may confuse target readers. Add translator's notes in parentheses where they appear: `[target text] ([source term] -- [brief explanation])`

{Inlined from 01-analysis.md comprehension challenges section. Each entry: term → explanation to use as note.}

## Translation Principles

- **Accuracy first**: Facts, data, and logic must match the original exactly
- **Meaning over words**: Translate what the author means, not just what the words say. When a literal translation sounds unnatural or fails to convey the intended effect, restructure freely to express the same meaning in idiomatic {target_lang}
- **Figurative language**: Interpret metaphors, idioms, and figurative expressions by their intended meaning. When a source-language image does not carry the same connotation in {target_lang}, replace it with a natural expression that conveys the same idea and emotional effect. Refer to the Figurative Language section in Content Background (if provided) for pre-analyzed metaphor mappings
- **Emotional fidelity**: Preserve the emotional connotations of word choices, not just their dictionary meanings
- **Natural flow**: Use idiomatic {target_lang} word order and sentence patterns; break or restructure sentences freely when the source structure doesn't work naturally
- **Terminology**: Use glossary translations consistently; annotate with original term in parentheses on first occurrence
- **Preserve format**: Keep all markdown formatting (headings, bold, italic, images, links, code blocks)
- **Respect original**: Maintain original meaning and intent; do not add, remove, or editorialize — but sentence structure and imagery may be adapted freely to serve the meaning
- **Translator's notes**: For terms or cultural references listed in Comprehension Challenges above, add a concise explanatory note in parentheses immediately after the term. Format: `[target text] ([source term] -- [brief explanation])`. Calibrate annotation depth to the target audience: general readers need more notes than technical readers. Only add notes where genuinely needed; do not over-annotate obvious terms.
```

---

### Part 2: Subagent spawn prompt (passed as Agent tool prompt)

#### Chunked mode (one subagent per chunk, all spawned in parallel)

```
Read the translation instructions from: {output_dir}/02-prompt.md

Translate this chunk:
1. Read `{output_dir}/chunks/chunk-{NN}.md`
2. Translate following the instructions in 02-prompt.md
3. Save translation to `{output_dir}/chunks/chunk-{NN}-draft.md`
```

#### Non-chunked mode

```
Read the translation instructions from: {output_dir}/02-prompt.md

Translate the source file and save the result:
1. Read `{source_file_path}`
2. Translate following the instructions in 02-prompt.md
3. Save translation to `{output_path}`
```

---

## Subagent Responsibility

Each subagent (one per chunk) is responsible **only** for producing the translation of its chunk. The main agent assembles the shared prompt (Step 2), spawns all subagents in parallel, then merges results and verifies the final output.

## Chunked Translation Flow

When content exceeds the chunk threshold (see Defaults in SKILL.md):

1. Main agent runs analysis (Step 1) on the **entire** document first → `01-analysis.md`
2. Main agent assembles translation prompt → `02-prompt.md`
3. Split into chunks → `chunks/`
4. Spawn one subagent per chunk in parallel (each reads `02-prompt.md` for shared context) → merge all results into `translation.md`
5. Final cross-chunk consistency check:
   - Check terminology consistency across chunk boundaries
   - Verify narrative flow between chunks
   - Fix any transition issues at chunk boundaries
