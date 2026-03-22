---
name: latex-book
description: LaTeX quality audit for memoir/XeLaTeX book production — validates generated .tex files against best practices for print-ready output. Use as a quality gate after editorial-typesetting generates LaTeX source, or independently when reviewing any .tex file intended for commercial printing or POD. Catches errors that will break a print file: overfull lines, unembedded fonts, wrong color mode, missing PDF/X compliance, widow/orphan problems, memoir class misuse, and XeLaTeX/fontspec anti-patterns. Also use when the user mentions "LaTeX quality," "check the tex file," "print preflight," "PDF/X," "KDP," "IngramSpark," "crop marks," or "the PDF was rejected by the printer."
---

# LaTeX Book Quality Audit

**Check for editorial context first:** If `.agents/editorial-context.md` exists, read the Typesetting Decisions record — the chosen trim size, bleed, binding type, font, and PDF target inform what to check and what thresholds to apply.

This skill audits `.tex` files for print-readiness. The editorial-typesetting skill generates LaTeX from markdown; this skill verifies that the output is correct — not just syntactically valid, but professionally sound for commercial book printing or POD submission.

The test of a clean print file: compile it, submit the PDF to the printer, and receive no rejection or technical correction notice.

---

## Intake

If the following are not in `.agents/editorial-context.md`, ask before auditing:

