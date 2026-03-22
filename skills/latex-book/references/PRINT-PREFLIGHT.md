# Print Preflight Checklist

Run this checklist after `latex-book` resolves all TX# issues and the document compiles cleanly. Every item must be confirmed before submitting the PDF to a printer or POD vendor.

Verify items against the compiled PDF, not the `.tex` source.

---

## 1. Compilation

| Item | Status | Notes |
|---|---|---|
| Document compiles without errors | | |
| Compiled twice (TOC and cross-references resolved) | | |
| Compile log contains zero `Overfull \hbox` warnings | | |
| Compile log contains no `Font shape ... not available` warnings | | |
| No `Undefined reference` warnings | | |
| No `Undefined citation` warnings | | |

---

## 2. Font Embedding

Run `pdffonts main.pdf` from the command line. Every row must show "yes" in the "emb" column.

| Item | Status | Notes |
|---|---|---|
| All body text fonts embedded | | |
| All heading fonts embedded | | |
| All fonts in included images/PDFs embedded | | |
| No "Type 3" fonts present (bitmapped — unacceptable for print) | | |

**Command:** `pdffonts main.pdf | grep -v "yes"` — any output (other than the header) indicates an unembedded font.

---

## 3. PDF/X Compliance

| Item | Status | Notes |
|---|---|---|
| PDF/X level confirmed (X-1a or X-3, per vendor requirement) | | Level: _______ |
| `pdfx` package loaded before `hyperref` in preamble | | |
| No transparency in the document (PDF/X-1a requirement) | | |
| No RGB color in a PDF/X-1a document | | |
| ICC color profile embedded (handled by `pdfx` package) | | |

**Verify PDF/X compliance:** Open in Adobe Acrobat → Tools → Print Production → Preflight → PDF/X profile. Or use Ghostscript: `gs -dPDFX -dBATCH -dNOPAUSE -sDEVICE=nullpage main.pdf`

---

## 4. Page Geometry

Verify by measuring the compiled PDF in a PDF viewer or Adobe Acrobat (File → Properties → Description).

| Item | Status | Notes |
|---|---|---|
| PDF page size matches stock size (trim + bleed if applicable) | | Expected: _______ × _______ in |
| Trim marks or bleed box correct (if bleed present) | | |
| Text does not extend into bleed area | | |
| Text does not extend within 0.125" of trim edge (safe zone) | | |
| Page numbers visible and within safe zone | | |
| Running heads visible and within safe zone | | |
| Inner margin sufficient — text not hidden in gutter | | |

---

## 5. Front Matter

| Item | Status | Notes |
|---|---|---|
| Half-title page present (if specified) | | |
| Title page: title, subtitle, author, publisher correct | | |
| Copyright page: year, holder, ISBN, legal language correct | | |
| Dedication present and correctly positioned (if specified) | | |
| Epigraph present and correctly attributed (if specified) | | |
| Table of contents present (if specified) | | |
| TOC page numbers match actual chapter start pages | | |
| TOC entries match chapter titles exactly | | |
| Front matter pages numbered in Roman numerals (i, ii, iii…) | | |
| Chapter 1 page numbered 1 in Arabic numerals | | |

---

## 6. Running Heads and Page Numbers

| Item | Status | Notes |
|---|---|---|
| Verso (left/even) pages: correct content in running head | | |
| Recto (right/odd) pages: correct content in running head | | |
| Running head case correct (mixed / all caps / small caps) | | |
| Page numbers in correct position (header outside corner / footer center / footer outside) | | |
| Chapter opening pages: no running head, page number only (or as specified) | | |
| Blank pages: no running head, no page number | | |
| Title page: no running head, no page number | | |
| Copyright page: no running head, no page number | | |

---

## 7. Chapter Structure

| Item | Status | Notes |
|---|---|---|
| All chapters present in correct order | | |
| Chapter titles match manuscript and TOC exactly | | |
| Chapters begin on recto (right/odd) pages (if `openright`) | | |
| Blank pages between chapters have no running head | | |
| Drop caps present on chapter openings (if specified) | | |
| Drop caps correctly sized and positioned | | |
| Section breaks rendered correctly (ornament / * * * / space) | | |
| No section breaks at the top or bottom of a page | | |

---

## 8. Typography Quality

| Item | Status | Notes |
|---|---|---|
| No widows (single line alone at top of page) | | |
| No orphans (single line alone at bottom of page) | | |
| No stranded headings (heading at bottom of page with < 2 lines following) | | |
| No more than 2–3 consecutive hyphenated lines anywhere | | |
| No hyphenated lines immediately before a page break | | |
| Paragraph spacing consistent throughout | | |
| No rivers of white space visible in justified text | | |
| Font rendering: no fake bold or fake italic visible | | |
| Ligatures rendering correctly (fi, fl, ff visible where expected) | | |
| Em dashes rendering as em dashes (not hyphens or en dashes) | | |
| Quotation marks rendering as curly quotes (not straight) | | |

---

## 9. Images and Figures

| Item | Status | Notes |
|---|---|---|
| All specified figures present | | |
| Figure numbers sequential | | |
| Captions match figures | | |
| No images stretched or incorrectly cropped | | |
| Raster images: minimum 300 DPI at print size | | |
| Line art: minimum 600 DPI or vector format | | |
| Image color mode matches document (grayscale / CMYK) | | |
| No pixelation visible at 100% zoom in PDF viewer | | |

---

## 10. Back Matter

| Item | Status | Notes |
|---|---|---|
| All back matter elements present in correct order | | |
| Appendix/appendices present and correctly labeled | | |
| Notes/bibliography formatted consistently | | |
| About the Author present (if specified) | | |
| Back matter page numbers continue correctly from main text | | |

---

## 11. Crop Marks and Submission Format

| Item | Status | Notes |
|---|---|---|
| **POD vendors (KDP, IngramSpark):** No crop marks in interior PDF | | |
| **Offset printer:** Crop marks present (or confirm vendor adds them) | | |
| PDF file size within vendor limits (KDP: 650 MB; IngramSpark: 2 GB) | | |
| PDF version acceptable to vendor (typically 1.3–1.7) | | |
| File named per vendor convention | | |

---

## 12. Vendor-Specific Requirements

### KDP (Kindle Direct Publishing — Print)
- Interior PDF/X-1a preferred; PDF 1.3–1.7 accepted
- No crop marks in interior PDF
- Cover and interior submitted as separate files
- B&W interior: grayscale PDF; Color interior: CMYK PDF
- Maximum file size: 650 MB

### IngramSpark
- Interior: PDF/X-1a required
- No crop marks in interior PDF
- Bleed: 0.125" on head, foot, and fore-edge (no bleed at spine)
- All fonts embedded
- Maximum file size: 2 GB
- File naming: use their template naming convention

### Offset Printer (general)
- Confirm PDF/X level with printer (usually PDF/X-1a or PDF/X-4)
- Confirm whether crop marks should be embedded or delivered as a bleed-only PDF
- CMYK color, all fonts embedded
- Request a "press proof" or "digital proof" before final run

---

## Sign-Off

| Final check | Status |
|---|---|
| All items above confirmed | |
| PDF opened and visually inspected at 100% zoom | |
| Representative pages checked: title, copyright, TOC, Ch. 1, mid-book, last page | |
| Vendor preflight tool run (if available) | |
| **File is ready to submit** | |
