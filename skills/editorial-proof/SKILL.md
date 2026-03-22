---
name: editorial-proof
description: Proofreading of nonfiction writing in its final laid-out form — using a professional five-pass method to catch typos from layout, orphans, widows, broken links, and formatting artifacts. Use only after the text has been typeset and placed in its final format (PDF, web page, formatted document, typeset galley). Also use when the user mentions "proofread," "final check," "catch typos," "orphans and widows," "broken links," "layout errors," "before we publish," "final pass," "proof the PDF," or "galley." Sixth and final stage of the editorial workflow — only after editorial-typesetting produces the final layout. Do NOT use for stylistic or content changes.
---

# Proofreading

**Check for editorial context first:** If `.agents/editorial-context.md` exists, read it before beginning. Load the Style Sheet from the copy editing pass if it's there — it defines the standard the layout must match.

## Intake

Read the context file. Then ask for anything not already captured. Proofreading is stage-dependent — several of these questions are gatekeeping questions, not just helpful context.

**Required — cannot begin without these:**
1. What is the final format of the document? (PDF from typeset LaTeX, formatted Word document, typeset book pages, web page ready for publication, other.) The format determines which error types apply — widows and orphans matter in a typeset PDF; broken links matter in a web document; both matter in a formatted Word doc.
2. **For print books (PDF from `editorial-typesetting`):** Has `latex-book` been run and all TX# issues resolved? If not, **stop and flag it** — proofreading a PDF that still has print production errors wastes the pass. Ask whether to return to `latex-book` first.
   **For all other formats (Word, web, etc.):** Has copy editing been completed and approved by the author? If the answer is no or uncertain, **stop and flag it** — proofreading before copy editing is complete will miss errors that belong to an earlier stage. Ask whether to proceed or return to `editorial-copy` first.

**Required to scope the proof correctly:**
3. Is the Style Sheet from the copy editing pass available? If yes, it will be used to verify the layout matches the approved text. If no, ask whether one exists — proofreading without a Style Sheet means consistency decisions cannot be verified.
4. Which of the following elements does the document contain? (Ask the user to confirm what's present — only check what's there.)
   - Table of contents
   - Index
   - Running headers or footers
   - Footnotes or endnotes
   - Figures or tables with captions
   - Hyperlinks or interactive elements
   - Contact information, CTAs, or a phone number / email

**Helpful if not already captured:**
5. What tool or platform was used for layout? (Adobe InDesign, Microsoft Word, Google Docs, web CMS, other.) Different tools introduce different conversion errors.
6. Is there a clean, approved copy-edited version to compare the layout against, or only the final layout document?
7. Is there a known deadline for corrections, or will a compositor apply them? (Shapes how issues are documented — compositor needs precise location codes; author self-correcting needs plain language.)

Record all answers in `.agents/editorial-context.md` before beginning the five passes.

---

## The Critical Distinction

Proofreading is not a second copy edit. It is a different job.

**Copy editing** works on a live word-processor document — text is still fluid, words can be changed for clarity, consistency decisions are still being made.

**Proofreading** works on a proof — a PDF, a staged web page, a typeset galley. By this stage, all content, style, and grammar decisions have been finalized. The proofreader is looking for a single category of problem: **errors introduced by the formatting process itself.**

If you are reading a Word document again after copy editing, you are doing a final copy-edit pass, not a proof. True proofreading assumes the text has moved from a live document into a fixed format, and that move can introduce errors that weren't there before.

**The proofreader makes no stylistic judgments.** If a sentence reads awkwardly, that ship has sailed. If a word choice is weak, that belongs to line editing. The proofreader's scope is production errors only — and that scope must be held strictly.

**If a proofreader finds something that should have been caught at a prior stage:** Flag it clearly, note which stage it belongs to, and let the author decide. Don't silently fix it, and don't silently ignore it.

---

## Why Layered Passes: Brain Drift

The core problem in proofreading is not attention — it is prediction. Your brain knows what the text is supposed to say, and it reads what it expects rather than what is actually on the page. This is called **brain drift**.

The antidote, established in Peggy Smith's *Mark My Words* and codified in CIEP professional practice, is to **never read the whole document the same way twice.** Each pass isolates a specific type of error and trains your attention on a single category. When you read for everything at once, you catch nothing reliably.

