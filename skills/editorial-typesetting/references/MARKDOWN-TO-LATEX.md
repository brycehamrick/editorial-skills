# Markdown to LaTeX Conversion Reference

Complete conversion table for transforming copy-edited markdown chapters into LaTeX source files. Used during Phase 1 of the typesetting stage when converting each `.md` chapter file to a `.tex` file.

All conversions assume the `memoir` class with XeLaTeX compilation.

---

## Document Structure

| Markdown | LaTeX | Notes |
|---|---|---|
| `# Chapter Title` | `\chapter{Chapter Title}` | One per file; omit `#` from chapter files — handle in `main.tex` via `\include` |
| `## Section` | `\section{Section}` | |
| `### Subsection` | `\subsection{Subsection}` | |
| `#### Sub-subsection` | `\subsubsection{Sub-subsection}` | Use sparingly |
| Unnumbered chapter (Preface, etc.) | `\chapter*{Preface}` | Asterisk suppresses numbering |
| Unnumbered section | `\section*{Section}` | |

---

## Inline Formatting

| Markdown | LaTeX | Notes |
|---|---|---|
| `**bold**` | `\textbf{bold}` | |
| `*italic*` or `_italic_` | `\textit{italic}` | |
| `***bold italic***` | `\textbf{\textit{bold italic}}` | |
| `` `code` `` | `\texttt{code}` | Or `\verb\|code\|` for inline code |
| `~~strikethrough~~` | `\sout{strikethrough}` | Requires `ulem` package |
| `^superscript^` | `\textsuperscript{superscript}` | |
| `~subscript~` | `\textsubscript{subscript}` | |

---

## Quotation Marks and Special Characters

Markdown typically uses straight or "smart" quotes. LaTeX requires specific encoding.

| Character | LaTeX | Notes |
|---|---|---|
| Opening double quote `"` | ` `` ` (two backticks) | Or use `\enquote{}` with `csquotes` |
| Closing double quote `"` | `''` (two apostrophes) | |
| Opening single quote `'` | `` ` `` (one backtick) | |
| Closing single quote `'` | `'` | |
| Em dash `—` or `---` | `---` | memoir handles correctly |
| En dash `–` or `--` | `--` | |
| Ellipsis `…` | `\ldots{}` | Or Unicode `…` with XeLaTeX |
| Ampersand `&` | `\&` | Raw `&` is a LaTeX command |
| Percent `%` | `\%` | Raw `%` begins a comment |
| Dollar sign `$` | `\$` | Raw `$` enters math mode |
| Hash `#` | `\#` | |
| Underscore `_` | `\_` | Outside math mode |
| Backslash `\` | `\textbackslash{}` | |
| Tilde `~` | `\textasciitilde{}` | |
| Caret `^` | `\textasciicircum{}` | |
| Left/right curly braces | `\{` `\}` | |

**Recommended:** Add `\usepackage{csquotes}` to the preamble and use `\enquote{text}` for all quotations. This automatically produces the correct quote style for the document language.

---

## Block Elements

### Paragraphs

Blank line between paragraphs in markdown → blank line between paragraphs in LaTeX (memoir handles indentation automatically based on `\parindent` and `\parskip` settings).

**First paragraph after a heading:** memoir suppresses indentation on the first paragraph after a heading by default (correct behavior). Do not add `\noindent` manually.

### Block Quotes

```
> This is a blockquote that spans
> multiple lines.
```

Becomes:

```latex
\begin{quote}
This is a blockquote that spans multiple lines.
\end{quote}
```

For longer extracts (epigraphs within the text, extended quotations):

```latex
\begin{quotation}
Long quotation with paragraph indentation for internal paragraphs.
\end{quotation}
```

### Code Blocks

````
```
code block content
```
````

Becomes:

```latex
\begin{verbatim}
code block content
\end{verbatim}
```

For syntax-highlighted code: add `\usepackage{listings}` or `\usepackage{minted}` to the preamble.

---

## Lists

### Unordered Lists

```markdown
- First item
- Second item
  - Nested item
```

```latex
\begin{itemize}
  \item First item
  \item Second item
  \begin{itemize}
    \item Nested item
  \end{itemize}
\end{itemize}
```

### Ordered Lists

```markdown
1. First item
2. Second item
```

```latex
\begin{enumerate}
  \item First item
  \item Second item
\end{enumerate}
```

### Definition Lists (if used)

No native markdown equivalent; use description environment:

```latex
\begin{description}
  \item[Term] Definition of term
