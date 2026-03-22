---
name: editorial-typesetting
description: Typesetting of nonfiction writing — converts copy-edited markdown source files into a complete, print-ready LaTeX document using the memoir class and XeLaTeX. Use when the manuscript is ready to move from word-processor format into final book layout. Handles trim size, margins, fonts, chapter styling, drop caps, running heads, page numbering, front matter, table of contents, and full markdown-to-LaTeX conversion. Also use when the user mentions "typeset," "lay out the book," "convert to LaTeX," "print-ready," "InDesign alternative," "book layout," "trim size," "running heads," "drop caps," or "format for print." Fifth stage of the editorial workflow — after editorial-copy, before editorial-proof.
---

# Typesetting

**Check for editorial context first:** If `.agents/editorial-context.md` exists, read it before beginning. Load the Style Sheet from the copy editing pass — it governs proper noun spelling, capitalization decisions, and number treatment in the typeset output.

## Intake

This stage has more intake questions than any other. Every decision made here is baked into the LaTeX preamble and cannot easily be changed later. Take them seriously.

Read the context file. Then ask for everything below that is not already captured. Ask all required questions before generating anything.

---

### Group 1: Document Structure

**Required:**
1. **What are the source files?** List the markdown files that make up the book, in order. Include front matter (title page, copyright, dedication, preface) and back matter (appendices, notes, about the author) if they exist. If the files are in the project directory, scan for `.md` files and present the list for the user to confirm order.
2. **What front matter does this book include?** (Confirm which apply: half-title page, title page, copyright page, dedication, epigraph, foreword, preface, acknowledgments, introduction. Note whether the introduction is front matter or Chapter 1.)
3. **What back matter does this book include?** (Confirm which apply: epilogue, afterword, appendix/appendices, endnotes or bibliography, index, about the author.)
4. **Does the book use parts** (Part I, Part II…) above the chapter level?

---

### Group 2: Page Geometry

**Required:**
5. **Trim size** — What are the finished page dimensions? Common options:
   - 5" × 8" (compact trade paperback)
   - 5.5" × 8.5" (standard trade paperback)
   - 6" × 9" (larger trade paperback — most common for nonfiction)
   - 7" × 10" (textbook/workbook)
   - 8.5" × 11" (manual, workbook)
   - Custom (specify width × height in inches)

6. **Bleed** — Does this book have any full-bleed elements: images, color backgrounds, or design elements that extend to the page edge and must be cut flush? If yes: standard bleed is **0.125" (3mm)** on all edges that will be cut (head, foot, and fore-edge — not the spine). If no: bleed is 0. Most text-only nonfiction interiors have no bleed.
   - **What bleed does in LaTeX:** The stock size (the PDF page) is made larger than the trim size by the bleed amount, and `\settrims` positions the trim box within it. This is what print vendors require to cut pages correctly.
   - If bleed is 0, stock size equals trim size and no trim marks are needed.

7. **Binding type** — How will this book be bound? The binding method determines the minimum gutter (inner margin) required to keep text from disappearing into the spine.
   - **Perfect bound** (softcover, POD services like KDP, IngramSpark) — most common for trade nonfiction
   - **Case bound** (hardcover, sewn signatures) — requires more gutter than perfect bound
   - **Saddle stitch** (stapled booklet, under ~64 pages) — minimal gutter needed
   - **Spiral or comb bound** (workbooks, manuals) — minimal gutter; pages open flat

8. **Page count estimate** — Approximately how many pages will the finished book be? This is needed to calculate the gutter. Thicker spines absorb more of the inner margin on press. If unknown, estimate from word count (roughly 250–300 words per page at 11pt in a 6×9 trim).

9. **Gutter (inner margin)** — The inner margin must be wide enough that text remains readable after the pages curve into the binding. Recommended minimums by binding type and page count:

   | Pages | Perfect bound | Case bound |
   |---|---|---|
   | Up to 150 | 0.75" | 0.875" |
   | 151–300 | 0.875" | 1" |
   | 301–500 | 1" | 1.125" |
   | 501–700 | 1.125" | 1.25" |
   | 700+ | 1.25" | 1.375" |

   Use the recommended value, or specify a custom gutter.