The five passes run in order. Do not combine them.

---

## The Five-Pass Method

### Pass 1: The Global Formatting Scan

**Do not read the words.** Look at the geometry of the page.

The goal is uniformity — every element of the same type should look identical. Read the document as a designer, not a reader.

**Check:**
- **Running heads and footers:** Are page numbers sequential, with no skips or repeats? Is the chapter title or section title in the header correct for each page? Does the footer contain the right information (publication date, document title, page count)?
- **Heading hierarchy:** Do all Level 1 headings use identical formatting — same font, size, weight, and spacing? Do all Level 2 headings match each other? Are there any headings that look different from their peers?
- **Paragraph spacing:** Is the space before and after headings consistent? Is body text spacing uniform throughout?
- **Widows:** A single word or short line sitting alone at the top of a page or column, separated from the rest of its paragraph. Flag for the designer.
- **Orphans:** The first line of a paragraph stranded at the bottom of a page, separated from the rest. Flag for the designer.
- **Stranded headings:** A heading that appears at the bottom of a page with fewer than two lines of body text following it. Flag for the designer.
- **Margin and alignment consistency:** Do text blocks, pull quotes, and callouts align correctly on the page?

---

### Pass 2: The High-Risk Elements (The "Cold Eyes" Pass)

Statistics show that the most visible, most embarrassing errors appear in the largest text. The heading is where everyone was too intimidated to mark a correction — and where everyone in the room will see it.

**Check:**
- **Every heading and subheading:** Read each one in isolation. Look at each word as a standalone unit. Transposed letters and dropped characters are common in large, bold text because the eye slides over it.
- **Table of contents:** Does each entry exactly match the heading as it appears in the document? Does the page number for each entry match the actual page the section starts on? A TOC generated before final pagination is a frequent source of errors.
- **Figure and table labels:** Does "Figure 1" appear under the first figure? Does "Table 3" label the third table? Are labels sequential with no gaps or repeats?
- **Captions:** Does each caption match the figure or table it accompanies? Was a caption accidentally transposed with another?
- **Pull quotes and callouts:** Does the pull quote appear verbatim in the body text? Is the attribution correct?
- **Cover, title page, and copyright page (for books):** Author name, title, subtitle, publisher, date — all verified.

---

### Pass 3: The Mechanical Read

Now read the body text — but read it slowly and literally, one word at a time. The goal is not comprehension; it is character-level accuracy. Read as if you are reading a foreign language you don't speak.

**Techniques to counteract brain drift:**
- Use a ruler or a blank sheet of paper to cover everything below the line you are reading, so your eye cannot skip ahead.
- Point to each word with a pencil or cursor as you read it.
- **The Backward Reading Technique:** For the highest-accuracy sections (titles, headings, abstracts, contact information), read from the last word to the first. This breaks your brain's ability to predict the next word entirely, forcing you to see only what is on the page. It is slow and disorienting — that is the point.

**Check:**
- **Doubled words:** "the the," "and and," "is is" — these typically occur at line breaks where copy-paste stitched two pieces together. They are nearly invisible on a normal read.
- **Missing words:** A word dropped during layout — usually a small word ("a," "the," "in," "of") that the brain supplies automatically.
- **Punctuation pairs:** Every opening quotation mark has a closing one. Every opening parenthesis has a closing one. Every em dash used as a pair has its partner. Read for the pairs, not for the content.
- **Smart quotes vs. straight quotes:** Did the layout process convert smart quotes back to straight quotes (or vice versa) inconsistently? Common in copy-paste and format conversions.
- **Em dash, en dash, hyphen integrity:** Did the layout process convert em dashes to hyphens or en dashes? Check a sample of each type.
- **Proper nouns against the Style Sheet:** Every instance of every proper noun — company names, personal names, product names, place names — verified against the Style Sheet spelling. "Microsoft" not "Mircosoft." "García" not "Garcia" if the diacritic was specified.
- **Abbreviations:** Consistent with the Style Sheet throughout.

---

### Pass 4: The Final Hygiene Check

This pass targets elements that are not part of the main text flow but are frequently the most consequential errors in business nonfiction.

