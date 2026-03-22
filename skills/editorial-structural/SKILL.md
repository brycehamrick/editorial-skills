---
name: editorial-structural
description: Conceptual and structural editing of nonfiction writing — the macro-level integrity check. Use when evaluating whether the thesis holds up, whether chapters are in the right order, or where the work needs more evidence, data, or visuals. Also use when the user mentions "structural edit," "does my thesis work," "is the argument solid," "reverse outline," "are chapters in the right order," "what's missing," "gap analysis," "does the concept hold," or "check the skeleton." First stage of the editorial workflow — do before editorial-development, editorial-line, editorial-copy, or editorial-proof.
---

# Conceptual & Structural Editing

**Check for editorial context first:** If `.agents/editorial-context.md` exists, read it before beginning.

## Intake

Read the context file. Then ask for anything not already captured — do not ask about what's already there.

**Required — cannot begin without these:**
1. What is the title of the work, and what form is it? (book chapter, full manuscript, white paper, essay, report, article)
2. Who is the intended audience? Be specific — not "business readers" but "C-suite executives at mid-market companies evaluating a software purchase."
3. What does the author believe the thesis is? Ask them to state it in one sentence. (The structural edit will test whether the work actually argues it — but you need their stated intent first.)

**Required for business writing:**
4. Is the primary reader expected to skim or read closely? (Shapes how structural recommendations are framed — an executive summary audience needs the conclusion at the front; a practitioner audience may read linearly.)

**Helpful if not already captured:**
5. What stage is this — early draft, near-final, or complete manuscript?
6. What is the intended publication or delivery context? (Trade publisher, self-published, internal report, conference paper)
7. Are there specific sections the author already suspects are weak, out of order, or underdeveloped?

Record all answers in `.agents/editorial-context.md` before running the assessment. If the user can't state the thesis in one sentence, that is already the first structural finding — note it and proceed.

---

You are checking the skeleton. This phase does not touch sentences. It does not look at punctuation, word choice, or paragraph flow. Those concerns belong to later stages. Here, you are asking only: is the foundation sound?

A piece with a weak concept and a broken structure cannot be saved by good prose. Fix the skeleton first.

Act as a structural editor in the tradition of Scott Norton's *Developmental Editing* (University of Chicago Press), applying his framework for Concept, Thesis, and Content to assess macro-level integrity before any other editing begins.

---

## The Central Diagnostic Problem

The most common structural problem in nonfiction drafts is **too many concepts competing for center stage.** Norton identifies this in Chapters 1, 2, and 3 as the primary presenting symptom — not one issue among many. An author may have five compelling ideas where one would suffice. Before anything else, find the concept that should win and assess whether the structure serves it.

---

## Three-Part Structural Assessment

### Part 1: The Thesis Check

**Norton's focus:** *Concept* (Chapter 1) and *Thesis* (Chapter 3).

The thesis is the load-bearing beam. If it's weak or absent, nothing built on top of it will stand. Every structural finding flows from whether the thesis is clear, arguable, and actually proven by the content.

**What to assess:**

**Concept integrity:**
- What is this piece fundamentally about — in one sentence?
- How many distinct concepts are competing for center stage? Which one should win?
- Does the stated concept hold up across the full range of material, or does the piece keep drifting toward a competing idea?
- Is the concept substantial enough to carry the piece, or should it be a shorter form? Too large for one piece?

**Thesis strength:**
- Is the thesis explicitly stated, and if so, where? (Authors often bury it in paragraph five or seven of the introduction — or hide it in the conclusion.)
- Is it arguable? Could a reasonable person disagree?
- Is it specific? ("Leadership matters" is not a thesis. "The leaders who outperformed their peers in this study did one counterintuitive thing consistently" is.)
- Is it actually argued, or just asserted? The thesis must be demonstrated, not declared.

**The hook:**
- The thesis does double duty: it drives the internal logic *and* it becomes the marketing hook — the line in the summary, the pitch, the executive summary.
- Is the thesis sharp enough to work as a hook? Could it anchor a one-paragraph summary of the piece?
- Is there a gap between what the author thinks the thesis is and what the work actually argues?

**The working title:**
- Does the title deliver on the actual argument?
- For business writing: does the title communicate the outcome or insight, not just the subject?

**Deliverable from Part 1:** A one-sentence thesis as you read it. The author confirms or corrects it. This becomes the editorial north star for everything that follows.

---

### Part 2: Structural Mapping — The Reverse Outline

**Norton's focus:** *Content* (Chapter 2) — the content map as a diagnostic tool.

A reverse outline is built from what the piece *actually says*, not what the author intended. Read the manuscript and write one sentence per section or chapter summarizing its actual argument or content. Then lay those sentences out in sequence and read them as a standalone document.

**What the reverse outline reveals:**
- Whether chapters are in the right order
- Whether any chapter is doing the work of another
- Whether the sequence builds toward the thesis or wanders
- Whether the opening earns the conclusion

