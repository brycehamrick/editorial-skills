# Editorial Skills for AI Agents

A collection of AI agent skills for editing nonfiction writing — books, essays, white papers, and long-form articles. Built for authors, editors, and writing teams who want AI coding agents to apply professional editorial standards at every stage of the editing process. Works with Claude Code and any agent that supports the [Agent Skills spec](https://agentskills.io).

Each skill corresponds to a distinct phase of the professional editorial workflow — from checking whether your argument holds up all the way through final proofreading after layout. Skills share a common context document so you never repeat yourself about the work, the audience, the style guide, or the author's voice.

## What are Skills?

Skills are markdown files that give AI agents specialized knowledge and workflows for specific tasks. When you add these to your project, your agent can recognize when you're working on an editorial task and apply the right frameworks and professional standards — structural logic checks, Scott Norton's developmental editing methodology, sentence-level line editing, Chicago or AP style enforcement, and proofreading protocols.

## How the Workflow Works

The editorial workflow is sequential. Each stage builds on the one before it. Don't polish sentences before the structure is right. Don't copy edit before the sentences are good. The `editorial-context` skill is the foundation — every other skill reads it first to understand the work, the audience, and the style guide before doing anything.

```
                        ┌──────────────────────────────────┐
                        │         editorial-context        │
                        │   (run first — read by all)      │
                        │  saves to .agents/editorial-     │
                        │         context.md               │
                        └─────────────┬────────────────────┘
                                      │
                                      ▼
                         ┌────────────────────────┐
                         │   editorial-structural  │
                         │  Stage 1: Logic, claims,│
                         │  argument validity,     │
                         │  data accuracy          │
                         └────────────┬────────────┘
                                      │
                                      ▼
                         ┌────────────────────────┐
                         │  editorial-development  │
                         │  Stage 2: Big picture — │
                         │  organization, sections,│
                         │  tone, audience fit     │
                         └────────────┬────────────┘
                                      │
                                      ▼
                         ┌────────────────────────┐
                         │     editorial-line      │
                         │  Stage 3: Sentence      │
                         │  craft, word choice,    │
                         │  rhythm, impact         │
                         └────────────┬────────────┘
                                      │
                                      ▼
                         ┌────────────────────────┐
                         │     editorial-copy      │
                         │  Stage 4: Grammar,      │
                         │  punctuation, style     │
                         │  guide adherence        │
                         └────────────┬────────────┘
                                      │
                          ┌───────────┴───────────┐
                          │ (optional branch)      │
                          ▼                        │
              ┌─────────────────────┐              │
              │ editorial-trans-    │              │
              │     lation          │              │
              │  Optional (4–5):    │              │
              │  translate into     │              │
              │  target language    │              │
              └──────────┬──────────┘              │
                         └──────────┬──────────────┘
                          ┌─────────┴─────────────┐
                          │                       │
                          ▼                       ▼
              ┌─────────────────────┐   ┌──────────────────┐
              │ editorial-typeset-  │   │  editorial-proof  │
              │      ting           │   │  Stage 5/6 (non- │
              │  Stage 5 (print     │   │  print): final    │
              │  books only):       │   │  layout check     │
              │  markdown → LaTeX   │   └──────────────────┘
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │     latex-book      │
              │  Quality gate:      │
              │  print audit before │
              │  proof              │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │   editorial-proof   │
              │  Stage 6 (print     │
              │  books): final      │
              │  PDF check          │
              └─────────────────────┘
```

**For print books:** all 6 stages apply — including typesetting, the latex-book quality gate, and proof.

**For essays, articles, and white papers:** stop after `editorial-copy`. Skip `editorial-typesetting` and `latex-book`. Run `editorial-proof` directly against the final formatted document.

Every skill also works standalone. You can run `/editorial-line` on a single chapter without having done a structural edit. The skills are designed for the full workflow but are independently useful.

## Available Skills

| Skill | Stage | Description |
|-------|-------|-------------|
| [editorial-context](skills/editorial-context/) | Foundation | Creates the shared context document — work type, audience, voice, style guide, goals. Run first. |
| [editorial-structural](skills/editorial-structural/) | 1 | Thesis, concept, reverse outline, gap analysis — the macro-level integrity check |
| [editorial-development](skills/editorial-development/) | 2 | Narrative arc, voice authority, modular flow — chapter-level movement and readability |
| [editorial-line](skills/editorial-line/) | 3 | Sentence-level craft, word choice, rhythm, persuasive impact |
| [editorial-copy](skills/editorial-copy/) | 4 | Grammar, punctuation, style guide adherence, consistency throughout |
| [editorial-translation](skills/editorial-translation/) | Optional (4–5) | Translation of finished nonfiction documents into any target language (default: Spanish). Optional step between copy editing and typesetting. |
| [editorial-typesetting](skills/editorial-typesetting/) | 5 *(print books only)* | Converts markdown to print-ready LaTeX using memoir/XeLaTeX — trim size, margins, fonts, drop caps, running heads |
| [latex-book](skills/latex-book/) | 5 companion | Print quality audit — font embedding, PDF/X compliance, widow penalties, compile log; quality gate before proof |
| [editorial-proof](skills/editorial-proof/) | 6 | Final check after layout — orphans, widows, typos from layout, broken links |

## Installation

### Option 1: Clone and Copy

```bash
git clone https://github.com/brycehamrick/editorial-skills.git
cp -r editorial-skills/skills/* .agents/skills/
```

### Option 2: Git Submodule

Add as a submodule for easy updates:

```bash
git submodule add https://github.com/brycehamrick/editorial-skills.git .agents/editorial-skills
```

Then reference skills from `.agents/editorial-skills/skills/`.

### Option 3: Copy Individual Skills

Copy only the skills you need:

```bash
# Copy just the skills you want
cp -r editorial-skills/skills/editorial-development .agents/skills/
cp -r editorial-skills/skills/editorial-line .agents/skills/
```

### Option 4: Fork and Customize

1. Fork this repository
2. Add your own style preferences, house style decisions, and reference files
3. Clone your fork into your projects

## Usage

### Start Every Project with Context

Run the context skill first. It asks about the work, the audience, the style guide, and the author's voice — then saves everything to `.agents/editorial-context.md`. Every other skill reads this file automatically, so you never repeat yourself across sessions.

```
/editorial-context
```

### Run the Full Workflow

**For print books:**

```
/editorial-structural    ← Does the argument hold? Is the data right?
/editorial-development   ← Is it organized well? Is the tone right?
/editorial-line          ← Is every sentence doing its job?
/editorial-copy          ← Is it grammatically correct? Style guide compliant?
/editorial-translation   ← (optional: translate into target language)
/editorial-typesetting   ← Convert markdown to print-ready LaTeX
/latex-book              ← Quality audit before proof (font embedding, PDF/X, widows)
/editorial-proof         ← Final check of the typeset PDF
```

**For essays, articles, and white papers:**

```
/editorial-structural    ← Does the argument hold? Is the data right?
/editorial-development   ← Is it organized well? Is the tone right?
/editorial-line          ← Is every sentence doing its job?
/editorial-copy          ← Is it grammatically correct? Style guide compliant?
/editorial-translation   ← (optional: translate into target language)
/editorial-proof         ← Final check before publishing
```

### Or Jump to What You Need

The skills work standalone. Invoke only what's relevant:

```
"Does this argument hold up?"
→ Uses editorial-structural

"Move these sections around and cut the fluff"
→ Uses editorial-development

"Make this chapter more punchy"
→ Uses editorial-line

"Check this against Chicago style"
→ Uses editorial-copy

"Translate this into Spanish"
→ Uses editorial-translation

"Convert this to LaTeX for printing"
→ Uses editorial-typesetting

"Check my LaTeX file before I submit to KDP"
→ Uses latex-book

"Final proofread before we go to print"
→ Uses editorial-proof
```

### Example Workflow

```
You: Set up a new editing project — it's a business book on leadership,
     aimed at C-suite readers, Chicago style.

→ /editorial-context creates .agents/editorial-context.md

You: Check if the argument in Chapter 3 actually supports the thesis.
→ /editorial-structural reads the context, assesses Chapter 3's logic

You: Restructure Chapter 4 — the examples come before the point they're
     supposed to illustrate.
→ /editorial-development reads the context, reorganizes Chapter 4

You: Tighten the prose in the opening section.
→ /editorial-line reads the context, edits at sentence level

You: Run a Chicago style pass on the full manuscript.
→ /editorial-copy reads the context, applies Chicago rules throughout

You: Translate the manuscript into Spanish for the Latin American edition.
→ /editorial-translation reads the context, translates the full document

You: Convert the manuscript to print-ready LaTeX for KDP.
→ /editorial-typesetting generates the full memoir/XeLaTeX project

You: Check the generated LaTeX before we go to proof.
→ /latex-book audits for font embedding, PDF/X, widows, compile log

You: Final check before the PDF goes to the printer.
→ /editorial-proof catches layout artifacts only — no content changes
```

## Skill Reference

### editorial-context

The foundation. Creates `.agents/editorial-context.md`, which captures:

- **The work** — type, subject, length, draft stage
- **Audience** — who they are, knowledge level, what they want, publication context
- **Voice & tone** — author's voice, formality, register, tone notes
- **Style guide** — Chicago, AP, APA, house style, exceptions
- **Project goals** — purpose, success criteria, call to action
- **Editing history** — stages completed, decisions made, outstanding issues
- **Author preferences** — specific concerns, off-limits changes

Run `/editorial-context` at the start of each project. Update it as decisions are made.

---

### editorial-structural — Stage 1

Checks the skeleton before anything else. Built on Scott Norton's framework for Concept, Thesis, and Content — the macro-level integrity check.

**Covers:**
- Thesis — is there one clear, arguable thesis? Is it stated? Is it actually argued, or just asserted?
- Concept — is one central idea in command, or are competing concepts fighting for center stage?
- Reverse outline — what does the piece actually argue, section by section? Are chapters in the right order?
- Content map — what each section does and what it contributes to the thesis
- Gap analysis — evidence gaps, logical gaps, missing visual or structural support

**Deliverable:** A structural report: the thesis as the editor reads it, concept assessment, reverse outline with any reorder recommendation, content map, prioritized gap list, and what's working.

**Do this before:** Everything else.

---

### editorial-development — Stage 2

The chapter-level flow pass. Built on Scott Norton's framework for Pacing, Transitions, and Vignettes. The skeleton is locked — now assess how the reader moves through the material.

**Covers:**
- Narrative arc — does the piece move the reader from Problem to Solution to Action? Is the arc intact or broken?
- Voice and authority — Norton's Level of Address: does the writing sound like an expert in command of the subject, calibrated correctly to the intended reader?
- Modular flow — do sub-headers match their content? Does the skim-path hold together for business readers? Where are the pacing mismatches and transition gaps?

**Deliverable:** An editorial report covering arc assessment, voice authority calibration, skim-path evaluation, pacing notes by section, and prioritized transition gaps.

**Do this after:** Structural. **Before:** Line editing.

---

### editorial-line — Stage 3

The artistic pass. Structure and argument are established — now make every sentence earn its place.

**Covers:**
- Word choice — precision, register, active vs. passive, eliminating vague and inflated language
- Sentence structure — variety, rhythm, emphasis, weak openings, buried subjects
- Impact — are the most important ideas in the most emphatic positions?
- Persuasive force — does this sentence make the reader believe something?
- Redundancy — throat-clearing, padding, summary that doesn't advance

**Deliverable:** Marked-up text with revised sentences, annotations on significant changes, alternative versions where a real choice exists, and a summary of dominant patterns addressed.

**Do this after:** Developmental editing. **Before:** Copy editing.

---

### editorial-copy — Stage 4

The technical pass. Correctness and consistency by the rules of the applicable style guide.

**Covers:**
- Grammar — subject-verb agreement, modifier placement, parallelism, fragments, run-ons
- Punctuation — commas, semicolons, colons, em/en dashes, apostrophes, quotation marks
- Capitalization — proper nouns, job titles, heading style, terms of art
- Numbers — when to spell out, percentages, dates, measurements (per style guide)
- Consistency — a style sheet of every decision made, ensuring uniform treatment throughout
- Citations and references — consistent format throughout
- Cross-references — internal references verified

**Deliverable:** Tracked changes in the document, a style sheet of decisions made, a brief note on recurring patterns, and flags for the author to resolve.

**Do this after:** Line editing. **Before:** Proofreading (or translation, if the document is being translated).

---

### editorial-translation — Optional step between stages 4 and 5

Translates a finished, copy-edited nonfiction document into a target language while preserving the author's intent, voice, and readability. This is a production step — it delivers a translated document, not an issue list.

**Covers:**
- Content analysis — terminology extraction, tone assessment, figurative language mapping, structural challenges — before translation begins
- Translation — full document or chunked for long documents (threshold: 4,000 words per chunk)
- Quality check — non-Europeanization check, register consistency, idiomatic accuracy
- Output — translated markdown file in a dated output directory

**Default target language:** Spanish (`es`). Works for any language pair.

**Codex opt-in:** By default, Claude performs the translation. If the `codex` skill is installed, you can opt in to using OpenAI's API for the translation pass instead.

**Reference files:**
- `ANALYSIS-WORKFLOW.md` — Eight content analysis sub-steps and full prompt templates for both analysis and translation
- `EXTEND-SCHEMA.md` — Schema for the optional `EXTEND.md` preferences file (target language, style, glossary, chunk settings)
- `STYLE-PRESETS.md` — Audience presets (general / technical / academic / business) and style presets (nine options; `elegant` is default for nonfiction)

**Do this after:** Copy editing. **Before:** Typesetting (or directly to proof, for non-print documents). Only when translation is needed.

---

### editorial-typesetting — Stage 5 *(print books only)*

Converts copy-edited markdown into a complete, print-ready LaTeX project using the memoir document class and XeLaTeX. This is not a template — it generates a full, customized preamble and source files from scratch, based on 29 intake questions covering every design decision that gets baked into the layout.

**Covers:**
- Page geometry — trim size, stock size, bleed, gutter (binding-type lookup table), margins, safe zone
- Typography — font selection and fontspec configuration (including fake bold/italic detection), microtype, drop caps
- Chapter and section styling — chapter title style, section break style, drop caps, heading hierarchy
- Running heads and page numbers — verso/recto content, case, position, suppression rules
- Front matter — half-title, title page, copyright page, dedication, epigraph, TOC
- Full markdown-to-LaTeX conversion — inline formatting, special characters, block elements, figures, tables, footnotes
- Core preamble — pdfx (PDF/X compliance, loaded before hyperref), widow/orphan/hyphenation penalties, `\raggedbottom`, `\aliaspagestyle` calls, babel, csquotes

**Deliverable:** A complete LaTeX project directory (`main.tex`, `preamble.tex`, `frontmatter/`, `chapters/`, `backmatter/`) ready to compile with `xelatex main.tex && xelatex main.tex`. Also populates the Typesetting Decision Record in `.agents/editorial-context.md`.

**Do this after:** Copy editing. **Before:** latex-book quality gate, then editorial-proof.

---

### latex-book — Stage 5 companion *(print books only)*

The quality gate between typesetting and proof. Audits the generated `.tex` files and compiled PDF against print production requirements. Does not generate LaTeX — it reads what `editorial-typesetting` produced and finds everything that would cause a print rejection or a visible error in the finished book.

**Covers:**
- memoir class correctness — `\checkandfixthelayout` placement, page style aliases, `\frontmatter`/`\mainmatter`/`\backmatter` sequence, `openright` and blank pages, `\raggedbottom` vs. `\flushbottom`
- XeLaTeX/fontspec correctness — fake bold/italic detection, ligature settings, microtype options, `csquotes` for quotation marks
- Typography quality — widow/orphan penalties, consecutive hyphenation, overfull `\hbox` warnings, underfull `\vbox`
- Print-ready PDF requirements — font embedding (`pdffonts` verification), PDF/X compliance, color mode, crop marks, image resolution
- Compile log — every error and print-relevant warning categorized

**Deliverable:** A TX#-prefixed issue list in `.agents/editorial-context.md`, each entry including the specific fix. After all TX# issues are resolved, runs the PRINT-PREFLIGHT.md checklist before declaring the file print-ready.

**Do this after:** editorial-typesetting compiles cleanly. **Before:** editorial-proof.

---

### editorial-proof — Stage 6

The final check. Only runs after the text is in its final laid-out format. This is not editing — it is quality control on the production.

**Covers:**
- Typos introduced during layout — dropped words, character conversion errors, spacing artifacts
- Orphans and widows — short lines stranded at the top or bottom of a page
- Word breaks — incorrect or misleading automatic hyphenation at line ends
- Broken links — all hyperlinks verified live (for digital documents)
- Page numbers and navigation — sequential, consistent, matching the table of contents
- Headings — all present, correct level, no stranded headings at page bottoms
- Images and captions — all present, captions match, figure numbers sequential
- Footnotes and endnotes — present, numbered correctly, on the right page

**Deliverable:** A marked-up proof, a list of flags for author decision, a brief summary of error categories.

**For print books — do this after:** `latex-book` clears all TX# issues. **For other formats — do this after:** Copy editing and final layout. This is the last step.

## The Shared Context Pattern

All skills follow the same pattern on startup:

```
Check for .agents/editorial-context.md
  → If found: read it, use what's there, only ask for what's missing
  → If not found: suggest running /editorial-context first, or ask the key questions inline
```

This means you can work across multiple sessions on the same project without losing context. Update `.agents/editorial-context.md` as decisions are made — when a style exception is adopted, when a stage is completed, when the author makes a structural choice. Every subsequent skill picks up the current state.

## Works Well With

- **stop-slop** — Catches AI writing patterns in any prose drafted during editing. Automatically invoked during `editorial-line` when drafting model rewrites.
- **latex-book** — Included in this repository as a companion to `editorial-typesetting`. Run it after every typesetting generation before moving to proof.

## What These Skills Are For

These skills are built for **nonfiction writing** — books, essays, white papers, articles, reports, and similar long-form work where argument, evidence, and author voice matter.

They are not designed for:
- Fiction (developmental editing for fiction involves different considerations)
- Marketing copy (see [marketingskills](https://github.com/coreyhaines31/marketingskills) for that)
- Academic papers with field-specific conventions that diverge significantly from trade editing practice

## Contributing

Found a way to improve a skill? Have a reference file to add — a style guide summary, a genre-specific checklist, a structural template? PRs welcome.

## License

[MIT](LICENSE) — use these however you want.
