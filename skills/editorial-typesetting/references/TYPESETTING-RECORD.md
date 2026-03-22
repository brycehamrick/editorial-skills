# Typesetting Decision Record

Copy this template into `.agents/editorial-context.md` under a `## Typesetting Decisions` heading at the start of the typesetting stage. Fill in every field before generating any LaTeX. This record is the equivalent of the copy editing Style Sheet — it documents every design decision so the layout is reproducible and any future corrections can be made consistently.

---

## Typesetting Decisions

**Project:** [Title]
**Date:** [Date]
**Compiler:** XeLaTeX
**Document class:** memoir

---

### Document Structure

**Source files (in order):**

| # | File | Type | Notes |
|---|---|---|---|
| | | Front matter / Chapter / Back matter | |

**Front matter elements present:**
- [ ] Half-title page
- [ ] Title page
- [ ] Copyright page
- [ ] Dedication
- [ ] Epigraph
- [ ] Table of contents
- [ ] List of figures / List of tables
- [ ] Foreword (author: _________)
- [ ] Preface
- [ ] Acknowledgments
- [ ] Introduction (treated as: [ ] Front matter  [ ] Chapter 1)

**Back matter elements present:**
- [ ] Epilogue
- [ ] Afterword
- [ ] Appendix / Appendices (how many: ___)
- [ ] Endnotes / Bibliography
- [ ] Index
- [ ] About the author

**Part structure:** [ ] Yes — Parts above chapter level  [ ] No

---

### Page Geometry

**Trim size:** _______ × _______ inches (width × height)

**Bleed:**
- Full-bleed elements present: [ ] Yes  [ ] No
- Bleed amount: [ ] 0.125" (3mm) standard  [ ] None  [ ] Other: _______
- Edges with bleed: [ ] Head  [ ] Foot  [ ] Fore-edge  (spine never bleeds)

**Stock size (PDF page dimensions):**
- If no bleed: same as trim → _______ × _______ in
- If bleed: trim + bleed on cut edges → _______ × _______ in
- `\settrims` offset (top, spine): _______ in, _______ in

**Binding type:** [ ] Perfect bound  [ ] Case bound  [ ] Saddle stitch  [ ] Spiral

**Estimated page count:** _______ pages

**Gutter (inner margin):** _______ in
*(Recommended minimums: ≤150pp perfect 0.75" / case 0.875" | 151–300pp 0.875"/1" | 301–500pp 1"/1.125" | 501–700pp 1.125"/1.25" | 700pp+ 1.25"/1.375")*

**Remaining margins:**
- Outer (fore-edge): _______ in
- Top (head): _______ in
- Bottom (foot): _______ in

**Safe zone:** [ ] 0.125" standard  [ ] Other: _______
*(Confirm all text and page numbers sit at least this far inside the trim edge)*

**LaTeX geometry block:**
```latex
\setstocksize{<stock-height>in}{<stock-width>in}
\settrimmedsize{<trim-height>in}{<trim-width>in}{*}
\settrims{<top-offset>in}{<spine-offset>in}
\setlrmarginsandblock{<gutter>in}{<outer>in}{*}
\setulmarginsandblock{<top>in}{<bottom>in}{*}
\checkandfixthelayout
```

---

### Typography

**Body font:** _______________________________
**Font source:** [ ] System font  [ ] LaTeX package  [ ] Google Fonts / downloaded

**Heading font:** [ ] Same as body  [ ] Different: _______________________________

**Font size:** [ ] 10pt  [ ] 11pt  [ ] 12pt

**Leading (line spacing):** [ ] memoir default  [ ] Custom: _______

**Small caps available in font:** [ ] Yes  [ ] No

---

### Chapter and Section Styling

**Drop caps:** [ ] Yes — _______ lines deep  [ ] No

**Chapter title style:**
- Alignment: [ ] Centered  [ ] Flush left  [ ] Other: _______
- Case: [ ] Title case  [ ] All caps  [ ] Small caps
- Chapter number: [ ] Above title ("Chapter N")  [ ] Same line  [ ] Large numeral  [ ] None
- memoir chapter style name (if using built-in): _______________________

**Section heading style (##):**
- Alignment: [ ] Flush left  [ ] Centered
- Weight: [ ] Bold  [ ] Italic  [ ] Bold italic
- Case: [ ] Title case  [ ] All caps  [ ] As written

**Section break style:**
- [ ] Ornamental glyph: _______
- [ ] * * *
- [ ] # # #
- [ ] Extra vertical space only

**Paragraph style:**
- [ ] First-line indent (standard for book prose)
- [ ] Block paragraphs with vertical space between

---

### Running Heads and Page Numbers

**Verso (left/even) pages — running head content:**
- [ ] Author name (exactly as it should appear: _______________________)
- [ ] Book title
- [ ] Other: _______________________

**Recto (right/odd) pages — running head content:**
- [ ] Current chapter title
- [ ] Book title
- [ ] Other: _______________________

**Running head case:**
- [ ] Mixed case (as written)
- [ ] All caps (`\MakeUppercase`)
- [ ] Small caps (`\textsc`)

**Running head style:** [ ] Italic  [ ] Roman  [ ] Bold

**Page number placement:**
- [ ] Outside corner of header (left on verso, right on recto) — standard
- [ ] Center of footer
- [ ] Outside corner of footer

**Front matter page numbering:**
- [ ] Roman numerals for front matter, Arabic restarting at Chapter 1 — standard
- [ ] Arabic throughout

**Suppress running heads on:**
- [ ] Chapter opening pages — standard
- [ ] Blank pages — standard
- [ ] Title page — always
- [ ] Copyright page — always

---

### Front Matter Content

**Title page:**
- Title: _______________________________
- Subtitle: _____________________________ (or none)
- Author: _______________________________
- Publisher: ____________________________ (or none)
- City: _________________________________ (or none)

**Copyright page:**
- Year: _______
- Holder: _______________________________
- Edition: ______________________________
- ISBN: _________________________________
- Legal language: _______________________
- Permissions/credits: __________________

**Dedication:** ___________________________________ (or none)

**Epigraph text:**
```
[Quote text here]
```
**Epigraph attribution:** _______________________

**Table of contents:**
- [ ] Include  [ ] Omit
- Depth: [ ] Chapters only  [ ] Chapters + sections  [ ] Chapters + sections + subsections
- [ ] Include front matter items (Preface, Acknowledgments) in TOC

---

### Compilation

**Operating system:** [ ] macOS  [ ] Windows  [ ] Linux

**LaTeX distribution:** [ ] MacTeX  [ ] MiKTeX  [ ] TeX Live

**Preferred editor / workflow:**
- [ ] TeXShop (macOS)
- [ ] VS Code with LaTeX Workshop
- [ ] Overleaf
- [ ] Command line

**Compile command:**
```bash
xelatex main.tex && xelatex main.tex
```

---

### Output Directory Structure

```
output/
├── main.tex
├── preamble.tex
├── frontmatter/
├── chapters/
└── backmatter/
```

**Actual output path:** _______________________________

---

*This record is created at the start of typesetting and referenced throughout. Any design change after initial generation must be recorded here with a reason.*