10. **Remaining margins** — Outer (fore-edge), top (head), and bottom (foot). Standard recommendations by trim size:

    | Trim | Outer | Top | Bottom |
    |---|---|---|---|
    | 5" × 8" | 0.625" | 0.75" | 0.875" |
    | 5.5" × 8.5" | 0.75" | 0.875" | 1" |
    | 6" × 9" | 0.75" | 0.875" | 1" |
    | 7" × 10" | 0.875" | 1" | 1.125" |
    | 8.5" × 11" | 1" | 1" | 1.25" |

    The outer margin is always narrower than the inner — the eye needs less white space on the open side than on the bound side. Increase the bottom margin if the page number sits in the footer.

11. **Safe zone** — All critical content (text, page numbers) must sit inside a safe zone inset from the trim edge to survive minor cutting variance on press. Standard: **0.125"** inside the trim on all sides. For most books this is already satisfied by the margins above — confirm with the print vendor if in doubt.

---

### Group 3: Typography

**Required:**
12. **Body font — serif or sans-serif?** Serif is standard for book-length prose (easier to read in long form). Sans-serif is sometimes used for technical manuals or highly designed nonfiction.
    - Serif options (all free/open source): EB Garamond (elegant, classical), Palatino (warm, widely used), Linux Libertine (clean, book-like)
    - Sans-serif options: Source Sans Pro (neutral, readable), Fira Sans (modern)
    - If the user has a specific font installed on their system (e.g., Minion Pro, Caslon), it can be used with XeLaTeX.

13. **Font size** — 10pt, 11pt, or 12pt?
    - 10pt: dense, for long books where page count matters
    - 11pt: standard for most trade nonfiction (recommended default)
    - 12pt: more open, suits shorter books or academic work

14. **Heading font** — Same as body font, or a different font for chapter titles and section headings? If different, serif or sans-serif, or a specific font name?

---

### Group 4: Chapter and Section Styling

**Required:**
15. **Drop caps** — Should each chapter opening use a dropped capital (a large decorative first letter)? If yes: how many lines deep should the drop cap be? (Standard: 2–3 lines.)

16. **Chapter title style** — How should chapter titles be presented?
    - **Centered, title case** (most common for literary nonfiction)
    - **Centered, all caps** (formal, authoritative)
    - **Flush left** (modern, editorial)
    - **With chapter number above** ("Chapter One" / "CHAPTER 1" above the title on a separate line)
    - **Number only, large** (a large numeral with the title below — contemporary design)
    - **No chapter number, title only**

17. **Section break style** — How should breaks between sections within a chapter be marked?
    - Ornamental glyph (❧ ❦ ✦ — specify or accept default)
    - Three spaced asterisks: `* * *`
    - Three spaced pound signs: `# # #`
    - Plain extra vertical space (no visible mark)

18. **Paragraph style** — First-line indent (standard for book prose) or block paragraphs with space between (common in business/digital writing)?

---

### Group 5: Running Heads and Page Numbers

**Required:**
19. **Running head content:**
    - Verso pages (left/even pages): author name, or book title?
    - Recto pages (right/odd pages): book title, or current chapter title?
    - Common pattern: verso = Author Name | recto = Chapter Title
    - All caps, small caps, or mixed case for running head text?

20. **Page number placement:**
    - Outside corner of the header (standard for two-sided books — number on the left on verso pages, right on recto pages)
    - Center of the footer
    - Outside corner of the footer

21. **Front matter page numbering:**
    - Roman numerals (i, ii, iii…) for front matter, Arabic numerals (1, 2, 3…) restarting at the first chapter? (Standard for traditional book publishing — strongly recommended.)
    - Or Arabic numerals throughout?

22. **Suppress headers on:**
    - Chapter opening pages (the page where a new chapter begins)? (Standard practice: yes — these pages carry a "chapter plain" style with no running head.)
    - Blank pages? (Standard practice: yes — a blank page with a running head looks like an error.)
    - Title page and copyright page? (Always yes — these are never headed.)

---

### Group 6: Front Matter Content

**Required to generate front matter:**
23. **Title page information:**
    - Book title (exact, as it should appear on the title page — may differ from working title)
    - Subtitle (if any)
    - Author name (exactly as it should appear)
    - Publisher name (if applicable)
    - City of publication (if applicable)

24. **Copyright page information:**
    - Copyright year
    - Copyright holder (author name, or publisher name)
    - Edition statement (if applicable — "First edition," "Second edition")
    - ISBN (if known)
    - Any required legal language (e.g., "All rights reserved," "Printed in the United States of America")
    - Permissions or credits for quoted material, if applicable

