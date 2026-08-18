<!--
URL: https://python-excel-automation.com/automating-reporting-workflows/generating-excel-reports-from-templates/
Fetch date: 2026-08-18
Source type: vendor/community blog
Research cluster: scoring-rubric-and-rollup
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# Generate Excel Reports from Templates, Python Excel Automation
URL: https://python-excel-automation.com/automating-reporting-workflows/generating-excel-reports-from-templates/
Published: 2026-06-18

The report generation stage has two strategies: build a workbook from scratch every run, or take a workbook someone already designed (logo, brand colors, formulas, print areas, a tuned page layout) and inject only the numbers that change. This guide covers the second strategy, template injection: faster to write, produces output stakeholders recognize, and keeps formatting decisions with the person who made the template rather than in Python code.

## Why template injection beats building from scratch

A finance team's quarterly report template encodes a lot of work: merged title banners, a corporate color palette, conditional formatting rules, a SUM formula over the data range, a frozen header, a print area fit to one page. Rebuilding all of that in code is brittle, since every later styling tweak has to be re-translated into Python and the two copies drift.

Template injection inverts the relationship: the .xlsx is the source of truth for appearance, the script is responsible only for data. Core pattern, three steps:

1. Load the prepared template with openpyxl's `load_workbook()`.
2. Write values into the specific cells that hold data, leaving everything else untouched.
3. Save the result as a new, dated file, never overwriting the template.

## Building a reusable template in code

```python
from openpyxl import Workbook
from openpyxl.styles import Font, PatternFill, Alignment

wb = Workbook()
ws = wb.active
ws.title = "Report"

# Title banner
ws["A1"] = "Regional Sales Report"
ws["A1"].font = Font(size=16, bold=True, color="1F4E78")
ws.merge_cells("A1:C1")

# Report-date cell
ws["A2"] = "Report date:"
ws["A2"].font = Font(italic=True)

# Styled header row at row 4
headers = ["Region", "Units", "Revenue"]
header_fill = PatternFill("solid", fgColor="4472C4")
for col, name in enumerate(headers, start=1):
    cell = ws.cell(row=4, column=col, value=name)
    cell.font = Font(bold=True, color="FFFFFF")
    cell.fill = header_fill
    cell.alignment = Alignment(horizontal="center")

# Totals row with a live formula
ws["A10"] = "Total"
ws["A10"].font = Font(bold=True)
ws["C10"] = "=SUM(C5:C9)"
ws["C10"].number_format = "#,##0.00"

wb.save("report_template.xlsx")
```

## The core pattern: load, write data cells, save a dated copy

```python
from datetime import date
from openpyxl import load_workbook

template = "report_template.xlsx"
wb = load_workbook(template)
ws = wb["Report"]

ws["B2"] = date.today().isoformat()

out = f"sales_report_{date.today():%Y%m%d}.xlsx"
wb.save(out)
```

The dated filename gives an audit trail, prevents one run from clobbering the previous one, and lets the same script run unattended on a schedule, each run writing its own distinct file instead of racing the last one. Treat the template file as read-only, version-controlled input.

## Filling a table region from a DataFrame

```python
from datetime import date
import pandas as pd
from openpyxl import load_workbook

data = pd.DataFrame({
    "region": ["North", "South", "West"],
    "units": [120, 95, 143],
    "revenue": [15990.00, 12047.50, 18744.25],
})

wb = load_workbook("report_template.xlsx")
ws = wb["Report"]
ws["B2"] = date.today().isoformat()

START_ROW = 5
for offset, record in enumerate(data.itertuples(index=False)):
    r = START_ROW + offset
    ws.cell(row=r, column=1, value=record.region)
    ws.cell(row=r, column=2, value=record.units)
    ws.cell(row=r, column=3, value=record.revenue)

out = f"sales_report_{date.today():%Y%m%d}.xlsx"
wb.save(out)
```

## Keep formulas intact: write values, not over formulas

Cell C10 holds `=SUM(C5:C9)`. Never write to it directly; write the data it sums and let Excel recalculate when the file opens. The rule: write only to cells that hold data, never to cells that hold formulas. openpyxl does not evaluate formulas, it stores the formula string and Excel computes the result on open. If a computed value is needed inside Python (rare for templates), reload with `load_workbook(path, data_only=True)`, but that returns the last value Excel cached, which is `None` for a file never opened in Excel.

## What survives an openpyxl write versus a pandas write

Cell styles, column widths, conditional formatting, and named ranges survive an openpyxl write. Images, charts, and data validation survive an openpyxl write but not a pandas rewrite of the sheet. `pandas.to_excel` targeting an existing sheet replaces the sheet contents wholesale, discarding the title banner, header fill, merged cells, totals formula, and print area. `pandas.to_excel` is explicitly called out as "the wrong tool" for the final write step when a branded template must be preserved.

## Extending a template's row range

If data fills more rows than the template's formula range covers, the formula must be extended manually or computed in code from the row count; e.g. if data now spans rows 5 to 12 but the totals formula only sums C5:C9, it must be updated to `ws["C13"] = "=SUM(C5:C12)"`. Clearing values (setting to `None`) rather than deleting rows is the safer pattern for a template's unused rows, since `delete_rows` would also remove the template's formatting and any conditional rules attached to those rows.

## Excel's own template format

Excel has a dedicated template format (.xltx, .xltm for macro-enabled templates); double-clicking an .xltx opens a copy rather than the original, giving the same no-overwrite behavior by convention rather than by script discipline. openpyxl can `load_workbook()` an .xltx directly; output should still be saved as .xlsx.
