<!--
URL: https://ecosire.com/blog/technical-seo-audit-checklist-2026
Fetch date: 2026-08-18
Source type: vendor blog
Research cluster: technical-seo-audit
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting a previously-flagged severe coverage gap (zero link-graph content found in round 1/2 sources).
-->

# Technical SEO Audit Checklist 2026: 47 Checks We Run on Every Client Site | ECOSIRE
URL: https://ecosire.com/blog/technical-seo-audit-checklist-2026
Published: 2026-06-06

The 47-point technical SEO audit checklist run on every client site in 2026: crawlability, indexation, canonicals, hreflang, Core Web Vitals, and logs.

A technical SEO audit answers one question: is anything about a site's infrastructure preventing content that deserves to rank from ranking? In 2026 that spans classic crawlability, the JavaScript rendering gap, Core Web Vitals field data, and a new layer: whether AI search crawlers can retrieve the content at all.

This is the literal 47-point checklist worked through on every client engagement, in the order run, with the decision rule for each check. It is sequenced by dependency: crawl problems invalidate indexation analysis, indexation problems invalidate content analysis. Run it top to bottom, log every finding with severity (Critical / High / Medium), and fix Critical items before touching anything cosmetic.

Key takeaways:

- Audit in dependency order: crawlability, then indexation, then duplication, then rendering, then performance, then enhancement layers; a Critical finding upstream changes everything downstream.
- Server log analysis is the only ground truth for how Googlebot actually spends its budget; crawl simulators approximate it, logs prove it.
- The most common Critical findings in 2026: faceted-navigation crawl traps, JavaScript-only content and links, hreflang reciprocity failures, and staging environments leaking into the index.
- Core Web Vitals must be judged on CrUX field data per template, not Lighthouse lab runs; only field data feeds rankings.
- Structured data belongs in the audit for rich-result eligibility, not as an AI-citation tactic; large-scale studies show schema does not drive LLM citations.
- AI retrievability is now a standard audit section: deliberate AI-crawler policy in robots.txt and server-side rendered content that retrieval bots (which execute little JavaScript) can read.
- An audit without prioritized, owner-assigned remediation tickets is a PDF, not an audit.

## Section A: Crawlability and Crawl Budget (Checks 1-8)

1. robots.txt is valid, accessible, and intentional. Returns 200 at the root, parses cleanly, declares the sitemap, and every Disallow line has a known reason. Diff it against the last known version; silent robots.txt changes cause more outages than any other single file.
2. XML sitemaps are clean and honest. Every URL returns 200, is canonical, and is indexable. Sitemaps containing redirects, 404s, or noindexed URLs train Google to distrust them. Large sites: segmented sitemaps per section so coverage problems can be localized.
3. Server logs show Googlebot spending budget on money pages. Pull 30 days of logs and compute the share of Googlebot hits landing on indexable, revenue-relevant URLs. Under approximately 70% means budget is leaking somewhere, and the logs say where.
4. Parameter and faceted-navigation traps are controlled. Filter, sort, and session parameters are either canonicalized and uncrawled, or deliberately indexable with unique content. Combinatorial URL explosion on ecommerce and listing sites is the most common Critical finding logged.
5. No redirect chains or loops on important paths. Every redirect resolves in one hop. Chains waste budget, leak equity, and break silently when one link in the chain changes.
6. Internal 404s and broken links are near zero. A full crawl lists every internal link to a 4xx target. A handful is hygiene; hundreds is an architecture problem.
7. No orphan pages among pages that matter. Cross-reference the crawl (link graph) against sitemaps and analytics. Pages with traffic or revenue but no internal links get linked; orphans with neither get judged for removal.
8. Server responds fast and reliably to bots. TTFB under approximately 600ms at origin, 5xx rate effectively zero in logs, no bot-specific throttling or WAF rules accidentally serving 403s to Googlebot.

## Section B: Indexation (Checks 9-14)

9. Indexed count roughly matches intended count. Search Console page indexing vs. the site's own canonical URL inventory. A large gap in either direction is the headline finding to explain.
10. noindex audit: nothing valuable is excluded. Crawl for meta robots and X-Robots-Tag headers; every noindex must be intentional. CMS template changes regularly noindex whole sections without anyone noticing.
11. Index bloat identified. Thin tag pages, internal search results, empty categories, printer views, expired listings sitting in the index dilute quality signals. Inventory them and decide: improve, consolidate, or remove.
12. "Crawled, currently not indexed" patterns diagnosed. This GSC bucket, read at scale, is Google's quality verdict by template. Clusters of one page type here point at thin or duplicative templates, not random bad luck.
13. Pagination is crawlable and consistent. Paginated series self-canonicalize (page 2 does not canonical to page 1), links are real anchors, and "view all" or load-more patterns have crawlable fallbacks.
14. Staging, dev, and test environments are out of the index. site: queries and Performance-report host data for staging subdomains. Leaked staging environments duplicate the entire site; authentication, not just noindex, is the fix.

## Section C: Canonicals and Duplication (Checks 15-19)

15. Every indexable page has a self-referencing canonical. Absolute URL, one per page, matching the served protocol and host.
16. One canonical host, one hop. http to https, www/non-www, trailing-slash and case variants all 301 to a single form, never via chained redirects or split server configs.
17. Parameterized duplicates canonicalize to the clean URL. UTM, sort, and pagination-irrelevant parameters never produce competing indexed versions.
18. Internal links agree with canonicals. If canonicals say /products/x but the site links /collections/y/products/x, Google receives contradictory signals daily. Make internal links point at canonical forms.
19. Cross-domain and syndication duplication handled. Content republished to partners, marketplaces, or international sister sites carries canonical or noindex agreements; otherwise the bigger domain wins the rankings for the content.

## Section D: International and hreflang (Checks 20-23)

20. hreflang annotations are reciprocal. Every alternate must link back. Non-reciprocal pairs are ignored entirely; this single failure invalidates most hreflang deployments audited.
21. x-default is declared for every URL group, pointing at the global or language-selector version.
22. Language-region codes are valid ISO formats (en-GB, not en-UK; zh-Hans where script matters), and annotations are consistent.
