<!--
URL: https://portfoliohub.io/blog/project-prioritization-template
Fetch date: 2026-08-18
Source type: vendor/community blog
Research cluster: scoring-rubric-and-rollup
Archived by: forge stage 2 sweep round 2 (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., covering the 8 pairs left uncovered by round 1.
-->

# Project Prioritization Template for Excel and Sheets | Portfolio Hub
URL: https://portfoliohub.io/blog/project-prioritization-template
Published: 2026-07-18

Project Prioritization Template for Excel and Sheets | Portfolio Hub

# Project Prioritization Template for Excel and Sheets

The template is fifteen minutes of work. Agreeing the weights before anyone sees a score is the part that takes a fortnight, and it is the part that makes the numbers stick.

 By Elena Marsh, PMO lead and portfolio strategist · July 18, 2026 · 8 min read 

A project prioritization template is a spreadsheet that scores every candidate project against agreed weighted criteria and sorts the result into a ranked list. Nine columns is enough. The build takes fifteen minutes; the work that makes it credible is agreeing the criteria and their weights with the people who will later dispute the ranking, and doing that before anyone has seen a single score.

This page is the artifact. For the reasoning behind the criteria and how to choose between scoring approaches, start with project prioritization criteria and project prioritization frameworks, then come back and build the sheet.

#### Key takeaways

- Five criteria, maximum. Every extra criterion pulls the scores toward the middle until the ranking stops separating anything.
- Weights must be agreed and locked before scoring starts. Weights set after the scores are visible are negotiation, not prioritization.
- Score 1 to 5 with a written anchor for each value, so a 4 means the same thing to two different scorers.
- Add a cost or effort column and a running total, then draw the capacity line. Without it you have a ranked wish list, not a portfolio.
- SUMPRODUCT does the whole weighted calculation in one formula and survives someone reordering the criteria.
- Keep the projects that fell below the line visible. Deleting them is how the same request comes back in six weeks with a new name.

Last updated July 2026.

## The columns a project prioritization template needs

Start with these. One row per candidate project, one tab, no merged cells.

| Column | Format | Why it earns a column |
| --- | --- | --- |
| ID | P-01, P-02 | So a project can be referenced in a meeting without ambiguity, and never reused. |
| Project name | Short text | Six words. Long names hide what the work actually is. |
| Sponsor | A person | Never a department. A row without a named sponsor should not be scored at all. |
| Criterion 1 to 5 | 1 to 5 score | One column per agreed criterion, with the weight in the header row. |
| Weighted score | Formula | The single number the ranking sorts on. |
| Cost or effort | Dollars or person-weeks | Turns a ranked list into a portfolio you can afford. |
| Cumulative cost | Formula | Running total down the ranked list. Where it crosses the budget is the line. |
| Rank | Formula | Calculated, never typed, so nobody can nudge it. |
| Decision | Approved / Deferred / Declined | Three values. The audit trail for why a project is not running. |

Resist the urge to add a comments column that becomes a novel. Add a separate notes tab keyed by project ID if the discussion needs recording.

## Choosing the criteria and their weights

Five criteria covering value, cost, risk, strategic fit, and urgency will separate almost any portfolio. Weights should reflect what the organization says it cares about, and they should be argued about in a room, once, and then written into the header row where everyone can see them.

| Criterion | Typical weight | What a 5 means | What a 1 means |
| --- | --- | --- | --- |
| Strategic fit | 30% | Directly advances a named strategic objective this year. | No stated link to any objective. |
| Financial value | 25% | Quantified benefit, validated by finance, landing inside 12 months. | Benefit is asserted and unquantified. |
| Urgency or cost of delay | 20% | Value falls sharply if this slips a quarter, or a deadline is external. | Nothing changes if it starts next year. |
| Risk if not done | 15% | Regulatory, security, or a system already failing. | Nice to have, no consequence. |
| Delivery confidence | 10% | Scope is clear, the team exists, similar work has been delivered before. | Scope is vague and the skills are not in house. |

Write the anchors for every score value, not just 5 and 1. The middle values are where scoring drifts, and a three-word definition of what a 3 looks like removes most of the argument later. Two people scoring the same project independently and landing within one point is the test that your anchors work.

## The exact Excel and Google Sheets formulas

Assume criterion scores sit in columns D through H, and the weights sit in row 2 of those same columns as decimals (0.30, 0.25, 0.20, 0.15, 0.10). Data starts in row 4.

- Weighted score, in I4: `=SUMPRODUCT($D$2:$H$2,D4:H4)`. Fill down. This returns a number between 1 and 5 and keeps working if you reorder the criteria.
- Rank, in L4: `=RANK(I4,$I$4:$I$40)`. Highest weighted score ranks 1.
- Cumulative cost down the ranked list, in K4: `=SUMIFS($J$4:$J$40,$L$4:$L$40,"<="&L4)`. This sums the cost of every project ranked at or above this one, so it works without physically sorting the sheet.
- Above or below the line, in M4: `=IF(K4<=$B$1,"In","Below the line")`, where B1 holds the available budget or capacity.
- Weight check, somewhere visible: `=SUM($D$2:$H$2)`. It must equal 1. Weights that quietly sum to 1.15 are the most common defect in a prioritization sheet.

All five work identically in Excel and Google Sheets. Add conditional formatting on the decision column and nothing else. A sheet with color on every cell is unreadable on a projector, which is where this one will be used.

## A worked example

Six candidate projects, the weights above, and a budget of 900,000 dollars. Scores and figures are illustrative.

| ID | Project | Fit (30%) | Value (25%) | Urgency (20%) | Risk (15%) | Confidence (10%) | Weighted | Cost | Cumulative |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| P-03 | Billing platform replacement | 5 | 4 | 4 | 5 | 2 | 4.25 | 420,000 | 420,000 |
| P-01 | Customer portal redesign | 4 | 4 | 3 | 2 | 4 | 3.50 | 260,000 | 680,000 |
| P-06 | Security remediation phase 2 | 2 | 1 | 4 | 5 | 4 | 2.80 | 180,000 | 860,000 |
| P-04 | Warehouse automation pilot | 3 | 4 | 2 | 1 | 3 | 2.75 | 310,000 | 1,170,000 |
| P-02 | Reporting data mart | 3 | 2 | 2 | 2 | 4 | 2.50 | 150,000 | 1,320,000 |
| P-05 | Office intranet refresh | 1 | 1 | 1 | 1 | 5 | 1.40 | 90,000 | 1,410,000 |

The line falls after P-06 at 860,000 dollars. Three projects are in, three are below the line. Notice what the arithmetic surfaced: the security remediation, which scores badly on strategic fit and financial value, still makes the cut because risk and urgency carry it. That is the weights doing their job. Notice also that the billing replacement has the lowest delivery confidence in the portfolio and the highest cost, which is a separate conversation the ranking should trigger rather than settle.

## Where the capacity line really goes

Budget is the easy constraint. The one that actually stops portfol