25. **Table of contents** — Include a generated TOC? If yes:
    - To what depth? (Chapter titles only, or include section headings within chapters?)
    - Should the TOC list front matter items (Preface, Acknowledgments) or only numbered chapters?

**For dedication/epigraph (if applicable):**
26. Dedication text (short — typically one sentence or one line)
27. Epigraph text and attribution (the quote and its source)

---

### Group 7: Compilation

**Helpful:**
28. What operating system and LaTeX distribution is the user running? (macOS with MacTeX, Windows with MiKTeX/TeX Live, Linux with TeX Live.) This affects compile instructions.
29. Does the user have a preferred LaTeX editor? (TeXShop, VS Code with LaTeX Workshop, Overleaf, command line.) This affects workflow guidance.

---

Record all answers in `.agents/editorial-context.md` under a `## Typesetting Decisions` heading using the template in [references/TYPESETTING-RECORD.md](references/TYPESETTING-RECORD.md) before generating any LaTeX.

---

## What This Stage Produces

The output of this stage is a complete, compilable LaTeX project:

```
output/
├── main.tex              # Root file — \input all chapters
├── preamble.tex          # All packages and design settings
├── frontmatter/
│   ├── halftitle.tex     # Half-title page (if included)
│   ├── titlepage.tex     # Title page
│   ├── copyright.tex     # Copyright page
│   ├── dedication.tex    # Dedication (if included)
│   ├── epigraph.tex      # Epigraph (if included)
│   ├── toc.tex           # Table of contents (if included)
│   ├── foreword.tex      # Foreword (if included)
│   ├── preface.tex       # Preface (if included)
│   └── acknowledgments.tex
├── chapters/
│   ├── ch01.tex
│   ├── ch02.tex
│   └── ...
└── backmatter/
    ├── appendix.tex      # Appendix/appendices (if included)
    ├── notes.tex         # Endnotes or bibliography (if included)
    └── aboutauthor.tex   # About the author (if included)
```

Compile with XeLaTeX (run twice to resolve cross-references and TOC):
```bash
xelatex main.tex
xelatex main.tex
```

---

## LaTeX Foundation: The memoir Class

All output uses the `memoir` document class. `memoir` is designed specifically for book-length works and handles trim sizes, margins, header/footer styles, chapter styles, and page layout without requiring dozens of additional packages.

**Compile engine:** XeLaTeX (required for `fontspec` and modern OpenType fonts).

**Core preamble structure:**

```latex
\documentclass[<fontsize>pt, twoside, openright]{memoir}

% --- PDF/X compliance ---
% Load FIRST — pdfx subsumes hyperref; do not also load hyperref separately.
% Use [x-1a] for IngramSpark, most offset printers, and KDP.
% Use [x-3] only if the vendor explicitly permits RGB color.
\usepackage[x-1a]{pdfx}

% --- Page geometry ---
\setstocksize{<height>in}{<width>in}
\settrimmedsize{\stockheight}{\stockwidth}{*}
\settrims{0pt}{0pt}
\setlrmarginsandblock{<inner>in}{<outer>in}{*}
\setulmarginsandblock{<top>in}{<bottom>in}{*}
\checkandfixthelayout

% --- Language and hyphenation patterns ---
\usepackage[american]{babel}   % change to [british] if needed

% --- Fonts (XeLaTeX/fontspec) ---
\usepackage{fontspec}
\setmainfont{<Body Font>}[Ligatures=TeX, Ligatures=Common]
\setsansfont{<Heading Font>}[Ligatures=TeX]   % omit if heading font = body font

% --- Microtypography ---
% expansion=false is required for XeLaTeX; expansion silently fails otherwise.
\usepackage[protrusion=true, expansion=false]{microtype}

% --- Quotation marks ---
\usepackage[autostyle]{csquotes}
% Use \enquote{...} for all quotations in the source — never raw "..." or ``...''

% --- Drop caps (include only when drop caps are enabled) ---
\usepackage{lettrine}

% --- Widow, orphan, and consecutive hyphenation penalties ---
\widowpenalty=10000
\clubpenalty=10000
\displaywidowpenalty=10000
\doublehyphendemerits=10000
\finalhyphendemerits=5000

% --- Page layout ---
\raggedbottom   % prevents ugly vertical stretching on short pages

% --- Page style aliases (required for all two-sided books) ---
\aliaspagestyle{cleared}{empty}    % blank pages: no header, no footer
\aliaspagestyle{chapter}{plain}    % chapter opening pages: page number only
\aliaspagestyle{title}{empty}      % title page: nothing

% --- PDF metadata ---
\hypersetup{
  pdftitle={<Book Title>},
  pdfauthor={<Author Name>},
  pdfsubject={},
  pdfkeywords={},
}
```

