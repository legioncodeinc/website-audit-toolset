<!--
URL: https://sulayman-bowles.dev/research/technical-seo/internal-links-directed-retrieval-graph
Fetch date: 2026-08-18
Source type: vendor/community blog
Research cluster: internal-linking-analysis
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting a previously-flagged severe coverage gap (zero link-graph content found in round 1/2 sources).
-->

# Internal Linking as a Directed Retrieval Graph
URL: https://sulayman-bowles.dev/research/technical-seo/internal-links-directed-retrieval-graph
Published: 2026-07-19

Internal Linking as a Directed Retrieval Graph

Analyze internal links as a directed graph using reachability, depth, components, edge context, orphan states, and executable validation instead of raw link counts.

 SULAYMAN BOWLES Technical SEO, AI Systems, Finance Research

## Direct answer: internal linking graph

An internal linking graph models pages as nodes and crawlable links as directed edges so teams can measure depth, orphan risk, inlink concentration, anchor context, cluster connectivity, and the actual retrieval paths supporting each important page.

### Original research artifact

A directed-edge schema, breadth-first depth calculation, orphan test, anchor audit, and cluster-connectivity checklist.

### What this page adds

Connect graph measures to user journeys and crawl evidence instead of presenting PageRank-like scores without inspectable edges.

## Memo Details

Category: SITE ARCHITECTURE. Author: SULAYMAN BOWLES. Published: 2026.07.19. Read time: 13 MIN. Source count: 5.

## Evidence Boundary

Graph metrics describe the captured internal architecture and help prioritize review. They do not measure proprietary ranking weights, guarantee crawling or indexing, or prove that adding a link will improve search performance.

## Article Metrics

Graph: DIRECTED. Edge context: RETAINED. Orphan states: 04. Primary artifact: LINK EDGE TABLE.

## Research Note

An internal link is a directed edge from one document to another, observed in a particular source or rendered state with anchor text, placement, and crawlability conditions. Reducing that edge to a destination count discards the information needed to explain architecture. A global navigation link, an editorial citation, a related-product card, a pagination control, and a hidden script route can all point to the same URL while serving different retrieval functions.

The graph-first approach preserves node identity and edge context, then asks reachable questions: which canonical pages can be reached from approved entry points, how many hops are required, which components are disconnected, where do redirects consume edges, and which important pages depend on one fragile source? Metrics narrow the review set. They do not replace the product judgment that determines which paths should exist.

## Store a link edge with enough context to review it

The minimum edge has a source URL, observed href, resolved destination, anchor or accessible name, DOM or source location, link type, discovery state, and artifact reference. Preserve whether the element was an anchor with an href because Google documents that form as the generally crawlable link pattern. A click handler on a div may support a user interaction while remaining a different technical object.

Normalize the source and destination against the same route-identity contract used by the crawl frontier, but retain the observed href. Relative paths, fragments, alternate hosts, tracking parameters, and redirects can then be diagnosed without losing evidence. Classify the destination after resolution as canonical, alias, external, asset, non-HTTP, malformed, or unknown.

Placement should be derived cautiously. Header, primary navigation, breadcrumb, main content, related content, pagination, filter, and footer are useful classes when the DOM structure supports them. Do not infer importance from CSS coordinates alone. The important point is that a repeated template edge and a unique editorial edge remain distinguishable.

Internal-link edge contract:

| Field | Example | Review question |
| --- | --- | --- |
| source_key | /guides/crawling | Which canonical page emits the edge? |
| observed_href | ../tools/crawler?ref=guide | What did the document actually contain? |
| destination_key | /tools/crawler | Which canonical identity receives it? |
| label | crawler architecture tool | Can a reader predict the destination? |
| placement | main/editorial | Is the edge contextual or repeated template chrome? |
| artifact_ref | run/url/source#node-184 | Can another reviewer reproduce the observation? |

## Measure reachability from real entry points

A page is structurally reachable when a directed path exists from an approved entry set through crawlable internal edges. The homepage is one entry, not the only one. Category hubs, section roots, locale roots, authenticated application shells, and feed or campaign landings can represent different user journeys. Define the entry set before calculating depth.

Run breadth-first search on canonical destinations after resolving known redirects. Report shortest depth and at least one path, but also count independent parent sources. A priority page reachable in two hops through one soon-to-be-retired article is more fragile than a page with several relevant parents. Path diversity is not a ranking metric; it is an architecture resilience measure.

