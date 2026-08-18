<!--
URL: https://autorubric.org/docs/api/
Fetch date: 2026-08-18
Source type: official docs
Research cluster: scoring-rubric-and-rollup
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# API Reference, AutoRubric
URL: https://autorubric.org/docs/api/
Author: Delip Rao

AutoRubric exports 91 public items across the main module and `autorubric.graders`, plus 20 additional building-block functions and types available from `autorubric.meta`.

## Relevant chapters

| Chapter | Key Exports | Description |
|---|---|---|
| CANNOT_ASSESS Handling | `CannotAssessConfig`, `CannotAssessStrategy` | Configure handling of uncertain verdicts |
| Core Grading | `Criterion`, `Rubric`, `EvaluationReport` | Fundamental types for rubric-based evaluation |
| Ensemble | `EnsembleEvaluationReport`, `JudgeVote` | Multi-judge aggregation |
| Metrics | `MetricsResult`, `compute_metrics` | Agreement and correlation metrics |
| Multi-Choice | `CriterionOption`, `MultiChoiceVerdict` | Ordinal and nominal scales |

## Architecture

### Grading flow

1. `Rubric.grade()` delegates to a grader's `grade()` method.
2. `CriterionGrader` treats a single LLM as an "ensemble of 1."
3. Makes concurrent LLM calls per criterion per judge via `asyncio.gather()`.
4. Aggregates votes using a configurable strategy.
5. Returns an `EnsembleEvaluationReport` (a consistent interface regardless of ensemble size).

### Score calculation

```
# Positive criteria: MET earns weight, UNMET earns 0
# Negative criteria: MET subtracts weight, UNMET contributes 0
weighted_sum = sum(verdict_value * criterion.weight for each criterion)
score = clamp(weighted_sum / total_positive_weight, 0, 1)  # if normalized
# Length penalty subtracted after base calculation
```

This is a positive/negative-weighted-sum-then-normalize pattern: sum each criterion's verdict value times its weight, then divide by the total positive weight to normalize into 0 to 1, with negative-weight criteria acting as penalties subtracted from the sum rather than being normalized against their own weight total.

## Conventions (the N/A-aware handling)

- All graders return `EnsembleEvaluationReport` for a consistent interface.
- `raw_score` (the unnormalized weighted sum) is populated regardless of the `normalize` setting on a successful grade, but is `None` on a failed/error report; consumers should filter on `error is not None`.
- Judge-call failures route through `classify_grading_error`: infrastructure or parse failures become `CANNOT_ASSESS` (`na=True`), excluded from scoring under the default SKIP strategy. Only genuinely `unknown` errors fall back to a conservative worst-case verdict (UNMET for a positive-weight criterion, MET for a negative-weight criterion, i.e. always the score-lowering outcome).
- Filter `error is not None` results out of training pipelines.
- Rate limiting is applied via `LLMConfig.max_parallel_requests` (a per-provider semaphore).

## Direct applicability to N/A-aware multi-level rollups

This is the closest raw-sourced example in this cluster of an explicit, named "N/A-aware" scoring mechanic: a criterion that cannot be assessed (`CANNOT_ASSESS`, `na=True`) is excluded from the weighted sum entirely under the default strategy, rather than being scored as a failure or silently included as zero. This is the general pattern this Bee's own N/A-handling should follow: an N/A leaf criterion should be dropped from both the weighted numerator and the weight denominator of its parent rollup, the same dual-exclusion requirement flagged (as an inference, not a directly-sourced claim) in this cluster's SUMPRODUCT/DataCamp source. AutoRubric's own docs do not describe a multi-level (leaf to sub-audit to category to final) hierarchy explicitly in this fetched page; its scoring model as documented here is single-level (one weighted sum over a flat set of criteria per rubric), so the leaf-to-category-to-final rollup structure itself is not directly grounded in this source, only the N/A-exclusion mechanic is.
