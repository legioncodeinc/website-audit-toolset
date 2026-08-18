<!--
URL: https://docs.ahrefs.com/en/api/reference/keywords-explorer/get-matching-terms
Fetch date: 2026-08-18
Source type: official docs
Research cluster: keyword-source-priority
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# Matching terms | Ahrefs for Developers
URL: https://docs.ahrefs.com/en/api/reference/keywords-explorer/get-matching-terms

API + MCP

`GET /v3/keywords-explorer/matching-terms`

## Query parameters

- `timeout` (integer): a manual timeout duration in seconds.
- `limit` (integer): the number of results to return. Max: `150000`. Default: `1000`.
- `order_by` (string): a column to order results by (see response schema for valid identifiers, except `volume_monthly`, which is not supported in `order_by` for this endpoint). Example: `field_a,field_b:asc,field_c:desc`.
- `where` (string): a filter expression over recognized column identifiers (differs from the identifiers recognized by `select`).
- `select` (string, required): a comma-separated list of columns to return.
- `keyword_list_id` (integer): the id of an existing keyword list.
- `keywords` (string): a comma-separated list of keywords to show metrics for.
- `country` (string, required): a two-letter country code (ISO 3166-1 alpha-2).
- `terms` (string): all keyword ideas, or keyword ideas phrased as questions. Allowed values: `all`, `questions`. Default: `all`.
- `match_mode` (string): keyword ideas contain the words from the query in any order (`terms` mode) or in the exact order written (`phrase` mode). Allowed values: `terms`, `phrase`. Default: `terms`.
- `output` (string): the output format. Allowed values: `json`, `php`, `xml`.

## Response fields (per keyword)

- `cpc` (integer or null): Cost Per Click, average price advertisers pay per ad click in paid search results, in USD cents.
- `cps` (number/float or null): Clicks Per Search, ratio of clicks to keyword search volume; shows how many different search results get clicked, on average, when people search for the target keyword in a given country.
- `difficulty` (integer or null, 10 units): an estimation of how hard it is to rank in the top-10 organic search results for a keyword, on a 100-point scale.
- `first_seen` (string date-time or null): the date Ahrefs first checked search engine results for a keyword.
- `global_volume` (integer or null, 10 units): how many times per month, on average, people search for the target keyword across all countries in Ahrefs' database.
- `intents` (object or null, 10 units): the purpose behind the user's search query, with boolean fields `informational`, `navigational`, `commercial`, `transactional`, `branded`, `local`.
- `keyword` (string).
- `parent_topic` (string or null): determines if you can rank for your target keyword while targeting a more general topic on your page instead; identified by taking the #1 ranking page for your keyword and finding the keyword responsible for sending the most traffic to that page.
- `serp_features` (array): enriched SERP results that are not traditional organic results (e.g. `ai_overview_sitelinks`, `ai_overview`, `local_pack`, `sitelink`, `news`, `image`, `video`, `discussion`, `tweet`, `paid_top`, `paid_bottom`, `paid_sitelink`, `shopping`, `knowledge_card`, and more).
- `serp_last_update` (string date-time or null): the date Ahrefs last checked search engine results for a keyword.
- `traffic_potential` (integer or null, 10 units): sum of organic traffic that the #1 ranking page for the target keyword receives from all the keywords it ranks for.
- `volume` (integer or null, 10 units): estimated average monthly number of searches for a keyword over the latest known 12 months of data.
- `volume_desktop_pct` / `volume_mobile_pct` (number/float or null): percentage of searches performed on desktop vs. mobile devices.
- `volume_monthly` (integer or null, 10 units): estimated number of searches for a keyword over the latest month; cannot be used in the `order_by` parameter.

Note: several fields are explicitly costed at "10 units" each per the endpoint's own documentation, indicating Ahrefs' API billing is unit-based per requested field rather than a flat per-keyword or per-task charge (contrast with DataForSEO's flat per-task-plus-per-item pricing documented separately in this research cluster).

Response status codes documented: 200, 400, 401, 403, 429, 500 (each carrying an `error` string field on non-200 responses).
