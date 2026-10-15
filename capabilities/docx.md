# Capability: Word documents (.docx)

Use when the deliverable is a Word file, or an existing .docx must be read or edited.

## Create (Python, python-docx)

```python
from docx import Document
from docx.shared import Pt, Inches
from docx.enum.text import WD_ALIGN_PARAGRAPH

doc = Document()
st = doc.styles["Normal"]; st.font.name = "Calibri"; st.font.size = Pt(11)
for s in doc.sections:
    s.left_margin = s.right_margin = Inches(1)

doc.add_heading("Title", level=0)
doc.add_heading("Section", level=1)
p = doc.add_paragraph("Body text. ")
p.add_run("Bold part").bold = True
doc.add_paragraph("Item", style="List Bullet")

t = doc.add_table(rows=1, cols=3); t.style = "Light Grid Accent 1"
for c, h in zip(t.rows[0].cells, ["A", "B", "C"]): c.text = h
row = t.add_row().cells; row[0].text, row[1].text, row[2].text = "1", "2", "3"

doc.add_picture("chart.png", width=Inches(5.5))
doc.save("out.docx")
```

## Edit an existing file

- Open with `Document(path)`, change text at the run level to keep formatting.
  Replacing `paragraph.text` wipes run formatting; edit `run.text` instead.
- Work on a copy; never overwrite the original upload.
- Tracked changes, comments, and complex fields are not exposed by python-docx.
  For those, unzip the .docx, edit `word/document.xml` carefully, re-zip, and
  confirm the file still opens.
- Search and replace across runs: a phrase may be split over several runs.
  Join, replace, then write back to the first run and blank the rest.

## Read

- Text: iterate `doc.paragraphs`; tables via `doc.tables`.
- Quick text dump of any docx: `pandoc in.docx -t markdown`.

## Structure rules

- Use real heading styles (Heading 1/2/3), not bold text, so navigation and
  tables of contents work.
- Real lists via list styles, never typed bullets or hyphens.
- Page numbers and headers go in the section header/footer.
- Keep fonts to one family, two at most.

## Check before delivering

```bash
soffice --headless --convert-to pdf out.docx
pdftoppm -png -r 70 out.pdf page
```

Look at every page image: overflowing tables, orphaned headings, broken images.
