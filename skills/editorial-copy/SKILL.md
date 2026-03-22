---
name: editorial-copy
description: Copy editing of nonfiction writing — grammar, punctuation, style guide adherence, and internal consistency using Amy Einsohn & Marilyn Schwartz's The Copyeditor's Handbook framework. Use when performing a mechanical audit of the text, building a style sheet, checking the 4 Cs (Clarity, Coherency, Consistency, Correctness), or verifying cross-references, citations, and heading hierarchy. Also use when the user mentions "copy edit," "grammar check," "style guide," "AP style," "Chicago style," "punctuation," "consistency check," "citations," "headers," "style sheet," or "is this grammatically correct." Fourth stage of the editorial workflow — after editorial-line, before editorial-typesetting.
---

# Copy Editing

**Check for editorial context first:** If `.agents/editorial-context.md` exists, read it before beginning. If a Style Sheet already exists there, load it — do not start a new one from scratch.

## Intake

Read the context file. Then ask for anything not already captured. A copy edit cannot begin without a governing style guide — all consistency decisions depend on it.

**Required — cannot begin without these:**
1. Which style guide governs this work? (Chicago Manual of Style, AP Stylebook, house style, or a hybrid. If hybrid: which guide takes precedence, and where does house style override it?)
2. American or British spelling?

**Required before initializing the Style Sheet:**
3. Are there any known house style rules to establish before starting? (Number treatment, capitalization of specific recurring terms, preferred citation format, any terminology the organization has already locked in.) Even "none that I know of" is a useful answer — record it.
4. Has a Style Sheet been started for this project from a previous session? If yes, load it. If no, it will be created from the template during Pass 1.

**Helpful if not already captured:**
5. Has this document been through prior editorial stages (structural, developmental, line)? If copy editing is being applied to a first or second draft, flag it — the pass will be less efficient, and stylistic issues outside the copy editor's scope will be harder to ignore.
6. Are there specific consistency problems the author or a prior reader already noticed? (Known issues can seed the Style Sheet before the pass begins.)
7. Does this document include citations or a bibliography? If so, what citation format is expected?

Record all answers in `.agents/editorial-context.md` and initialize the Style Sheet before running the audit.

---

Copy editing is the mechanical audit. The argument is sound (editorial-structural), the reader's path is clear (editorial-development), and the sentences are crafted (editorial-line). Now you ensure the text is correct and consistent by the rules of the applicable style guide.

Act as a copy editor trained in Amy Einsohn and Marilyn Schwartz's *The Copyeditor's Handbook* (University of Chicago Press). The copy editor's invisible hand: when done well, readers notice nothing. When done badly, readers notice everything.

Copy editing is not about making the writing better. It is about making it right.

---

## The Style Sheet: The Copy Editor's Primary Tool

Before running any audit, create a Style Sheet. The Style Sheet is a live document maintained throughout the pass — it records every consistency decision made so that the same decision is made the same way throughout the text, and so that later stages (proofreading) and future editors have a record.

The Style Sheet lives in `.agents/editorial-context.md` under a `## Style Sheet` heading. Use the template in [references/STYLE-SHEET-TEMPLATE.md](references/STYLE-SHEET-TEMPLATE.md).

**What goes on the Style Sheet:**
- The governing style guide (Chicago, AP, house style, or hybrid)
- Every proper noun and its verified spelling
- Every hyphenation decision (decision-maker vs. decision maker)
- Every capitalization decision for recurring terms
- Every number treatment decision (spell out vs. numeral, percentage format)
- Every abbreviation and its first-use expansion
- Any deviation from the standard guide with the reason
- House style overrides

**The rule:** If you make a decision once, it goes on the Style Sheet. If you find a deviation from a prior decision, it is a C# issue.

---

## The 4 Cs Framework (Einsohn's Method)

Every issue found during the copy edit maps to one of four categories. The Cs are not sequential passes — they are a classification system for what you find and why it matters.

### C1: Correctness

Fixing objective errors — things that are demonstrably wrong by the rules of grammar, spelling, and punctuation.

**Grammar:**
- Subject-verb agreement
- Pronoun-antecedent agreement
- Tense consistency within a passage (unintentional shifts)
- Faulty parallelism in lists, series, and coordinate structures
- Dangling and misplaced modifiers
- Sentence fragments (flag as intentional or unintentional; fix only if unintentional)
- Run-on sentences and comma splices

**Spelling:**
- Consistent American or British spelling throughout (not mixed)
- Commonly confused words: affect/effect, complement/compliment, its/it's, principal/principle, who/whom, lay/lie
- Technical terms spelled correctly and consistently
- Proper nouns verified against authoritative sources