---

## Preamble Settings by Design Decision

### Trim Size, Bleed, Gutter, and Margins

In memoir, the **stock size** is the PDF page size (trim + bleed on cut edges). The **trim size** is the finished page after cutting. `\settrims` positions the trim box within the stock.

**No bleed (text-only interior — most common):**
```latex
% Stock = trim; no bleed area needed
% Example: 6×9, perfect bound ~300 pages
\setstocksize{9in}{6in}
\settrimmedsize{\stockheight}{\stockwidth}{*}
\settrims{0pt}{0pt}
\setlrmarginsandblock{1in}{0.75in}{*}    % inner (gutter), outer
\setulmarginsandblock{0.875in}{1in}{*}   % top, bottom
\checkandfixthelayout
```

**With bleed (full-bleed images or color backgrounds):**
```latex
% Stock = trim + bleed on head, foot, and fore-edge (NOT spine)
% Example: 6×9 trim with 0.125" bleed
\setstocksize{9.25in}{6.125in}           % height + 2×bleed, width + 1×bleed
\settrimmedsize{9in}{6in}{*}
\settrims{0.125in}{0.125in}             % top offset, spine offset (0 bleed at spine)
\setlrmarginsandblock{1in}{0.875in}{*}  % inner (gutter), outer (outer must clear safe zone)
\setulmarginsandblock{1in}{1.125in}{*}  % top, bottom (must clear bleed + safe zone)
\checkandfixthelayout
```

