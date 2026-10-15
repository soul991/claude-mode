# Capability: PDFs

Use for reading, creating, merging, splitting, filling, or OCR-ing PDFs.

## Read and inspect

- Text: `pdftotext -layout in.pdf -` or pypdf `PdfReader(p).pages[i].extract_text()`.
- Tables: `pdfplumber.open(p).pages[i].extract_tables()`.
- Visual check of any page: `pdftoppm -png -r 80 -f 3 -l 3 in.pdf pg` then look at it.
- Scanned PDF (no selectable text): OCR.

```bash
pdftoppm -png -r 300 scan.pdf s
for f in s-*.png; do tesseract "$f" "${f%.png}" ; done
```

Pick the strategy by document type: text-heavy (extract text), scanned (OCR),
slide-like (rasterise and look), forms (read fields), data-heavy (tables).
Do an inventory first: page count, whether text is selectable, embedded images.

## Merge, split, rotate, encrypt (pypdf)

```python
from pypdf import PdfReader, PdfWriter
w = PdfWriter()
for p in ["a.pdf", "b.pdf"]:
    for page in PdfReader(p).pages: w.add_page(page)
w.write("merged.pdf")

r = PdfReader("merged.pdf"); w = PdfWriter()
for i in range(0, 3): w.add_page(r.pages[i])       # split: first 3 pages
w.write("part1.pdf")

page = PdfReader("a.pdf").pages[0]; page.rotate(90)   # rotate
w.encrypt("userpass")                                  # encrypt before writing
```

## Create

- From Markdown/HTML: `pandoc in.md -o out.pdf` or render HTML via a headless browser.
- Programmatic: reportlab (`canvas.Canvas`, or `platypus` for flowing text and tables).
- Use real fonts with embedded glyphs for non-Latin text; test the output.

## Fill forms

```python
r = PdfReader("form.pdf"); print(r.get_fields().keys())
w = PdfWriter(); w.append(r)
w.update_page_form_field_values(w.pages[0], {"Name": "A. Person"}, auto_regenerate=False)
w.set_need_appearances_writer(True)
w.write("filled.pdf")
```

Re-open the filled file and read the fields back to confirm the values stuck.
Flat (non-fillable) forms: overlay text with reportlab at measured coordinates.

## Watermark, redact, compress

- Watermark: build a one-page PDF with reportlab, then `page.merge_page(mark)`.
- Redaction must remove content, not paint over it. Verify that the text is gone
  by extracting it again. Never claim redaction without that check.
- Compress: `qpdf --object-streams=generate in.pdf out.pdf` or ghostscript.

## Always

Work on copies. Check page count and open the result before delivering.
