<!--
URL: https://openpyxl.readthedocs.io/en/stable/formatting.html
Fetch date: 2026-08-18
Source type: official docs
Research cluster: scoring-rubric-and-rollup
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# Conditional Formatting, openpyxl 3.1.3 documentation
URL: https://openpyxl.readthedocs.io/en/stable/formatting.html

Excel supports three different types of conditional formatting: builtins, standard, and custom. Builtins combine specific rules with predefined styles. Standard conditional formats combine specific rules with custom formatting. It is also possible to define custom formulae for applying custom formats using differential styles.

Note: the syntax for the different rules varies so much that openpyxl cannot know whether a rule makes logical sense; it only writes the XML.

## Basic rule syntax

```python
from openpyxl.formatting import Rule
from openpyxl.styles import Font, PatternFill, Border
from openpyxl.styles.differential import DifferentialStyle

dxf = DifferentialStyle(font=Font(bold=True), fill=PatternFill(start_color='EE1111', end_color='EE1111'))
rule = Rule(type='cellIs', dxf=dxf, formula=["10"])
```

Because some rule signatures are verbose, openpyxl provides convenience factory functions (`ColorScaleRule`, `IconSetRule`, `DataBarRule`, `CellIsRule`, `FormulaRule`).

## Builtin formats

The builtin conditional formats are ColorScale, IconSet, DataBar. They combine a type ('num', 'percent', 'max', 'min', 'formula', 'percentile') with a comparison value.

### ColorScale

2-color or 3-color gradients:

```python
from openpyxl.formatting.rule import ColorScaleRule
rule = ColorScaleRule(start_type='percentile', start_value=10, start_color='FFAA0000',
    mid_type='percentile', mid_value=50, mid_color='FF0000AA',
    end_type='percentile', end_value=90, end_color='FF00AA00')
```

### IconSet

Choose from a fixed icon library: '3Arrows', '3ArrowsGray', '3Flags', '3TrafficLights1', '3TrafficLights2', '3Signs', '3Symbols', '3Symbols2', '4Arrows', '4ArrowsGray', '4RedToBlack', '4Rating', '4TrafficLights', '5Arrows', '5ArrowsGray', '5Rating', '5Quarters'.

```python
from openpyxl.formatting.rule import IconSetRule
rule = IconSetRule('5Arrows', 'percent', [10, 20, 30, 40, 50], showValue=None, percent=None, reverse=None)
```

### DataBar

openpyxl supports DataBars as defined in the original specification (borders and directions were added in a later spec extension, support for which is more limited):

```python
from openpyxl.formatting.rule import DataBarRule
rule = DataBarRule(start_type='percentile', start_value=10, end_type='percentile', end_value='90',
    color="FF638EC6", showValue="None", minLength=None, maxLength=None)
```

## Standard conditional formats

The standard conditional formats are Average, Percent, Unique or duplicate, Value, Rank. Example combining several rule types on one worksheet:

```python
from openpyxl import Workbook
from openpyxl.styles import Color, PatternFill, Font, Border
from openpyxl.styles.differential import DifferentialStyle
from openpyxl.formatting.rule import ColorScaleRule, CellIsRule, FormulaRule

wb = Workbook()
ws = wb.active

redFill = PatternFill(start_color='EE1111', end_color='EE1111', fill_type='solid')

# Two-color scale
ws.conditional_formatting.add('A1:A10',
    ColorScaleRule(start_type='min', start_color='AA0000', end_type='max', end_color='00AA00'))

# Three-color scale
ws.conditional_formatting.add('B1:B10',
    ColorScaleRule(start_type='percentile', start_value=10, start_color='AA0000',
        mid_type='percentile', mid_value=50, mid_color='0000AA',
        end_type='percentile', end_value=90, end_color='00AA00'))

# Format if cell is less than a formula/cell reference
ws.conditional_formatting.add('C2:C10',
    CellIsRule(operator='lessThan', formula=['C$1'], stopIfTrue=True, fill=redFill))

# Format if cell value is between two values
ws.conditional_formatting.add('D2:D10',
    CellIsRule(operator='between', formula=['1','5'], stopIfTrue=True, fill=redFill))

# Format using an arbitrary formula
ws.conditional_formatting.add('E1:E10',
    FormulaRule(formula=['ISBLANK(E1)'], stopIfTrue=True, fill=redFill))
```

This documents the exact API shapes (`ColorScaleRule`, `CellIsRule`, `FormulaRule`, `IconSetRule`, `DataBarRule`) that a Python-generated branded XLSX scoring report would use to visually flag rollup scores (e.g. red/yellow/green color scale on a final weighted score column, or a formula-driven rule flagging N/A-excluded rows).