Keep source and rendered graphs separate when client execution adds navigation. If the source graph cannot reach an article but the rendered graph can, the finding is dependency on the tested client path, not absolute orphaning. If neither graph reaches it but a sitemap lists it, label it sitemap-only. Each state implies a different repair.

Reachability states for a public canonical page:

| State | Observed evidence | Interpretation |
| --- | --- | --- |
| source-reachable | Path through source anchor href edges | Server-delivered discovery path exists |
| render-only | No source path; path appears after tested execution | Discovery depends on client rendering scenario |
| sitemap-only | No internal path; canonical URL is nominated in sitemap | Declared but not architecturally integrated |
| external-only | Known inbound reference but no internal path | Third-party discovery exists; internal context absent |
| unobserved | No captured path or nomination | Coverage or publication gap; verify inventory first |

## Diagnose components before labeling orphan pages

A directed graph can contain weakly connected groups that are isolated from the primary site and strongly connected groups that circulate internally without a path from an entry. These components often reveal retired subdirectories, alternate hosts, faceted islands, staging remnants, or microsites imported without navigation. Inspect representative URLs and edge classes before assigning one site-wide remedy.

An orphan label needs an inventory source. A page discovered only through a database export, analytics, log file, external backlink, or sitemap is not equivalent to a page discovered during the internal crawl. Record the source that proves the node exists. Without that, the absence of inlinks may simply mean the crawler never knew the URL.

Not every zero-inlink URL needs a new link. Redirect targets, campaign pages, utility endpoints, legal notices, feed documents, and intentionally private states may have special entry paths or should leave the indexable inventory. The decision should be keep and link, consolidate and redirect, retain with bounded reachability, noindex, or remove, not add links everywhere.

Practical steps:

- Compare crawl nodes with sitemap, analytics, logs, CMS exports, and approved route registries.
- Separate zero observed inlinks from zero eligible crawlable inlinks.
- Inspect weak and strong components for shared template or host causes.
- Assign an intended entry path before proposing a link.
- Remove aliases and noncanonical URLs from the candidate set before counting orphans.

## Graph metrics and their common misuse

In-degree identifies destinations receiving many captured edges; out-degree identifies sources that distribute many. Depth exposes long retrieval paths. Betweenness can identify bridge pages whose removal disconnects routes. Strong components expose circulation. Edge concentration shows whether most paths depend on one template. These measures are useful because they reveal structures worth reviewing.

Raw PageRank or similar centrality scores can be calculated on an internal graph, but the score is a model of the captured link network, not a disclosed search-engine value. Results are sensitive to which nodes and edges were included, how redirects were resolved, whether repeated links were collapsed, and how dangling nodes were handled. Store those choices next to the output.

Anchor text and surrounding context answer a different question: whether the relationship is legible. Repeated exact-match anchors are not automatically better, and generic labels are not automatically wrong. Review whether the phrase helps a reader understand the destination, fits the sentence or component, and distinguishes nearby links.

| Metric | Useful question | Common misuse |
| --- | --- | --- |
| shortest depth | How many eligible hops from the intended entry? | Treating every deep page as low quality |
| in-degree | Which destinations attract or lack internal references? | Equating count with proprietary authority |
| parent diversity | How many independent sources support the route? | Counting repeated template links as independent |
| betweenness | Which pages bridge otherwise separate sections? | Changing bridges without journey review |
| component membership | Which routes circulate outside the main architecture? | Calling every isolated component an error |

## Repair plans and re-verification

A link plan should name the source page, destination canonical, placement, intended reader question, anchor or component label, owner, and expected graph change. This prevents the recommendation "add more internal links" from becoming a site-wide template block. The strongest repairs usually connect an existing explanatory page to the next useful artifact or decision.

After implementation, crawl the same scope and rebuild both source and rendered edge tables. Assert that the new edge is a crawlable anchor, reaches the canonical destination without an avoidable redirect, appears in the intended component, and does not create broken or duplicate links. Recalculate reachability and depth only after the edge-level checks pass.

Monitor for regressions when templates or route registries change. A page can return to sitemap-only status when a collection stops rendering, a navigation key changes, or a canonical path is renamed without updating contextual links. The durable artifact is therefore not a one-time score; it is a versioned graph and a small set of architecture invariants.

Internal-link quality is the ability of people and crawlers to reach the right canonical pages through meaningful, crawlable paths, not the number of links a template can emit.

Useful internal architecture gives priority pages several meaningful, crawlable paths from real entry points. The durable artifact is a versioned graph whose reachability and path-diversity invariants survive template and route changes.