**Gutter note:** The inner margin is the gutter. When bleed is present, the outer, top, and bottom margins must be large enough that text sits at least 0.125" inside the trim line (safe zone) even after the bleed area is removed. Verify: outer margin (0.875") − safe zone (0.125") = 0.75" of visible margin — acceptable. If the outer margin is smaller than 0.25", increase it.

### Running Heads and Page Numbers

```latex
% Define a page style named 'main'
\makepagestyle{main}

% Recto (odd/right) page: chapter title right, page number far right
\makeoddhead{main}{}{}{\itshape\rightmark\quad\thepage}

% Verso (even/left) page: page number far left, author name left
\makeevenhead{main}{\thepage\quad\itshape Author Name}{}{}

% Chapter opening pages: page number only, no running head
\makepagestyle{chapter}
\makeoddfoot{chapter}{}{\thepage}{}
\makeevenfoot{chapter}{}{\thepage}{}

% Apply styles
\pagestyle{main}
\aliaspagestyle{chapter}{chapter}
\aliaspagestyle{cleared}{empty}   % blank pages: no header
```

For all-caps running heads, wrap content in `\MakeUppercase{...}` or `\MakeTextUppercase{...}` (with `textcase` package).

For small caps: `\textsc{\rightmark}`.

### Chapter Title Style

memoir provides built-in chapter styles. Set with `\chapterstyle{<style>}`:
- `default` — number and title on separate lines, default spacing
- `hangnum` — number hangs into the left margin
- `article` — compact, article-like
- `veelo` — large number, elegant spacing
- `bianchi` — bold number, horizontal rule
- `demo2` — contemporary, sans number label

For fully custom chapter styling, use `\makechapterstyle`. A centered, title-case style with "Chapter N" above:

```latex
\makechapterstyle{customcentered}{%
  \renewcommand{\printchaptername}{\centering\chapterfont CHAPTER}
  \renewcommand{\chapternamenum}{\space}
  \renewcommand{\printchapternum}{\chapterfont\thechapter}
  \renewcommand{\afterchapternum}{\par\vspace{1em}}
  \renewcommand{\printchaptertitle}[1]{\centering\Large\itshape ##1}
}
\chapterstyle{customcentered}
```

### Drop Caps

```latex
\usepackage{lettrine}

% In each chapter, first paragraph opens with:
\lettrine[lines=3, lraise=0.1]{T}{he} opening words continue here...
```

The `lines` parameter sets the drop cap height. `lraise` adjusts vertical alignment. This must be applied manually to the first paragraph of each chapter during conversion.

### Section Breaks

For ornamental breaks, define a command:
```latex
\newcommand{\sectionbreak}{%
  \vspace{2em}
  \begin{center}❧\end{center}  % replace with preferred glyph
  \vspace{1em}
}
```

Use `\sectionbreak` in the text where `---` or `* * *` appears in the markdown.

### Front Matter Roman Numerals

```latex
\frontmatter   % switches to Roman numerals
% ... title page, copyright, TOC, preface ...
\mainmatter    % switches to Arabic, restarts at 1
% ... chapters ...
\backmatter    % no chapter numbers; Roman or Arabic per preference
```

---

## Markdown-to-LaTeX Conversion

See [references/MARKDOWN-TO-LATEX.md](references/MARKDOWN-TO-LATEX.md) for the full conversion table.

**Core conversion rules applied during chapter conversion:**

| Markdown | LaTeX |
|---|---|
| `# Chapter Title` | `\chapter{Chapter Title}` |
| `## Section` | `\section{Section}` |
| `### Subsection` | `\subsection{Subsection}` |
| `**bold**` | `\textbf{bold}` |
| `*italic*` | `\textit{italic}` |
| `> blockquote` | `\begin{quote}...\end{quote}` |
| `---` (section break) | `\sectionbreak` |
| `- item` (unordered list) | `\begin{itemize}\item...\end{itemize}` |
| `1. item` (ordered list) | `\begin{enumerate}\item...\end{enumerate}` |
| `[text](url)` | `\href{url}{text}` |
| `![alt](path)` | `\includegraphics[width=\linewidth]{path}` |
| Em dash `---` in prose | `---` (memoir handles correctly) |
| Smart quotes | Convert to `\enquote{...}` (with `csquotes`) or `''...''` |
| Footnote `[^1]` | `\footnote{...}` |

---

## Two-Phase Process

This stage has a different shape from the editorial stages — it produces an artifact rather than a diagnostic.

**Phase 1 — Generate and Review:**
1. Record all design decisions in the Typesetting Record (`.agents/editorial-context.md`)
2. Generate `preamble.tex` from the design decisions
3. Generate all front matter files
4. Convert each markdown chapter file to a `.tex` file in the `chapters/` directory
5. Generate `main.tex` assembling all files in order
6. Present the generated files to the user with a summary: what was generated, what assumptions were made, what requires user verification
7. Provide compile instructions specific to the user's platform and editor

**Phase 2 — Verification and Correction:**
The user compiles the document and reviews the output. Common issues to address:
- Chapter titles that need manual styling adjustment
- Drop cap placement on chapters that open with a quote or unusual character
- Section break placement (markdown `---` may need to be disambiguated from front matter rules)
- Image paths that need updating to the actual asset locations
- Overfull `\hbox` warnings from long words or URLs that don't break cleanly (add `\sloppy` or manual `\linebreak` at the offending line)
- TOC depth that needs trimming

After corrections, recompile twice to ensure TOC page numbers are resolved.

**Then invoke `latex-book`** before proceeding to `editorial-proof`. `latex-book` audits the generated `.tex` files and compiled PDF against print production requirements — font embedding, PDF/X compliance, widow penalties, page style aliases, and compile log warnings. Address all TX# issues it identifies before the document is considered typeset-ready. `latex-book` is a quality gate, not an optional pass.

---

## What This Stage Is Not

- It is not making editorial changes to the text — that is complete by the time typesetting begins
- It is not a graphic design service — it produces a clean, professional typeset layout, not a custom designed cover or interior with bespoke illustration
- It is not a substitute for a professional compositor for highly complex layouts (books with heavy illustration, complex tables, or multi-column layouts may need InDesign)
- It does not proofread the output — errors in layout are caught by editorial-proof, which runs after this stage

---

## References

- [TYPESETTING-RECORD.md](references/TYPESETTING-RECORD.md) — Design decision template (analogous to the copy editing Style Sheet)
- [MARKDOWN-TO-LATEX.md](references/MARKDOWN-TO-LATEX.md) — Full markdown-to-LaTeX conversion reference

---

## Workflow Position

This is stage 5 of 6 in the editorial workflow:
1. **editorial-structural** — Logic, argument soundness, data accuracy
2. **editorial-development** — Big-picture structure, organization, tone
3. **editorial-line** — Sentence-level craft, word choice, rhythm
4. **editorial-copy** — Grammar, punctuation, style guide adherence
5. **editorial-typesetting** — Markdown to print-ready LaTeX *(you are here)*
6. **editorial-proof** — Final check of the typeset output *(do next)*
