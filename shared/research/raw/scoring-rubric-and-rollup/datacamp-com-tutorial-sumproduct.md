<!--
URL: https://www.datacamp.com/tutorial/sumproduct
Fetch date: 2026-08-18
Source type: vendor/community blog
Research cluster: scoring-rubric-and-rollup
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# SUMPRODUCT() tutorial, DataCamp
URL: https://www.datacamp.com/tutorial/sumproduct

Before functions like SUMIF() and SUMIFS() existed, SUMPRODUCT() was one of Excel's primary tools for handling conditional logic: filtering data, applying multiple criteria, and calculating weighted results. Even today it handles scenarios newer functions struggle with, especially when multiple conditions, arrays, or calculations need to be evaluated together.

## Fundamental concepts and basic syntax

SUMPRODUCT() takes two or more ranges, multiplies their corresponding values, and sums the results into a single final value, combining calculation and aggregation into one formula and eliminating the need for helper columns.

Syntax: `SUMPRODUCT(array1, [array2], ...)`.

Rules:
- Each array must have the same number of rows and columns, since SUMPRODUCT() aligns items by position; a mismatched shape throws a #VALUE! error.
- Blank cells are treated as zeros.
- Text is ignored in calculations unless used in a logical expression.

## Default behavior: multiplication and summation

Example: `=SUMPRODUCT(A2:A4, B2:B4)` with Quantity in A and Price in B evaluates row by row (2x50=100, 3x30=90, 1x20=20) then sums to 210. This replaces helper columns that would otherwise compute row-level totals before summing.

## Advanced arithmetic and operator usage

SUMPRODUCT() can evaluate full arithmetic expressions (addition, subtraction, division) row by row before summing. Example, total revenue minus discounts:

```
=SUMPRODUCT((B2:B6*C2:C6)-E2:E6)
```

When arrays are separated by commas, each is treated as an independent input and SUMPRODUCT() multiplies corresponding elements across arrays before summing.

## Conditional calculations and logical criteria (the N/A-aware pattern)

SUMPRODUCT() can evaluate logical conditions directly inside a formula. A logical test like `D2:D6="Fruit"` produces an array of TRUE/FALSE values, which are NOT automatically usable in arithmetic. Attempting `=SUMPRODUCT((D2:D6="Fruit"), B2:B6)` directly returns 0, because logical values must first be converted to numbers.

The double-unary operator `--` performs that conversion, turning `{TRUE,TRUE,FALSE,TRUE,FALSE}` into `{1,1,0,1,0}`:

```
=SUMPRODUCT(--(D2:D6="Fruit"), B2:B6)
```

Only rows marked with 1 are included in the calculation; rows where the condition is FALSE contribute zero. This is the general mechanism for making SUMPRODUCT ignore/exclude specific rows (e.g. a criterion marked N/A or Not Applicable) from a weighted computation: build a boolean array testing for "included" status, convert it to 1/0 with `--`, and multiply it into the SUMPRODUCT alongside the value and weight arrays.

## Handling multiple criteria (AND/OR logic)

AND logic: multiply conditions together, since only 1x1 equals 1, so a row is included only when every condition evaluates to TRUE:

```
=SUMPRODUCT(--(A2:A10>50)*--(B2:B10<100)*C2:C10)
```

Equivalently, comma-separated arrays are also multiplied together by default:

```
=SUMPRODUCT(--(A2:A10>50), --(B2:B10<100), C2:C10)
```

## Direct applicability to N/A-aware weighted rollups

Combining the weighted-average pattern (`SUMPRODUCT(values,weights)/SUM(weights)`, documented in the companion Exceljet/Microsoft sources in this cluster) with this conditional-inclusion pattern gives the general N/A-aware weighted formula shape:

```
=SUMPRODUCT(--(applicable_range<>"N/A"), value_range, weight_range) / SUMPRODUCT(--(applicable_range<>"N/A"), weight_range)
```

Both the numerator and the denominator must apply the same inclusion mask, otherwise a criterion marked N/A would still contribute its weight to the denominator while contributing zero to the numerator, silently dragging the average down rather than being excluded. This dual-masking requirement is not explicitly spelled out by this source (which covers the masking mechanism but not this specific rollup-correctness pitfall), so it is flagged here as an inference built from this source's documented mechanism rather than a directly quoted claim.