**Punctuation (per the applicable style guide):**
- Serial/Oxford comma: Chicago requires it; AP generally does not — apply per guide, consistently
- Em dash, en dash, and hyphen: three distinct marks with distinct uses. Em dash (—) for parenthetical breaks. En dash (–) for ranges (pages 12–15) and compound modifiers with an open element. Hyphen (-) for standard compound modifiers.
- Quotation marks: punctuation placement inside or outside per guide (American English: inside; British: logically)
- Apostrophes: possession (the editor's handbook), contractions (it's = it is), not plurals
- Colons and semicolons: correct grammatical use; consistent spacing

---

### C2: Consistency

Ensuring that every choice made once is made the same way throughout. This is the Style Sheet in action.

**Hyphenation:**
The most frequent consistency failure in nonfiction. "Decision-maker" on page 2 and "decision maker" on page 47 is an error. "Well-known" before a noun, "well known" predicatively — mark the distinction and apply it consistently.

**Capitalization:**
- Proper nouns: consistently capitalized everywhere they appear
- Job titles: capitalized when used as a title before a name (President Lincoln), lowercased when used descriptively (the president)
- Recurring terms of art: if capitalized once, capitalized always (or not at all — but choose)
- Headers: title case or sentence case — consistent throughout, per guide or house style

**Numbers:**
- When to spell out vs. use numerals: Chicago spells out one through one hundred; AP spells out one through nine. Apply per guide throughout.
- Percentages: "50 percent" vs. "50%" — choose one and hold it
- Dates: month-day-year, day-month-year, or ISO format — per guide or house style
- Large numbers: "$4 million" vs. "$4,000,000" — choose and hold
- Units: "10 km" vs. "10 kilometers" — choose and hold

**Lists and bullets:**
- Punctuation: periods, semicolons, or none — consistent across all lists
- Capitalization of first word: consistent across all lists
- Grammar: parallel structure throughout (all noun phrases, or all imperative sentences, not mixed)

**Citations and references:**
- Consistent format for all source types (books, articles, websites, interviews)
- Footnotes vs. endnotes: consistent throughout
- Abbreviations within citations: ibid., op. cit., or full citation — per guide

**Abbreviations:**
- Every abbreviation introduced at first use with the full form spelled out: "the Federal Reserve (Fed)"
- Consistent thereafter — never the full form after the abbreviation has been introduced without explanation

---

### C3: Clarity

Removing constructions that make the reader stop or misread — not stylistic improvements, but genuine comprehension failures.