\end{description}
```

---

## Section Breaks

A horizontal rule in markdown (`---` on its own line, or `* * *`) used as a section break becomes the custom `\sectionbreak` command defined in the preamble:

```latex
\sectionbreak
```

**Important:** The `---` horizontal rule must be distinguished from the YAML front matter delimiter and the em dash. Context determines which it is:
- At the top of a markdown file: YAML front matter — strip it
- Inline in a sentence: em dash → `---`
- On its own line between paragraphs: section break → `\sectionbreak`

---

## Hyperlinks

```markdown
[link text](https://example.com)
```

```latex
\href{https://example.com}{link text}
```

Requires `\usepackage[hidelinks]{hyperref}` in the preamble.

For bare URLs:

```markdown
https://example.com
```

```latex
\url{https://example.com}
```

---

## Images and Figures

```markdown
![Alt text](path/to/image.png)
```

```latex
\begin{figure}[htbp]
  \centering
  \includegraphics[width=0.85\linewidth]{path/to/image}
  \caption{Alt text}
  \label{fig:descriptive-label}
\end{figure}
```

Notes:
- Omit the file extension in `\includegraphics` — XeLaTeX will find `.png`, `.jpg`, `.pdf`
- Adjust `width` to `\linewidth`, `0.85\linewidth`, or a fixed dimension
- Add `\usepackage{graphicx}` to preamble
- For images without captions (decorative): use `\includegraphics` directly without the `figure` environment

---

## Tables

Markdown tables require significant manual conversion. Each pipe-delimited table becomes a `tabular` or `longtable` environment.

Simple markdown table:
```markdown
| Column A | Column B | Column C |
|---|---|---|
| Data 1 | Data 2 | Data 3 |
```

LaTeX equivalent:
```latex
\begin{table}[htbp]
  \centering
  \caption{Table caption here}
  \label{tab:descriptive-label}
  \begin{tabular}{lll}
    \toprule
    Column A & Column B & Column C \\
    \midrule
    Data 1 & Data 2 & Data 3 \\
    \bottomrule
  \end{tabular}
\end{table}
```

Add `\usepackage{booktabs}` to the preamble for professional `\toprule`, `\midrule`, `\bottomrule` rules.

For tables that span multiple pages, use `longtable` instead of `tabular`.

Column alignment codes: `l` (left), `c` (center), `r` (right), `p{<width>}` (fixed-width, wraps text).

---

## Footnotes

```markdown
Text with a footnote.[^1]

[^1]: The footnote content here.
```

```latex
Text with a footnote.\footnote{The footnote content here.}
```

Notes:
- In LaTeX, the footnote content is placed inline at the point of reference, not collected at the bottom
- memoir handles footnote layout automatically
- Footnotes in headings: use `\protect\footnote{...}` or move to a `\thanks{}` command on the title page

---

## Drop Caps (Chapter Openings)

When drop caps are enabled, the first paragraph of each chapter must be manually converted:

Markdown:
```
The opening paragraph of the chapter begins here with the first word.
```

LaTeX:
```latex
\lettrine[lines=3, lraise=0.1]{T}{he} opening paragraph of the chapter begins here with the first word.
```

Rules:
- The first argument `{T}` is the drop cap letter (uppercase)
- The second argument `{he}` is the remainder of the first word (without the drop cap letter)
- Apply only to the first paragraph of each chapter — not to chapters that begin with a quote or epigraph (handle those separately: place the opening quote in a `\begin{quote}` block, then begin the text paragraph with the drop cap)

---

## YAML Front Matter

Markdown files often begin with YAML front matter (title, author, date metadata). Strip this entirely during conversion — the LaTeX document structure handles all metadata in the preamble and title page.

```markdown
---
title: Chapter One
author: Author Name
---
```

→ Strip. The chapter title comes from `\chapter{Chapter One}` in the LaTeX file.

---

## Special Cases and Edge Cases

| Situation | Handling |
|---|---|
| Smart quotes already in markdown | Verify encoding; convert to ` `` ` and `''` or use `\enquote{}` |
| Non-breaking space (` `) | Use `~` in LaTeX (e.g., `Figure~\ref{fig:label}`) |
| Diacritics (é, ü, ñ) | XeLaTeX handles Unicode natively — leave as-is |
| Mathematical expressions | Wrap in `$...$` (inline) or `\[...\]` (display) |
| Chapter epigraphs | Use memoir's `\epigraph{text}{attribution}` command |
| Verse / poetry | Use `verse` environment: `\begin{verse}...\end{verse}` |
| Callout boxes / sidebars | Use memoir's `\sidebar{}` or a `framed` environment with `\usepackage{framed}` |
| Dialogue with em dashes | Em dashes in prose: `---` works correctly in XeLaTeX |
| Section not to appear in TOC | `\section*{Title}` — asterisk suppresses TOC entry and numbering |
| Long URL that breaks badly | Wrap in `\url{}` — `hyperref` handles line breaking of URLs |

---

## Preamble Packages Summary

Packages required based on content types used:

| Package | When to include |
|---|---|
| `fontspec` | Always (XeLaTeX font selection) |
| `microtype` | Always (microtypography) |
| `hyperref` | Always (PDF metadata, links) |
| `graphicx` | When images are present |
| `booktabs` | When tables are present |
| `csquotes` | Recommended always (smart quotation handling) |
| `lettrine` | When drop caps are enabled |
| `longtable` | When multi-page tables are present |
| `ulem` | When strikethrough is used |
| `listings` or `minted` | When syntax-highlighted code blocks are present |
| `framed` or `tcolorbox` | When callout boxes are present |
| `textcase` | When all-caps running heads are needed |
