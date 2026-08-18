<!--
URL: https://kennytan.net/tools/internal-link-equity-auditor/
Fetch date: 2026-08-18
Source type: vendor/community blog
Research cluster: internal-linking-analysis
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting a previously-flagged severe coverage gap (zero link-graph content found in round 1/2 sources).
-->

# Internal Link Equity Auditor - PageRank-style analysis of your site's internal link graph | kennytan.net
URL: https://kennytan.net/tools/internal-link-equity-auditor/
Published: 2026-04-01

Most SEO audits focus on per-URL signals (titles, schema, speed) but Google's link-graph weighting still drives major ranking outcomes, and internal linking is the one link signal a publisher fully controls. The problem is measurement: you can see 500 URLs in a crawler, but which of them are the real hubs, which are orphans, and which priority URLs are starved of equity? This auditor runs the PageRank math on a graph pasted from a crawl export or site-map dump, with priority URLs marked, and returns ranked equity distribution, structural flags, and specific link-addition recommendations (from top-20% URLs that don't currently link to an under-served priority URL).

Internal link graph is pasted as `source|target` per line, from a sitemap + crawl export (Screaming Frog, Ahrefs, Sitebulb) or a manual export. Expect 10-100 URLs for small sites, up to 10K for larger catalogs before browser-side compute gets slow.

Damping factor: Google's original value 0.85, representing the probability a random surfer follows a link vs jumps to a random page. Iterations: convergence for graphs under 10K nodes; most graphs stabilize in 20-30 iterations.

## Equity-distribution classification - reference

Priority-URL equity-distribution categories with diagnostic thresholds and typical fix:

| Category | Equity share | Inbound internal links | Signal | Typical fix |
| --- | --- | --- | --- | --- |
| HEALTHY | Top 20% of pages | 20+ internal links | Site-wide architecture directs equity here | Maintain; monitor for regression |
| MODERATE | 40-80th percentile | 8-20 internal links | Pages indexed + ranking, equity underweight | Add 3-5 contextual links from relevant hubs |
| UNDER-SERVED | Bottom 20% / equity-starved | <8 internal links | Important-per-strategy but structurally orphaned | Add 5-10 high-equity source-page links |
| ORPHAN | 0 inbound internal | 0 (sitemap-only) | Page exists but discoverable only via sitemap | Link from at least one topical hub immediately |
| DEAD-END | (n/a) | outbound 0 | Page has links in but no outs, an equity sink | Add 2-5 related-content outbound links |
| OVER-LINKED | >5% of total site equity | >150 inbound | Boilerplate over-exposure (e.g., footer-only link) | Reduce site-wide link; target contextual only |

## Why internal link equity matters

Google's original PageRank paper is 27 years old and the algorithm's direct role has been refactored many times since, but the underlying insight, that a link's value depends on the linker's value recursively, still drives a major component of search ranking via successors like TrustRank, topic-sensitive PageRank, and the various link-graph signals inside Google's Navboost and similar systems. A publisher does not fully control external links to their site, but does fully control their internal link graph, making internal linking the highest-leverage link-equity lever for most publishers.

Most audits miss this because measuring internal link equity requires graph-level computation, not per-URL analysis. Seeing "post X has 12 inbound internal links" is not the same as "post X holds 2.3% of total site equity" because those 12 links might be from low-equity leaf nodes. PageRank's recursive definition captures this: equity flows from linkers to linked, weighted by the linker's own equity, until the distribution stabilizes.

## What the equity distribution tells you about structure

The shape of the equity distribution reveals structural SEO health better than any single metric. A healthy hub-and-spoke site has the top 20% of URLs holding 40-70% of equity (Gini 0.40-0.65); Google receives a clear signal about which pages are authoritative. A flat distribution (Gini under 0.3) means no discernible hub, every page looks equally important, which in effect means none of them are particularly important. An over-concentrated distribution (Gini over 0.75) starves most of the content; the hubs rank but the spokes never break through.

The fix depends on the shape. Flat: designate 3-5 hubs, aggressively link everything related into them, build topic-cluster structure. Over-concentrated: identify under-served priority URLs, add inbound links from hubs, and consider whether outbound over-linking from hubs is diluting per-link equity.

## Orphans + dead-ends: why they're asymmetric problems

Orphans (URLs with 0 inbound internal links) are much worse than dead-ends (URLs with 0 outbound internal links). Orphans don't get discovered via internal crawl; Google reaches them only via sitemap.xml or external links, which means crawl-budget and discovery-lag issues. Dead-ends pass no equity forward but still receive equity, so they can still rank; they just don't contribute to the graph's flow. The asymmetry matters for remediation priority: fix orphans first.

Orphan fix: find related content, add at least one inbound link, ideally from a hub. Dead-end fix: add 3-5 contextual internal links to related content; this also passes equity forward and improves user session depth. Not every dead-end needs fixing (landing pages, conversion flows may be intentionally terminal), but the default is to link-out for organic-traffic URLs.

## Priority URLs: where the recommendations get specific

The most actionable output is priority-URL analysis. A pasted priority list (hubs, tools, high-revenue posts) is classified as HEALTHY (top-20% equity), MODERATE (above median but outside top 20%), or UNDER-SERVED (below median). For each UNDER-SERVED priority URL, the top-20% URLs that don't currently link to it are surfaced as specific source pages to add links from, prioritized by relevance to content.

## Handling dangling nodes correctly

Naive PageRank implementations produce incorrect scores when the graph contains dead-ends (pages with 0 outbound links); those pages accumulate equity but never pass it forward, causing the distribution to drift away from convergence. Proper PageRank redistributes each iteration's "dangling mass" (equity held by dead-ends) uniformly across all nodes, ensuring convergence and accurate scores regardless of how many dead-ends the site has.

## What this tool does not measure

Four things require different tools: (1) external link equity, this auditor analyzes internal links only, external backlinks drive the base equity a site has overall and are measured by tools like Ahrefs, Semrush, Moz Link Explorer; (2) link context quality, anchor text relevance and position on page (header vs footer links carry different weight) and surrounding content topic-match, since this auditor measures topology only; (3) historical equity flow, how equity has shifted over time as links were added/removed, requiring longitudinal crawls; (4) Google-specific signal weighting, Google's actual algorithm applies post-PageRank layers (topical authority, E-E-A-T, query-specific adjustments) that this auditor's foundational graph math does not replicate 1:1. Use as a structural-health signal, not a precise rank predictor.
