# Capability: presentations (.pptx)

Use when the deliverable is a slide deck, or a .pptx must be read or edited.

## Content first

1. Write the storyline as a list of slide headlines. Each headline is a full
   sentence stating the takeaway ("Churn fell 18% after the pricing change"),
   not a topic ("Churn").
2. One idea per slide. Cut anything that does not support the headline.
3. Details go in speaker notes.

## Create (Python, python-pptx)

```python
from pptx import Presentation
from pptx.util import Inches, Pt
from pptx.dml.color import RGBColor

prs = Presentation()
prs.slide_width, prs.slide_height = Inches(13.333), Inches(7.5)   # 16:9
blank = prs.slide_layouts[6]

s = prs.slides.add_slide(blank)
tb = s.shapes.add_textbox(Inches(0.7), Inches(0.5), Inches(11.9), Inches(1.2))
tf = tb.text_frame; tf.word_wrap = True
tf.text = "Churn fell 18% after the pricing change"
tf.paragraphs[0].runs[0].font.size = Pt(34)
tf.paragraphs[0].runs[0].font.bold = True

s.shapes.add_picture("chart.png", Inches(0.7), Inches(1.9), width=Inches(8))
s.notes_slide.notes_text_frame.text = "Speaker notes here."
prs.save("deck.pptx")
```

Native charts: `from pptx.chart.data import CategoryChartData`, then
`shapes.add_chart(XL_CHART_TYPE.COLUMN_CLUSTERED, x, y, cx, cy, data)`.

## Design rules

- Large type: titles 30-40pt, body at least 18pt.
- Three colours at most (one accent), one font family, consistent margins.
- Align to a grid; same title position on every slide.
- Prefer a chart or diagram to a table, and a table to a paragraph.
- High contrast; never put text on a busy image without an overlay.
- Do not use stock phrases as filler ("Thank you", "Questions?") unless asked.

## Edit an existing deck

- Open, change text at run level to preserve formatting, save as a new file.
- Respect the template's layouts and theme; do not restyle unless asked.
- Reorder or delete slides by manipulating `prs.slides._sldIdLst`.

## Check before delivering

```bash
soffice --headless --convert-to pdf deck.pptx
pdftoppm -png -r 50 deck.pdf slide
```

Look at every slide image for overflow, overlap, tiny text, and misalignment.