**Check:**
- **Hyperlinks:** Click every link. Does it resolve? Does it go to the correct destination? Is the link text accurate? (A link that says "Chapter 3" should go to Chapter 3, not Chapter 2.)
- **Anchor links:** In long documents, do internal links (footnote numbers, TOC entries, cross-references marked "see page X") navigate correctly?
- **Contact information and CTAs:** In business writing, every phone number, email address, website URL, and "contact us" or "buy now" element must be 100% correct. These are the highest-consequence errors — they directly break the reader's ability to act.
- **Dates and day-of-week accuracy:** "Monday, March 23" — confirm that March 23 is actually a Monday in the year of publication. Date-day mismatches are surprisingly common and look careless.
- **Version and date stamps:** Is the document's date, version number, or "last updated" field correct for this publication?
- **Footnote and endnote numbering:** Are note numbers sequential in the text? Does each in-text number correspond to the correct note content?
- **Index spot-check (if present):** Select 10–15 entries at random. Do they point to pages where the term actually appears?

---

### Pass 5: The Silent Read (The Sense Check)

One final read — this time for sense. Read for showstoppers: errors so egregious they survived every prior pass because they are real words in the right order, but the wrong meaning.

**What to look for:**
- **Wrong-word errors:** "pubic" for "public," "form" for "from," "trail" for "trial" — real words, wrong word, no spell-check catches them.
- **Negation errors:** "The policy does not require approval" vs. "The policy does require approval" — a dropped "not" that reverses the meaning entirely.
- **Number transpositions:** "$1.4 million" that should be "$14 million." These survived the Mechanical Read because the numbers are real numbers; they survived the Hygiene Pass because the digits are present.
- **Attribution errors:** A quote attributed to the wrong person. A statistic credited to the wrong study.
- **Contradictions introduced by layout:** Did moving a text block accidentally place a claim near a claim it contradicts?

This is the only pass where you read for flow and meaning. Keep it fast — you are not editing, you are doing a final scan for catastrophic errors.

---

## Two-Phase Process

This skill runs in two phases. Do not skip to Phase 2.

**Phase 1 — Diagnostic (always first):**
Run all five passes and write every finding to `.agents/editorial-context.md` under a `## Proof Issues` heading. Use this format:

```
### P[#] — [Brief descriptor]
- **Location:** [Page number, section, or element — precise enough for a compositor to find it without searching]
- **Issue:** [What the error is — dropped word, widow, broken link, caption mismatch, wrong word, etc.]
- **Pass:** [Which pass caught it: Formatting / High-Risk / Mechanical / Hygiene / Sense]
- **Action:** [Correct / Flag for designer / Flag for author decision]
```

Do not apply corrections in Phase 1. The diagnostic is complete when all five passes are done and every finding is documented.

**Phase 2 — Resolution (after the user reviews):**
Present a summary by pass category — how many issues per pass type, any patterns. The user then chooses:

- **Correct manually** — They apply corrections, confirm each with Claude. Evaluate and respond.
- **Ask Claude to specify corrections** — Work through each P# issue, stating the exact correction. Corrections to production errors only — no rewrites, no restyling.

After all corrections are applied, recommend a **second proof pass** on the corrected version: every correction is a potential source of a new error. The second pass can be faster — target only the areas where corrections were made, plus Pass 2 and Pass 5.

---

## What Proofreading Is Not

- It is not making stylistic improvements — that is line editing, which is complete
- It is not catching grammar errors that were present in the approved copy-edited text — those belong to an earlier stage
- It is not reorganizing content — that is developmental editing, which is complete
- It is not a judgment call about the writing — it is a quality check on the production process

---

## References

- [PROOF-CHECKLIST.md](references/PROOF-CHECKLIST.md) — Five-pass checklist by element type, for use as a running tally during each pass

---

## Workflow Position

This is stage 6 of 6 in the editorial workflow:
1. **editorial-structural** — Logic, argument soundness, data accuracy
2. **editorial-development** — Big-picture structure, organization, tone
3. **editorial-line** — Sentence-level craft, word choice, rhythm
4. **editorial-copy** — Grammar, punctuation, style guide adherence
5. **editorial-typesetting** — Markdown to print-ready LaTeX
6. **editorial-proof** — Final check of the typeset output *(you are here — this is the end)*