**Dangling modifiers:**
The modifier has no grammatical subject, or its subject is not the sentence's subject.
- *Wrong:* "Having read the report, the conclusions were surprising." (The conclusions didn't read the report.)
- *Right:* "Having read the report, I found the conclusions surprising."

**Ambiguous pronoun references:**
The pronoun's antecedent is unclear.
- *Wrong:* "The manager told the employee he was late." (Who was late?)
- *Right:* "The manager told the employee that the employee was late." Or: "The manager, who was late, told the employee."

**Faulty parallelism:**
Items in a list or series must be grammatically parallel.
- *Wrong:* "The report covers costs, revenue, and how to interpret the data."
- *Right:* "The report covers costs, revenue, and data interpretation."

**Squinting modifiers:**
A modifier that could apply to either the preceding or the following element.
- *Wrong:* "Employees who work hard sometimes get promoted." (Always sometimes? Or sometimes the hard workers get promoted?)

**Clarity at the copy edit stage** is not about making vague sentences specific — that is line editing. It is about removing genuine grammatical ambiguity: sentences where the reader cannot determine the correct meaning from the text.

---

### C4: Coherency

Ensuring that facts do not contradict each other across different sections of the same document.

**What to check:**
- Numbers that appear in multiple places (a statistic in the introduction and again in a later chapter must match)
- Dates and timelines: events must appear in the correct sequence and with consistent dates
- Proper nouns: a person or organization named in one way in chapter 2 must be named the same way in chapter 7
- Claims: an assertion made in the introduction must not be contradicted in the conclusion without acknowledgment
- Cross-references to other sections, chapters, figures, or tables: does the referenced content actually say what the reference implies?

**Coherency is not fact-checking** — verifying whether the underlying claim is true belongs to editorial-structural. Coherency is internal consistency of fact: checking whether the document contradicts itself.

---

## Technical Verification

Beyond the 4 Cs, a professional copy edit includes a technical pass over structural elements.

### Cross-References

- Every "See Chapter 4" or "as discussed in Section 2.3" — verify the referenced section exists and addresses what the cross-reference implies
- Every "See Figure 3.1" or "See Table 2" — verify the figure or table exists and is numbered correctly
- Page number cross-references: flag these (they cannot be verified until layout); note them for the proofreading stage

### Citation and Bibliography

In nonfiction, every factual claim should have a traceable source.
- Every citation in the text has a corresponding entry in the bibliography or notes
- Every bibliography entry has at least one corresponding citation
- Citation format is consistent across all entries (author order, date placement, punctuation, italics vs. quotation marks for titles)
- URLs are present for online sources; access dates per guide
- Author names are spelled consistently between in-text citations and bibliography

### Heading Hierarchy

- All Level 1 headings use the same formatting, capitalization, and punctuation style
- All Level 2 headings under them use the same pattern
- No heading level is skipped (a Level 3 heading should not appear without a Level 2 above it)
- Numbered headings: numbering scheme is consistent and sequential
- Headers read as a coherent skim-path (this overlaps with development, but at the copy stage: verify formatting integrity, not argument integrity)

---

## Three-Pass Execution

Unlike line editing, which relies on ear, copy editing relies on checklists. Run three passes.

**Pass 1 — Style Sheet Setup:**
Before reading the manuscript, establish the Style Sheet:
- Record the governing style guide
- Note any house style rules from `.agents/editorial-context.md`
- Record proper nouns that appear in the brief or title
Begin reading. Add to the Style Sheet with every decision made.

**Pass 2 — The Mechanics Pass (4 Cs Sweep):**
Read through the full text once, applying all four Cs:
- Mark every error (Correctness)
- Check every recurring element against the Style Sheet (Consistency)
- Flag every ambiguous construction (Clarity)
- Note every internal factual conflict (Coherency)
This is a close reading, sentence by sentence. Do not skim.

**Pass 3 — Numbers and Proper Nouns:**
Read through the text once more, this time looking only at:
- All numerals, percentages, dates, and measurements
- All proper names (people, companies, places, titles)
- All abbreviations and acronyms
These are where the most consequential errors live in business nonfiction — wrong numbers and misspelled names are the errors that embarrass.

---

## Two-Phase Process

This skill runs in two phases. Do not skip to Phase 2.

**Phase 1 — Diagnostic (always first):**
Run all three passes and write every finding to `.agents/editorial-context.md` under a `## Copy Issues` heading. Use this format:

```
### C[#] — [Brief descriptor]
- **Location:** [Specific sentence or passage — quote the relevant text]
- **Issue:** [What the error or inconsistency is — name the C: Correctness, Consistency, Clarity, or Coherency]
- **Rule:** [The specific rule violated — cite the style guide and section where applicable]
```

Also record the Style Sheet in full under `## Style Sheet` using the template in [references/STYLE-SHEET-TEMPLATE.md](references/STYLE-SHEET-TEMPLATE.md).

Do not apply corrections in Phase 1. The diagnostic is complete when all issues are documented and the Style Sheet reflects every decision made during the pass.

**Phase 2 — Resolution (after the user reviews):**
Present a summary organized by C category (how many Correctness issues, how many Consistency, etc.) and the completed Style Sheet. The user then chooses:

- **Correct manually** — They apply corrections, then ask whether each satisfies the original issue. Evaluate against the specific rule.
- **Ask Claude to correct** — Work through each C# issue in sequence, stating the correction and the rule it restores. No rewrites — copy editing fixes errors; it does not improve style.

---

## Copy Editing vs. Proofreading

This is the most common point of confusion between these two stages.

| | Copy Editing | Proofreading |
|---|---|---|
| **Stage** | Text is still in word-processor format | Text is in final layout (PDF, typeset pages) |
| **Flexibility** | Can change words to improve clarity | Change words only if flat-out wrong |
| **Scope** | Grammar, style, syntax, internal consistency, citations | Typos, page numbers, layout artifacts, widows/orphans |
| **Style Sheet** | Created here | Consulted here; not started here |
| **Errors caught** | Errors in the text itself | Errors introduced by the layout process |

At the copy editing stage, the text can still move. At proofreading, it cannot.

---

## What Copy Editing Is Not

- It is not rewriting sentences for style or impact — that is line editing
- It is not reorganizing the argument or structure — that is developmental editing
- It is not verifying whether claims are factually accurate against external sources — that is structural editing
- It is not catching layout artifacts, broken links, or widows and orphans — that is proofreading

---

## References

- [STYLE-SHEET-TEMPLATE.md](references/STYLE-SHEET-TEMPLATE.md) — Style sheet template for each new copy edit project

---

## Workflow Position

This is stage 4 of 6 in the editorial workflow:
1. **editorial-structural** — Logic, argument soundness, data accuracy
2. **editorial-development** — Big-picture structure, organization, tone
3. **editorial-line** — Sentence-level craft, word choice, rhythm
4. **editorial-copy** — Grammar, punctuation, style guide adherence *(you are here)*
5. **editorial-typesetting** — Markdown to print-ready LaTeX *(do next)*
6. **editorial-proof** — Final check of the typeset output
