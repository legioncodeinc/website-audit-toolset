<!--
URL: https://unveilseo.com/blog/internal-link-audit
Fetch date: 2026-08-18
Source type: vendor blog
Research cluster: internal-linking-analysis
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting a previously-flagged severe coverage gap (zero link-graph content found in round 1/2 sources).
-->

# How to Audit Internal Links for Signal, Not Plumbing | Unveil SEO Blog | Unveil SEO
URL: https://unveilseo.com/blog/internal-link-audit
Published: 2026-06-30
Author: Mathias Decourt

Most internal link audits stop at the plumbing: find the broken links, fix the redirects, spot the orphan pages. That is the baseline, and it matters. But it is also where most audits end. The harder question is not "do the links work?" It is "do the links transmit anything useful?"

## The technical audit: does the plumbing work?

These are the checks every audit should start with, catching the issues that prevent links from functioning at all.

- Broken links (404s): a link pointing to a page that no longer exists passes no authority and creates a dead end for both users and crawlers. Run a crawl (Screaming Frog, Sitebulb, or equivalent), filter by HTTP status code 4xx, and fix or remove each one.
- Links pointing to redirects: an internal link targets a URL that 301-redirects to another page. The link still works for the user, but each hop wastes crawl budget and dilutes the signal. Update the link to point directly to the final URL.
- Orphan pages: pages that exist on the server but receive zero internal links. Search engines can still find them through the sitemap, but they receive significantly less crawl priority. Botify's research found that orphan pages consume 26% of crawl budget on average, with extreme cases reaching 70%.
- Nofollow on internal links: the rel="nofollow" attribute tells Google not to pass authority through a link. On internal links this is almost always unintentional (a CMS default, a template error, or a plugin side effect). Check the crawl for internal links carrying nofollow and remove the attribute.
- Pages buried too deep: if a page requires more than three clicks from the homepage, Google treats it as lower priority. John Mueller is quoted: "A flatter site structure is easier for us to crawl." Check the crawl depth report and flag anything above 3.

These five checks are table stakes. If an audit stops here, the links are known to function, but not whether they accomplish anything.

## The signal audit: do your links actually transmit something?

A link can be technically perfect (no 404, no redirect, correct HTML) and still carry zero useful signal. The difference is in what the link says, where it points, and how authority flows through it.

### Anchor quality

A page can receive thousands of links and still score poorly if those links say nothing. Four dimensions to check:

| Dimension | What to look for | Red flag |
| --- | --- | --- |
| Generic ratio | Share of anchors that are "click here", "read more", "en savoir plus" | > 30% generic |
| Diversity | Number of unique anchor texts pointing to each important page | < 3 unique anchors |
| Topical relevance | Does the anchor contain words related to the target page's topic? | Zero overlap with target |
| Length | Number of words in the anchor | Mostly 1-word or empty anchors |

Each page's anchor profile can be scored out of 100 across these four dimensions to show exactly where the signal is weak: diversity, generic ratio, topical relevance, and anchor length. This matters because Google does not just read the anchor text, it reads a window of surrounding text to determine what signal a link carries. An empty anchor in a generic sentence transmits close to nothing, regardless of how many links point to the page.

### High-potential pages that are underlinked

This is described as the highest-ROI check in the entire audit, and one almost nobody does systematically. Method: pull Google Search Console Performance data (impressions, average position), cross it with crawl data (number of inbound internal links per page), then filter for pages with high impressions, position 8-15, and few internal links. These pages already rank; they are on the edge of page one. A few well-placed internal links can push them over.

### Dead-end pages

A page that receives links but emits zero contextual outbound links. Authority flows in and stops. These are the inverse of orphan pages: not invisible, but selfish. Detect by filtering the crawl for pages with 0 contextual outbound links (excluding navigation).

### High-authority pages that don't redistribute

A page receives strong external backlinks but has zero internal outbound links. The authority enters the site and pools on one page instead of flowing through the structure. Cross backlink data (Ahrefs, GSC) with the crawl's outbound link count; any page with high external authority and no internal outbound links is a bottleneck.

### Anchor text cannibalization

The same exact anchor text points to two different pages. Google receives conflicting signals about which page is the right target for that term. Detect by exporting all internal links and sorting by anchor text; any anchor that appears with two or more distinct destination URLs needs to be resolved.

## The audit sequence

1. Crawl the site with GSC and GA4 integrations enabled.
2. Fix the plumbing: broken links, redirects, nofollow, buried pages.
3. Detect orphans: compare crawled URLs vs. sitemap and GSC.
4. Audit anchors: run an anchor quality check or export and classify anchors from the crawler.
5. Find signal gaps: underlinked high-potential pages, dead-ends, authority pools, cannibalization.
6. Prioritize by impact: pages with high impressions + low links first, then anchor fixes, then structural leaks.

Cadence: every publication (is the new content linked from existing pages?), monthly (check for new 404s, redirect chains, and recently published pages that were never integrated), quarterly (full structural audit covering coverage, anchors, and signal, including whether the semantic cluster architecture still holds as content grows), and after any major site change like a redesign or migration.

## FAQ

An orphan page receives no internal links; it is invisible to crawlers and users navigating the site normally. A dead-end page receives links in but emits zero outbound contextual links, so it is discoverable but does not redistribute the authority it accumulates.
