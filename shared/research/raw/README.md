# Raw research archive, forge stage 2 sweep (three rounds, all 20 pairs covered)

Three rounds of research now cover all 20 Bee/Stinger pairs. Sources fetched via
`mcp__Exa__web_search_exa` followed by `mcp__Exa__web_fetch_exa` (maxCharacters 7000), archived here
one file per source, headed with URL, fetch date, and source type per queen-bee-stinger's
forge-stage-2 convention. Each file was also copied (not symlinked) into every feeding Stinger's own
`skills/<slug>-stinger/references/research/raw/` folder, replacing that folder's `.gitkeep`
placeholder.

69 raw source files total, 80 distributed copies across 20 Stingers (some Stingers sit at the
intersection of more than one cluster and receive copies from each).

All 20 pairs have been through forge stage 3 (distillation) at least once. The 10 pairs listed in
"Round 3" below have been distilled twice: once after round 2 (flagged thin-coverage), and again
after round 3 closed most of those gaps. See each Stinger's own
`references/research/distilled-<short-slug>.md` for the current distilled article.

## Round 1 clusters (step 6 of the original build sequence)

| Cluster folder | Sources | Feeds |
|---|---|---|
| `platform-fingerprinting/` | 2 | stack-fingerprint-stinger, site-crawler-stinger |
| `third-party-and-injection/` | 2 | vendor-inventory-stinger, web-security-posture-stinger, analytics-stack-stinger |
| `seo-standards/` | 2 | technical-seo-stinger, content-semantics-stinger, internal-linking-stinger |
| `aeo-and-answer-engines/` | 2 | aeo-audit-stinger, content-semantics-stinger |
| `core-web-vitals-and-delivery/` | 2 | performance-cwv-stinger |
| `accessibility/` | 2 | accessibility-audit-stinger |
| `web-security-posture/` | 2 | web-security-posture-stinger |
| `analytics-and-deanonymization/` | 2 | analytics-stack-stinger |
| `ai-content-detection/` | 2 | blog-content-stinger |

## Round 2 clusters (the 8 pairs round 1 left uncovered)

| Cluster folder | Sources | Feeds |
|---|---|---|
| `audit-intake-workflow/` | 2 | audit-intake-stinger |
| `icp-positioning/` | 2 | icp-positioning-stinger |
| `keyword-source-priority/` | 2 | keyword-intelligence-stinger |
| `scoring-rubric-and-rollup/` | 2 | audit-scoring-stinger |
| `audit-report-authoring/` | 2 | audit-reporting-stinger |
| `ecommerce-catalog-audit/` | 2 | ecommerce-catalog-stinger |
| `visual-funnel-audit/` | 2 | visual-funnel-stinger |
| `social-presence-audit/` | 2 | social-presence-stinger |

Every one of the 20 Bee/Stinger pairs now has at least 2 raw sources feeding it. This closed the
gap flagged in `library/requirements/reports/step7-handoff-report.md`.

## Round 3 clusters (deeper research pass on the 10 pairs round 2 flagged thin-coverage)

Round 2 left 10 pairs at exactly 2 raw sources each, flagged thin in their own distilled files.
This round targeted those 10 specifically, with extra search depth on the two pairs the earlier
addendum called most load-bearing (audit-scoring, keyword-intelligence), and a from-scratch new
cluster for internal-linking, whose round-1/2 sources turned out to contain zero link-graph content
at all.

| Cluster folder | New sources this round | Total sources now | Feeds |
|---|---|---|---|
| `audit-intake-workflow/` | 3 | 5 | audit-intake-stinger |
| `icp-positioning/` | 3 | 5 | icp-positioning-stinger |
| `keyword-source-priority/` | 4 | 6 | keyword-intelligence-stinger |
| `scoring-rubric-and-rollup/` | 5 | 7 | audit-scoring-stinger |
| `audit-report-authoring/` | 3 | 5 | audit-reporting-stinger |
| `ecommerce-catalog-audit/` | 3 | 5 | ecommerce-catalog-stinger |
| `visual-funnel-audit/` | 3 | 5 | visual-funnel-stinger |
| `social-presence-audit/` | 3 | 5 | social-presence-stinger |
| `internal-linking-analysis/` (new cluster) | 4 | 4 (plus 2 still-irrelevant round-1 carryovers left in place, uncited) | internal-linking-stinger |
| `technical-seo-audit/` (new cluster) | 3 | 3 (plus 2 round-1 carryovers, partially relevant) | technical-seo-stinger |

All 10 pairs' distilled files were rewritten from scratch, re-ingesting every raw file (old and new)
in that pair's archive, in the same dense/tabular/cited format used throughout this repo. Genuine
progress, stated honestly rather than oversold:

- **keyword-intelligence**: tier 3 (AI/statistical keyword inference without GSC or Trends data) and
  tier 4 (paid keyword API pricing and mechanics) of the plugin's binding 4-tier source-priority
  chain are now grounded, closing what was previously a complete gap for those two tiers.
- **audit-scoring**: the N/A-aware SUMPRODUCT-style masking formula, openpyxl branded-XLSX
  generation mechanics, and a multi-criteria weighted-rollup pattern with explicit N/A exclusion are
  now grounded. The leaf-to-sub-audit-to-category-to-final nesting structure itself is still an
  inference rather than a directly-sourced pattern; the distilled file says so.
- **internal-linking**: previously had zero link-graph content in its archive. Now has cited,
  grounded coverage of orphan-page detection, click-depth via breadth-first search, anchor-text
  quality scoring, anchor-text cannibalization, and internal-PageRank-style equity flow. Some
  specific thresholds come from a single vendor source each and are not yet cross-validated; flagged
  as such rather than presented as consensus.
- **audit-intake, icp-positioning, audit-reporting, ecommerce-catalog, visual-funnel,
  social-presence, technical-seo**: each closed at least one of its previously-named gaps (see each
  pair's own distilled file for specifics); each also still names at least one honest remaining gap
  rather than papering over it. Notably, icp-positioning found no source anywhere supporting this
  plugin's specific "two-stage" buyer-readiness framing (sources converge on a three-stage model
  instead), so its distilled file now states plainly that the two-stage model must be built as an
  explicit collapse of the three-stage one, not presented as independently sourced.

Verification run independently after all five research agents reported back (not taken on their word
alone): a repo-wide dash-guard scan and a citation-integrity script confirming every `[raw/...]`
bracket in all 10 rewritten distilled files resolves to a real file, and every raw file in each
pair's archive is cited at least once. Both came back clean. One nuance on the dash guard: round-1/2
raw archive files (verbatim-quoted third-party article text, not authored content) do contain em/en
dashes inherited from their source pages; that is expected and was left untouched, since altering a
quoted source would break citation integrity. Every file actually authored this round (all 10
distilled files, all 34 new raw archive files' headers and surrounding structure) is dash-clean.
