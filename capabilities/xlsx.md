# Capability: spreadsheets (.xlsx, .csv)

Use when the deliverable is a spreadsheet, or tabular data must be cleaned,
analysed, or converted.

## Create (Python, openpyxl)

```python
from openpyxl import Workbook
from openpyxl.styles import Font, PatternFill, Alignment
from openpyxl.utils import get_column_letter

wb = Workbook(); ws = wb.active; ws.title = "Data"
ws.append(["Item", "Qty", "Price", "Total"])
for i, (n, q, p) in enumerate([("A", 2, 9.5), ("B", 5, 3.2)], start=2):
    ws.append([n, q, p, f"=B{i}*C{i}"])          # formulas, not pasted values
ws["A7"], ws["D7"] = "Sum", "=SUM(D2:D3)"

for c in ws[1]:
    c.font = Font(bold=True, color="FFFFFF")
    c.fill = PatternFill("solid", fgColor="1F3A5F")
    c.alignment = Alignment(horizontal="center")
ws.freeze_panes = "A2"
for col in range(1, 5):
    ws.column_dimensions[get_column_letter(col)].width = 14
for r in ws.iter_rows(min_row=2, min_col=3, max_col=4):
    for c in r: c.number_format = "#,##0.00"
wb.save("out.xlsx")
```

## Rules

- Derived values are formulas. Hard-code only true inputs, and put inputs in
  clearly labelled cells (an Inputs sheet for models).
- Separate inputs, calculations, outputs.
- Consistent formats: dates as dates, money with a currency format, percentages as %.
- Freeze headers, set widths, no merged cells inside data tables.
- Use absolute references (`$B$1`) for constants copied down a column.

## Formulas are not calculated by openpyxl

Recalculate and check for errors before you claim the numbers are right:

```bash
soffice --headless --convert-to xlsx --outdir recalced out.xlsx
python -c "
from openpyxl import load_workbook
ws = load_workbook('recalced/out.xlsx', data_only=True).active
bad = [c.coordinate for r in ws.iter_rows() for c in r
       if isinstance(c.value, str) and c.value.startswith('#')]
print('errors:', bad)"
```

## Cleaning messy data (pandas)

- `pd.read_csv(path, dtype=str)` first, then convert columns deliberately.
- Report: row count, null counts per column, duplicate rows, odd values.
- Trim whitespace, normalise case and dates, drop only what you can justify,
  and say what you dropped and how many rows.
- Keep the raw file untouched; write cleaned output to a new file.

## Charts in a workbook

`from openpyxl.chart import BarChart, LineChart, Reference`; add to the sheet,
label axes and title. Verify visually via the soffice render.