**Required:**
1. Where are the `.tex` files? (Path to `main.tex` or the project root.)
2. What is the target print vendor or format? (KDP, IngramSpark, offset printer, or other POD — each has slightly different requirements for PDF/X level, color mode, and crop marks.)
3. Has the project been compiled successfully at least once? (If not, fix compilation errors first — a PDF that doesn't exist cannot be audited.)

**Helpful:**
4. What font is specified in the preamble? (Needed to check for fake bold/italic issues.)
5. Does the interior contain any color images or color design elements? (Determines CMYK vs. grayscale requirements.)

---

## Audit Categories

Every finding maps to one of five categories. Run them in order.

---

### Category 1: memoir Class Correctness

memoir has specific usage patterns. Deviating from them produces subtle errors that are hard to diagnose after the fact.

**`\checkandfixthelayout` placement:**
- Must appear after ALL geometry commands (`\setstocksize`, `\settrimmedsize`, `\settrims`, `\setlrmarginsandblock`, `\setulmarginsandblock`) and before `\begin{document}`.
- Never called more than once. If geometry changes after the initial call, call it again — but only once per final geometry state.
- Missing `\checkandfixthelayout`: margins silently fail to apply. This is the most common memoir geometry error.

**Page style aliases — the three required:**
```latex
\aliaspagestyle{cleared}{empty}    % blank pages: no header, no footer
\aliaspagestyle{chapter}{plain}    % chapter opening pages: page number only
\aliaspagestyle{title}{empty}      % title page: nothing
```
Missing these means blank pages display running heads (looks like a layout error in print) and chapter opening pages carry a full running head (against typographic convention).

**`\frontmatter` / `\mainmatter` / `\backmatter` sequence:**
- `\frontmatter`: Roman numeral page numbering, no chapter numbering. Must precede the first front matter file.
- `\mainmatter`: Resets page counter to 1, Arabic numerals, chapter numbering active. Must precede Chapter 1.
- `\backmatter`: No chapter numbering, but page numbering continues. Must precede back matter.
- All three must appear in this order, once each. Missing any one produces wrong page numbers in the TOC.

**`openright` and blank pages:**
- `openright` (set in `\documentclass`) forces chapters to begin on recto (odd/right) pages.
- This creates intentional blank pages. They must be styled `empty` via `\aliaspagestyle{cleared}{empty}`.
- Check: is `openright` set? Is `cleared` aliased to `empty`?

**`\raggedbottom` vs `\flushbottom`:**
- memoir defaults to `\flushbottom` for two-sided documents — it stretches vertical space to align bottom margins across facing pages.
- For most trade nonfiction: `\raggedbottom` looks better and avoids ugly inter-paragraph gaps on pages with headings or short paragraphs.
- Recommendation: use `\raggedbottom` unless the book has uniform paragraph density throughout. Add it to the preamble explicitly — don't rely on the default.

**`\epigraph` for chapter epigraphs:**
- memoir provides `\epigraph{text}{attribution}`. Use it rather than manual `\begin{quote}` formatting.
- Correct: `\epigraph{The quote text.}{---Author, \textit{Source}}`
- Anti-pattern: a manually formatted blockquote with `\hfill` attribution.

**Float placement:**
- Use `[tbp]` not `[h]` alone. `[h]` forces the float exactly at that position even if it doesn't fit — this causes ugly column gaps and page overflows in print.
- For full-page figures: `[p]` (figures-only page).

---

### Category 2: XeLaTeX and fontspec Correctness

**Fake bold and fake italic detection:**
- If `\textbf{}` is used with a font that has no dedicated bold face, XeLaTeX synthesizes a "fake bold" by thickening strokes algorithmically. This looks bad in print and is rejected by some prepress workflows.
- Check: does the font specified in `\setmainfont` have explicit `BoldFont` and `BoldItalicFont` entries, or are they being resolved automatically?
- EB Garamond requires explicit specification — it has no traditional bold:
  ```latex
  \setmainfont{EB Garamond}[
    Ligatures=TeX,
    ItalicFont={EB Garamond Italic},
    BoldFont={EB Garamond Medium},
    BoldItalicFont={EB Garamond Medium Italic}
  ]
  ```
- Palatino and Linux Libertine have proper bold faces and resolve automatically.

**Ligature settings:**
- `Ligatures=TeX` is required for correct handling of `--` (en dash), `---` (em dash), and backtick quotes.
- `Ligatures=Common` enables standard typographic ligatures (fi, fl, ff, ffi, ffl). Recommended for all serif body fonts.
- Anti-pattern: `\setmainfont{Font Name}` with no options — em dashes and ligatures may not render correctly.

**microtype with XeLaTeX:**
- Character expansion does not work with XeLaTeX. Use:
  ```latex
  \usepackage[protrusion=true, expansion=false]{microtype}
  ```
- `expansion=true` with XeLaTeX causes a compile warning and is silently ignored — but it signals the preamble was not written for XeLaTeX. Fix it explicitly.

**`csquotes` for all quotation marks:**
- Never use raw `"..."` or `` ``...'' `` in LaTeX source. Use `\enquote{...}` from the `csquotes` package.
- `csquotes` is language-aware (respects `babel`/`polyglossia` settings) and handles nested quotes automatically.
- In the preamble: `\usepackage[autostyle]{csquotes}`
- In the text: `\enquote{This is a quote.}` not `"This is a quote."`
- Anti-pattern: any raw double quote character in the `.tex` source outside of code/verbatim blocks.

**`babel` or `polyglossia` for hyphenation:**
- XeLaTeX requires correct language settings to load the right hyphenation patterns.
- For American English: `\usepackage[american]{babel}` or `\usepackage{polyglossia} \setdefaultlanguage[variant=american]{english}`
- Missing language package: LaTeX falls back to English hyphenation patterns, which may be fine for most US English text but can fail on specific words.

---

### Category 3: Typography Quality

**Widow and orphan penalties:**
Every book preamble must set these. Their absence allows widows and orphans that are invisible at compile time but embarrassing in print:

```latex
\widowpenalty=10000        % prevents last line of paragraph alone at top of page
\clubpenalty=10000         % prevents first line of paragraph alone at bottom of page
\displaywidowpenalty=10000 % prevents widows before display math
```

A value of 10000 prohibits the condition entirely. LaTeX will adjust spacing elsewhere to avoid it. Values of 9000+ strongly discourage but allow as a last resort.

**Consecutive hyphenation:**
```latex
\doublehyphendemerits=10000   % discourages two consecutive hyphenated lines
\finalhyphendemerits=5000     % discourages hyphen on second-to-last line of paragraph
```

**Overfull `\hbox` — lines extending into the margin:**
- Every `Overfull \hbox` warning in the compile log is a line that protrudes into the margin in the printed book.
- Causes: words LaTeX cannot hyphenate, URLs, long proper nouns.
- Fixes (in order of preference):
  1. Add hyphenation exception: `\hyphenation{In-gram-Spark}`
  2. Add discretionary hyphen in the source: `In\-gram\-Spark`
  3. Rewrite the offending sentence
  4. Use `\sloppy` locally as a last resort (increases word spacing — use sparingly)
- **Zero overfull boxes is the target.** Every one that ships is a visible error.

**Underfull `\vbox` with `\flushbottom`:**
- Common on pages where chapters end near the bottom.
- Fix: switch to `\raggedbottom`.

---

### Category 4: Print-Ready PDF Requirements

**Font embedding — non-negotiable:**
- All fonts must be fully embedded in the output PDF. Unembedded fonts cause immediate rejection by every commercial printer.
- XeLaTeX embeds fonts by default when fonts are loaded via `fontspec`.
- Verify after compile: `pdffonts main.pdf` (command line). Every entry in the "emb" column must read "yes."
- If any font is not embedded: identify it, find where it enters the document (often a diagram or included PDF), and resolve.

**PDF/X compliance:**
- PDF/X is the print industry standard for "ready-to-print" PDFs. It enforces font embedding, color profiles, and no transparency among other requirements.
- **PDF/X-1a**: most widely required — all color must be CMYK or spot color, no transparency, all fonts embedded. Required by IngramSpark and most offset printers.
- **PDF/X-3**: allows RGB color — acceptable for some digital printers and KDP.
- Use the `pdfx` package:
  ```latex
  \usepackage[x-1a]{pdfx}   % or [x-3] for PDF/X-3
  ```
- `pdfx` must be loaded **before** `hyperref` — or it will be loaded instead of `hyperref` (it includes equivalent functionality).
- Check: is `pdfx` in the preamble? Is it loaded in the right order?

**Color mode:**
- **Black-and-white interior** (most trade nonfiction): grayscale. All images must be grayscale. Any RGB or CMYK image will be flagged in preflight.
- **Color interior**: CMYK. RGB images must be converted to CMYK before inclusion. XeLaTeX does not convert color spaces automatically.
- Check: does the color mode of every included image match the document's color requirement?

**Crop marks:**
- When bleed is present (stock size > trim size), crop marks show the cutter where to trim.
- **POD vendors (KDP, IngramSpark):** Do NOT include crop marks in the interior PDF. The vendor adds them. Submitting a PDF with crop marks to a POD vendor typically causes rejection.
- **Offset printers:** Require crop marks. Use the `crop` package or confirm with the printer whether to include them or deliver a bleed-only PDF.
- Check: is the bleed present? Is the vendor a POD service? If both yes — crop marks must be absent from the PDF.

**PDF metadata:**
```latex
\hypersetup{
  pdftitle={Exact Book Title},
  pdfauthor={Author Name},
  pdfsubject={Subject or genre},
  pdfkeywords={keyword1, keyword2},
  pdfproducer={XeLaTeX with memoir class},
}
```
Missing metadata won't reject a print job, but it is required for ISBN registration workflows and good practice for distribution.

**Image resolution:**
- Photographs and raster images: minimum **300 DPI** at final printed size.
- Line art, diagrams, logos: minimum **600 DPI**, or use vector format (PDF, EPS, or SVG converted to PDF).
- Check: are any included images raster? If so, verify DPI. An image that looks fine on screen at 72 DPI will be visibly pixelated at 300 DPI in print.

---

### Category 5: Compile Log Errors and Warnings

After each compile, the log must be reviewed. Not all warnings are benign.

**Errors (must fix before submitting):**
- `! Font ... not loadable` — font not installed or name wrong
- `! LaTeX Error: File '...' not found` — missing image or included file
- `! Undefined control sequence` — command typo or missing package
- `! Missing $ inserted` — math mode entered unintentionally

**Warnings that are print errors:**
- `Overfull \hbox` — line protrudes into margin (see Category 3)
- `Font shape ... not available, using ... instead` — font fallback triggered; likely fake bold/italic

**Warnings that can be ignored:**
- `Underfull \hbox (badness ...)` — minor spacing adjustment, usually fine
- `PDF inclusion: found PDF version 1.x, but at most 1.y allowed` — version mismatch, usually harmless but worth noting

---

## Two-Phase Process

**Phase 1 — Audit:**
Read the `.tex` files and compile log. Document every finding in `.agents/editorial-context.md` under `## LaTeX Audit Issues`:

```
### TX[#] — [Brief descriptor]
- **File:** [Which .tex file — preamble.tex, main.tex, ch01.tex, etc.]
- **Category:** [memoir / fontspec / Typography / PDF / Compile log]
- **Issue:** [What the problem is]
- **Fix:** [The specific correction to make]
```

Unlike the editorial skills, fixes are included in Phase 1 — LaTeX issues have definitive correct solutions, not author-judgment calls.

**Phase 2 — Resolution:**
Work through each TX# issue in sequence, applying the fix directly to the `.tex` file. After all fixes, recompile and confirm the log is clean. Run the preflight checklist in [references/PRINT-PREFLIGHT.md](references/PRINT-PREFLIGHT.md) before declaring the file print-ready.

---

## What This Skill Is Not

- It is not a substitute for the print vendor's own preflight — always run the vendor's preflight tool on the final PDF before submitting
- It is not a design review — whether the layout looks good is assessed by reading the compiled PDF, not the source
- It is not a proofreading pass — textual errors in the `.tex` source belong to `editorial-proof`

---

## Companion Skills

- **editorial-typesetting** — generates the LaTeX this skill audits; invoke `latex-book` after the initial generation
- **editorial-proof** — proofreads the compiled PDF output; runs after `latex-book` confirms the source is clean

---

## References

- [PRINT-PREFLIGHT.md](references/PRINT-PREFLIGHT.md) — Final checklist before submitting the PDF to a printer or POD vendor