**Structural questions to answer:**
- Does the chapter sequence build logically toward the thesis, or does it wander?
- Is there a chapter that doesn't connect to the thesis? What is it doing?
- Are any two chapters covering the same ground?
- Is the conclusion sitting at the end when it should be at the front? (See business writing note below.)
- Does the opening establish stakes quickly enough for the intended reader?

**Business writing note — move the conclusion forward:**
In traditional academic structure, the conclusion comes last. In business writing — white papers, reports, proposals, executive-facing documents — readers expect the conclusion (the "so what") in the executive summary or introduction. If the piece follows academic sequencing for a business audience, flag it and recommend restructuring: lead with the finding, then build the case.

**Content map:**
In addition to the reverse outline, produce a brief content map: a one-paragraph summary of each section or chapter, noting what it argues and what it contributes to the thesis. The content map shows redundancy, gaps, and underdeveloped territory at a glance.

**Deliverable from Part 2:** The reverse outline (one sentence per section), the content map, and a chapter reorder recommendation if the sequence needs work.

---

### Part 3: Gap Analysis

**Norton's focus:** The editor's obligation to identify where the argument needs more support before recommending revision.

Gap analysis is not fact-checking. You are not verifying that claims are true — you are identifying where claims are made without sufficient support for the intended audience. The author resolves the gaps; you locate them.

**Types of gaps:**

**Evidence gaps:**
- A significant claim is made but not supported — no data, no citation, no example
- An anecdote is being used as proof rather than illustration
- Statistics are cited without source, sample size, or relevance to the specific claim
- The evidence offered is real but doesn't actually support the claim being made

**Logical gaps:**
- The argument skips a step the reader needs to follow
- The conclusion requires an assumption the piece never establishes
- Post hoc reasoning: X happened after Y, therefore Y caused X
- Hasty generalization: one or two examples presented as universal

**Visual and structural support gaps:**
- A complex comparison or trend that needs a chart or table
- A process or sequence that needs a diagram
- A case study that would demonstrate a principle better than a paragraph of assertion
- A sidebar or callout that would let the reader access supporting detail without interrupting the main argument

**Deliverable from Part 3:** A prioritized gap list — what's missing, where it appears, and what type of support would address it (data, case study, visual, additional argument).

---

## Two-Phase Process

This skill runs in two phases. Do not skip to Phase 2.

**Phase 1 — Diagnostic (always first):**
Read the work, run the full assessment, and write each discovered issue to `.agents/editorial-context.md` under a `## Structural Issues` heading. Use this format for each entry:

```
### S[#] — [Brief descriptor]
- **Location:** [Specific section, chapter, or paragraph]
- **Issue:** [What the problem is]
- **Why:** [What it costs — the reader, the argument, or the thesis]
```

Do not offer fixes. Do not suggest revisions. Do not rewrite anything. The diagnostic is complete when all issues are documented in the context file and the thesis, reverse outline, and gap list are recorded there for use by subsequent stages.

**Phase 2 — Resolution (after the user reviews):**
Present a brief summary of what was found. The user then chooses:
- **Edit manually** — They revise the manuscript, then ask whether the change satisfies the original issue. Evaluate and respond.
- **Ask Claude to revise** — Work through each issue in sequence, proposing a specific resolution. Use the `stop-slop` skill when drafting any new prose.

---

## Workflow

1. **First read — no marking.** Get the complete shape of the piece.
2. **State the thesis.** In your own words, in one sentence. If you can't, that is the first finding.
3. **Build the reverse outline.** One sentence per section or chapter: what does it actually argue?
4. **Evaluate chapter sequence.** Does the order serve the thesis? Is the conclusion in the right place?
5. **Build the content map.** One paragraph per section: what it does, what it contributes.
6. **Run the gap analysis.** Flag evidence gaps, logical gaps, and missing visual support.
7. **Write all issues to `.agents/editorial-context.md`** in the format above.
8. **Present a summary** of findings and offer the two resolution paths.

---

## What Gets Written to the Context File

Record the following in `.agents/editorial-context.md` after the diagnostic:

- **Thesis (as read):** The thesis in one sentence — confirmed or corrected by the author
- **Reverse outline:** One sentence per section, in sequence
- **Structural issues list:** All findings in the `S[#]` format above
- **What's working:** Sections where the argument is solid — anchors for the revision

Every issue must name a specific location. A finding without a location cannot be acted on.

---

## What This Stage Is Not

- It is not fixing sentences, prose, or style — those belong to later stages
- It is not checking grammar or punctuation
- It is not reorganizing paragraphs within chapters — that is developmental editing
- It is not fact-checking in a research sense — it flags where fact-checking is needed

---

## Workflow Position

This is stage 1 of 6 in the editorial workflow:
1. **editorial-structural** — Thesis, concept, reverse outline, gap analysis *(you are here)*
2. **editorial-development** — Narrative arc, voice, modular flow *(do next)*
3. **editorial-line** — Sentence-level craft, word choice, rhythm
4. **editorial-copy** — Grammar, punctuation, style guide adherence
5. **editorial-typesetting** — Markdown to print-ready LaTeX
6. **editorial-proof** — Final check of the typeset output
