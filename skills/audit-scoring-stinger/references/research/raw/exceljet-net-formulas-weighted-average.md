<!--
URL: https://exceljet.net/formulas/weighted-average
Fetch date: 2026-08-18
Source type: vendor/community blog
Research cluster: scoring-rubric-and-rollup
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# Weighted average, Excel formula | Exceljet
URL: https://exceljet.net/formulas/weighted-average
Published: 2015-11-28 (page continuously updated)
Author: Dave Bruns

## Summary

To calculate a weighted average, use a formula based on the SUMPRODUCT function and the SUM function. In the example shown, the formula in G5, copied down, is:

```
=SUMPRODUCT(weights,C5:E5)/SUM(weights)
```

where `weights` is the named range I5:K5. As the formula is copied down, it returns the weighted average seen in column G.

## Generic formula

```
=SUMPRODUCT(weights,values)/SUM(weights)
```

## Explanation

A weighted average (also called a weighted mean) is an average where some values are more important than others, i.e. some values have more "weight." It is calculated by multiplying the values to average by their corresponding weights, then dividing the sum of the results by the sum of the weights. In Excel this is represented by the generic formula above, where `weights` and `values` are cell ranges.

The core of this formula is the SUMPRODUCT function, which multiplies ranges or arrays together and returns the sum of products.

### Worked example

Scores for 3 tests appear in columns C through E, and weights appear in the named range `weights` (I5:K5). The formula in cell G5 is:

```
=SUMPRODUCT(weights,C5:E5)/SUM(weights)
```

SUMPRODUCT multiplies weights by corresponding scores and sums the result:

```
=SUMPRODUCT(weights,C5:E5) // returns 88.25
=SUMPRODUCT({0.25,0.25,0.5},{90,83,90})
=SUMPRODUCT({22.5,20.75,45})
=88.25
```

The result is then divided by the sum of the weights:

```
=88.25/SUM(weights)
=88.25/SUM({0.25,0.25,0.5})
=88.25/1
=88.25
```

Note: when calculating a weighted average, it is common to assign weights that add up to 1. When the weights do add up to 1, the divisor becomes 1 and has no effect on the result. However, it is not required that weights add up to 1, and the general form of the formula above handles either case.

As the formula is copied down column G, the named range `weights` (I5:K5) does not change, since it behaves like an absolute reference, while the scores in C5:E5, a relative reference, change with each new row.

### Weights that do not sum to 1

Weights don't need to add up to 1. For example, a weight of 1 for the first two tests and a weight of 2 for the final (since the final is twice as important) still produces the correct weighted average:

```
=SUMPRODUCT(weights,C5:E5)/SUM(weights)
=SUMPRODUCT({1,1,2},{90,83,90})/SUM(1,1,2)
=SUMPRODUCT({90,83,180})/SUM(1,1,2)
=353/4
=88.25
```

### Transposing weights

SUMPRODUCT requires array dimensions to be compatible: if the data is in a horizontal array, the weights should also be in a horizontal array, or SUMPRODUCT returns a #VALUE error. If weights are stored vertically, flip them with TRANSPOSE:

```
=SUMPRODUCT(TRANSPOSE(weights),C5:E5)/SUM(weights)
```

After TRANSPOSE runs, a vertical array `{0.25;0.25;0.5}` becomes a horizontal array `{0.25,0.25,0.5}` (semicolons indicate a vertical array, commas a horizontal one), and the formula solves the same way as the horizontal case.

## Related, named-range usage note

This source's canonical example builds the formula entirely around a named range (`weights`) rather than plain cell references, explicitly for readability and to keep the weights row acting like an absolute reference as the formula is copied down rows. This is a direct grounding for a named-range-driven scorecard design, distinct from the plain `$D$2:$H$2`-style absolute references used elsewhere in this research cluster's other sources.
