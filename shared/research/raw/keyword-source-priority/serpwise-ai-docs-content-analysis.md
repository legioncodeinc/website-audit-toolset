<!--
URL: https://serpwise.ai/docs/content-analysis/
Fetch date: 2026-08-18
Source type: official docs
Research cluster: keyword-source-priority
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# Content Analysis: Serpwise Documentation
URL: https://serpwise.ai/docs/content-analysis/

Automated content quality metrics: word count, readability, keyword extraction, and duplicate detection for every crawled page.

Content Analysis extracts quality metrics from every page the Edge Crawler processes. Word count, readability scores, keyword density, and content hashing are all computed automatically during crawling, with no extra credits required.

---

## Metrics Extracted

The following metrics are computed and stored for every crawled page:

| Metric | Description |
| --- | --- |
| Word Count | Total words in the main content area |
| Reading Time | Estimated reading time based on word count |
| Readability | Flesch-Kincaid grade level score |
| Content Hash | Unique hash of the page content for duplicate detection |
| Image Count | Number of images found on the page |
| Internal Links | Count of links pointing to other pages on the same domain |
| External Links | Count of links pointing to other domains |
| Schema Types | JSON-LD schema types detected (Product, Article, etc.) |

View these metrics on the Content tab of any URL Detail page.

---

## Content Quality

### Thin Content Detection

Pages with fewer than 100 words of main content are flagged as thin content. Thin pages can hurt your domain's overall SEO performance, since search engines may consider them low-value or fail to rank them.

The Site-Wide SEO Dashboard shows a count of all thin content pages across your domain for easy triage.

### Readability

The Flesch-Kincaid grade level indicates the education level needed to understand the content:

| Grade Level | Interpretation |
| --- | --- |
| 5 to 8 | Easy to read, suitable for a broad audience |
| 9 to 12 | Moderate, appropriate for most web content |
| 13+ | Difficult, consider simplifying for wider reach |

Lower readability scores generally correlate with better engagement, especially for consumer-facing content.

---

## Keyword Extraction

Serpwise extracts top keywords from each page using TF-IDF (Term Frequency-Inverse Document Frequency) analysis across your domain. This surfaces the most distinctive terms on each page relative to your other content.

- Per-page keywords: the most prominent terms on a specific page
- Domain-wide analysis: keywords are weighted against your full page index, highlighting terms that are uniquely important to each page rather than common site-wide terms

Use keyword data to verify pages are targeting intended topics and to spot content gaps.

---

## Duplicate Detection

Each page's content is hashed during crawling. When multiple pages share the same content hash, they're flagged as potential duplicates.

The Content tab on the URL Detail page shows:

- The content hash for the current page
- Any other pages on the same domain with a matching hash

Duplicate content can dilute search rankings. Use canonical tags or redirects to consolidate duplicate pages.

---

## How Data Is Collected

Content metrics are extracted automatically during every crawl, with no separate process to enable or configure. When the Edge Crawler indexes a page, the audit engine parses the HTML, extracts content, and computes all metrics in a single pass.
