---
name: editorial-context
description: Use at the start of any editing project to create or update the shared editorial context document. Also use when the user mentions "set up the project," "capture the context," "who is the audience," "what style guide are we using," "start editing," "new project," or wants to avoid repeating foundational information across editing sessions. Creates .agents/editorial-context.md that all other editorial skills read automatically. Run this first before using editorial-structural, editorial-development, editorial-line, editorial-copy, or editorial-proof.
---

# Editorial Context

This skill establishes the shared context for an editing engagement. It creates `.agents/editorial-context.md`, which all other editorial skills read before beginning work — so you never have to repeat yourself about the audience, the style guide, the author's voice, or the project goals.

## Check for Existing Context

Before asking questions, check these sources in order:

1. **`PROJECT.md`** — If this file exists in the project root, read it first. It is the primary project context in GSD-managed projects and contains the project description, goals, audience, and scope. Treat it as authoritative and do not ask questions already answered there.
2. **`.agents/editorial-context.md`** — If this file exists, read it. Summarize what's there and ask if anything needs to be updated for the current project or session.
3. **Neither exists:** Work through the questions below to build context from scratch.

When both files exist, merge them — `PROJECT.md` is the source of truth for project-level facts; `.agents/editorial-context.md` holds editorial-specific decisions (style guide, voice notes, issue history) that accumulate during editing.

## Context-Gathering Workflow

Work through these sections conversationally. You don't need to ask every question — use judgment about what's relevant for the project type. A short essay needs less setup than a book manuscript.

### 1. The Work

- What is the title or working title?
- What type of writing is this? (nonfiction book / essay / article / white paper / report / other)
- What is the subject or central topic?
- Approximately how long is it? (word count or page count)
- What stage is it at? (outline / first draft / second draft / near-final / complete)

### 2. The Audience

- Who is the primary reader? Be specific — not "general readers" but a description of who they are, what they know, and why they'd pick this up.
- What is their knowledge level on this subject? (expert / informed general reader / general public)
- What do they want from this piece? What are they hoping to get or learn?
- Where will this be published or distributed? (trade book / academic journal / magazine / corporate internal / blog / self-published)

### 3. Voice & Tone

- How would you describe the author's voice?
- What is the formality level? (formal / semi-formal / conversational)
- What is the tone? (authoritative / accessible / polemical / analytical / narrative / instructional / other)
- Are there any voice notes — things to preserve, things to avoid?

### 4. Style Guide

- Which style guide applies? (Chicago Manual of Style / AP / APA / MLA / house style / other)
- Are there any key style decisions already made? (serial comma, number style, heading capitalization, etc.)
- Any exceptions or overrides to the standard guide?

### 5. Project Goals

- What is the purpose of this piece? What is it trying to do?
- What does success look like? How will you know it worked?
- Is there a call to action, a thesis the reader should accept, or a behavior it should change?

### 6. Editing History

- Which editing stages have already been completed, if any?
- Were there any significant decisions made in prior editing passes?
- Are there any outstanding issues or concerns from previous work?

### 7. Author Preferences

- Are there any specific concerns the author has flagged?
- Are there areas to handle with particular care?
- Are there any changes that are off-limits?

## Output

Save the completed context to `.agents/editorial-context.md` using this structure:

```markdown
# Editorial Context

## The Work
- **Title/Working title:**
- **Type:**
- **Subject:**
- **Length:**
- **Stage:**

## Audience
- **Primary reader:**
- **Knowledge level:**
- **What they want:**
- **Publication context:**

## Voice & Tone
- **Author's voice:**
- **Formality:**
- **Tone:**
- **Voice notes:**

## Style Guide
- **Guide:**
- **Key decisions:**
- **Exceptions:**

## Project Goals
- **Purpose:**
- **Success looks like:**
- **Call to action / thesis:**

## Editing History
- **Stages completed:**
- **Key decisions:**
- **Outstanding issues:**

## Author Preferences
- **Specific concerns:**
- **Areas to watch:**
- **Off-limits changes:**
```

## Updating Context

Context can be updated at any point during the editing process. When a new decision is made — a style exception adopted, a structural change agreed upon, a stage completed — update `.agents/editorial-context.md` to reflect it. All subsequent skills will pick up the updated state.

## What Comes Next

Once context is established, the editing workflow proceeds in this order:

1. **editorial-structural** — Logic, argument soundness, data accuracy
2. **editorial-development** — Big-picture structure, organization, tone
3. **editorial-line** — Sentence-level craft, word choice, rhythm
4. **editorial-copy** — Grammar, punctuation, style guide adherence
   - **editorial-translation** — Optional: translate the copy-edited document into another language *(only when translation is needed)*
5. **editorial-typesetting** — Markdown to print-ready LaTeX *(print books only — skip for essays, articles, and white papers)*
   - **latex-book** — Quality gate after typesetting; run before proceeding to proof
6. **editorial-proof** — Final check of the typeset output; formatting artifacts only

**Note on stages 5–6:** If the project is not a print book (e.g., a web article, white paper, or essay), skip `editorial-typesetting` and `latex-book` entirely. Go directly from `editorial-copy` to `editorial-proof` using the copy-edited document as the proof source.
