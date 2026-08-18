<!--
URL: https://seoxpert.io/guides/complete-technical-seo-audit
Fetch date: 2026-08-18
Source type: vendor blog
Research cluster: technical-seo-audit
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting a previously-flagged severe coverage gap (zero link-graph content found in round 1/2 sources).
-->

# The Complete Technical SEO Audit: A 2026 Checklist
URL: https://seoxpert.io/guides/complete-technical-seo-audit
Published: 2026-04-23

This audit has been run on roughly 500 sites: small business homepages, agency portfolios, e-commerce checkouts, B2B SaaS dashboards, and whatever else came through the Seoxpert scanner. The order below is the order things are run in real audits, not alphabetical or grouped by "importance to Google" in the abstract. Every step fixes things that downstream steps depend on.

The most common audit mistake is starting at Core Web Vitals because Lighthouse gave a 67. Optimizing the LCP on a page that has noindex from a forgotten staging deploy is wasted work. Fix the stack from the bottom up.

## Why audit order matters

Technical SEO is a stack. The order Google does things in is: discovery (find the URL via links or sitemap) -> fetch (download the HTML, respecting robots.txt) -> render (run the JavaScript) -> index (decide whether to keep it, and which canonical URL to attribute it to) -> rank (compete for queries against everything else).

A cited example: a Shopify storefront whose owner had paid an SEO agency $4,000 to "optimize Core Web Vitals," with a 30-page report of Lighthouse screenshots, was tanking in organic traffic because a Shopify app installed two months earlier was injecting noindex,nofollow into every product detail page. The fix took 90 seconds (uninstall the app). The Lighthouse work would have been useful in three months, once indexing came back.

## 1. Crawl access

Three checks cover almost every real crawl failure: someone made a change to staging, then deployed staging-to-production by accident, and nobody noticed because the homepage still loads in a browser.

### robots.txt is reachable and permissive

Fetch /robots.txt on every subdomain. A 404 is fine (means no rules, full crawl allowed). A 500 or timeout is bad; Googlebot pauses crawling entirely until the file responds. The worst case: a Disallow: / from staging deployed to production. Observed twice in practice, once on a Webflow site that exported its staging environment for "backup," once on a Next.js app where a developer-only middleware was left in. Both times the site dropped out of Google over about 4 days. Use the robots.txt tester immediately after any infra deploy.

### XML sitemap is valid and complete

Three specific checks: (1) the sitemap URL returns 200 and parses as valid XML, (2) every URL in it returns 200 (not 3xx, not 4xx; Google warns on either), (3) indexable pages on the site that are NOT in the sitemap are flagged. The third is described as the silent killer: a WordPress site audited had 4,200 indexable URLs but the sitemap had only the 600 oldest posts because the SEO plugin's sitemap generator had silently failed years earlier. Three years of new content was crawled late or not at all. The default Next.js sitemap also gets this wrong if dynamic routes are not included explicitly.

### Internal links reach every important page

A page with zero inbound internal links is an "orphan." Google can find it via the sitemap, but it has no PageRank flowing in, so it ranks badly even when indexed. Every important page should be reachable from the homepage in 3 clicks or fewer. The most common cause: a category page that was once linked from the main nav but got moved to a footer-only or sitemap-only link during a redesign.

## 2. Indexing signals

Once crawled, each page tells Google whether to index it and which URL to prefer. Indexing conflicts are silent; pages vanish from search without warnings in Search Console unless specifically checked for.

### Canonical tag resolves correctly

Every indexable page needs a canonical tag pointing to the preferred URL, often itself. Five failure modes to check:

- Self-canonicals pointing to a different URL (protocol or trailing-slash mismatch).
- Canonicals pointing to pages that return 3xx, 4xx, or 5xx.
- Canonicals pointing to a noindex page (signals conflict, both may be ignored).
- Multiple canonical tags on the same page (only one is honoured).
- Cross-domain canonicals that may not be intentional.

### noindex is only where you mean it

A template-level noindex applied to production is as catastrophic as the robots.txt scenario described above. The fix: grep the codebase for noindex, audit every occurrence, and confirm only intended pages have it (internal search results, filtered product views, login pages, thank-you pages, draft preview routes). For WordPress sites, check Yoast and RankMath settings; for headless CMS deployments, check the metadata pulled from the CMS API.

### Redirect chains are short

Example of an accumulated chain: http://example.com/Page -> https://example.com/Page -> https://www.example.com/Page -> https://www.example.com/page -> https://www.example.com/page/. Each step is a redirect rule added one at a time over years. Each hop costs approximately 80ms of latency for users and a hop of crawl budget for Google. Two hops max is the target; three hops triggers Search Console warnings. Run a redirect chain check on both apex and www variants.

### hreflang is reciprocal and valid

For multilingual or multi-regional sites, hreflang annotations must be reciprocal (if the English page points to the Danish page, the Danish page must point back) and use exact ISO 639-1 language codes plus optional ISO 3166 country codes. The most common bug found is the BCP 47 region tag for the UK: it is en-GB, not en-UK. If hreflang is malformed or non-reciprocal, Google silently ignores it and falls back to its own language detection, which is described as wrong about 30% of the time on edge cases.

## 3. On-page signals

Once the page is crawlable and indexable, the content needs to tell Google what it is about.

### Unique, descriptive title tags

Each indexable page has a unique title tag, 55-60 characters, that describes the specific topic. Duplicate titles across many pages are a template-leak signal; missing titles force Google to synthesise one from H1 or anchor text.

### One H1 per page, aligned with the title

Common failure modes: H1 wrapped around the logo (same on every page), missing H1 entirely, or an H1 that contradicts the title and target keyword.

### Meta descriptions under the truncation point

Target 120-160 characters.

## 7. Monitoring and regression detection

Every deploy can reintroduce a previously fixed technical issue. Most regressions happen from: template changes (a refactor that accidentally removes canonical tags from every product page), infrastructure changes (CDN config, host rename, staging robots.txt in production), and third-party additions (a new analytics script that pushes LCP from 1.8s to 4.2s).
