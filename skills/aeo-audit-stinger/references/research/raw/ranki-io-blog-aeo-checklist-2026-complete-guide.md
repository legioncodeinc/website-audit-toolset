<!--
URL: https://ranki.io/blog/aeo-checklist-2026-complete-guide
Fetch date: 2026-08-18
Source type: vendor blog
Research cluster: aeo-and-answer-engines
Archived by: forge stage 2 sweep (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc. build sequence step 6.
-->

# The 2026 AEO Checklist — 15 Signals AI Engines Use to Pick Citations
URL: https://ranki.io/blog/aeo-checklist-2026-complete-guide
Published: 2026-05-28

The 2026 AEO Checklist — 15 Signals AI Engines Use to Pick Citations

# The 2026 AEO checklist — 15 signals AI engines actually use

Every signal I have watched move citation outcomes across hundreds of audited pages, ranked, with the deterministic fix for each. Heuristic-first, so you can verify the scan output against your own DOM.

By Younes Lamnabhi· In SEO since 2009· Updated May 28, 2026· 18 min read

The short version

Answer Engine Optimization in 2026 is a structural game with fifteen signals, not five hundred. The ones that actually move citation rates are FAQPage schema, Article or BlogPosting schema, a definitional first paragraph (30-90 words), llms.txt presence, robots.txt access for GPTBot / ChatGPT-User / ClaudeBot / PerplexityBot / Google-Extended, an author byline, and answer-style H2/H3 headings. The rest are foundational SEO signals that AEO inherits. Run a real-page scan, fix the failed signals in order, re-scan in 7 days, ship.

Most of the AEO checklists circulating in 2026 list fifty or sixty signals, half of which do not move anything. I rebuilt mine after a year of running real-page scans against pages we knew were either cited or not cited by ChatGPT, Perplexity, Claude, Gemini and Google AI Overviews. The signals that actually matter shrunk to fifteen. The rest are foundational SEO that AEO inherits — they show up in any decent on-page audit, do not deserve a separate AEO label, and quietly distract from the structural moves that change citation outcomes.

This guide is the checklist itself, with the reasoning behind each signal and the deterministic fix for each miss. It is the list I run against my own clients' pages every Monday morning. If you want the score without doing the math by hand, drop a URL into the free AEO scan at the end — it grades all fifteen against your live HTML and returns a 0–100 score, a category breakdown and a fix for each fail.

## What an AEO score actually grades

An AEO score is a weighted measure of structural readiness for AI citation extraction. It does not measure the literal probability your page will appear in a given ChatGPT or Perplexity answer — that depends on the query, the user's location, the model's freshness window and the citation pool for that topic. It measures whether your page has the foundation those engines look for when they decide which pages to retrieve, re-rank and quote. A page can earn a 90+ score and still not appear for queries it does not topically match. A page with a 30 score will almost never be cited even for queries it perfectly matches, because it fails at the extraction layer.

The signals split into four tiers by impact. Schema tier is the highest leverage in 2026 because Google deprecated FAQ rich snippets in 2023, and most SEOs dropped FAQPage JSON-LD as a side effect. AI engines kept parsing it. Pages that still ship FAQPage schema have a measurable citation advantage. Content-shape tier is the second tier — definitional intros, answer-style headings, structured tables. Crawl tier is third — llms.txt, robots.txt access for AI bots, author byline. Foundation tier is the rest — HTTPS, title length, meta description, H1, lang attribute, Open Graph, JSON-LD presence. The first three tiers are where AEO diverges from SEO. The fourth tier is shared.

## The 15 signals in order of impact

The list, weighted highest-impact first. Each signal has a single mechanical fix and a verification step. A real-page AEO scanner grades all fifteen in 60 seconds — the score is the weighted sum of pass / warn / fail outcomes.

1. FAQPage JSON-LD — 5–8 real Q/A pairs in structured data at the bottom of the page.
2. Article or BlogPosting JSON-LD — gives extractors the headline, author, datePublished, articleBody fields they look for.
3. Definitional first paragraph — 30–90 words, directly answers the page topic in plain English.
4. llms.txt at site root — a five-line markdown file at /llms.txt indexing your most important pages.
5. AI-bot robots.txt access — GPTBot, ChatGPT-User, ClaudeBot, PerplexityBot, Google-Extended, Cohere-AI allowed.
6. Author byline — author microdata, rel="author", or.
7. Answer-style H2/H3 headings — phrased as the literal question a user would type.
8. Structured tables — markup for comparisons, specs, feature breakdowns.
9. Any JSON-LD on the page — even if not FAQPage or Article, signals structured-data readiness.
10. HTTPS — non-negotiable in 2026.
11. Title length 30–60 characters — descriptive, keyword-front-loaded.
12. Meta description 80–160 characters — concrete, written for humans first.
13. Exactly one H1 — matches the page intent and the title.
14. Lang attribute on — tells AI crawlers what language the page is in.
15. Open Graph tags — og:title, og:description, og:image.

That is the whole list. There are not fifty signals that matter in 2026 — there are fifteen, ranked by structural impact on citation extraction. Anyone selling a "200-point AEO audit" is mostly counting the same signal in fifteen different ways.

## Schema tier: FAQ, Article, JSON-LD

Schema is the highest-leverage layer in AEO because the AI extraction pipeline parses JSON-LD before it parses prose. FAQPage and Article schema together give the extractor a pre-structured view of your page that does not require it to re-derive structure from HTML. The model arrives with the entities, dates, authors, questions and answers already labeled. Pages without schema force the extractor to infer all of that, and inference is lossy.

### FAQPage schema — the single highest-impact AEO signal

FAQPage JSON-LD is the most consequential signal in the entire checklist. The pattern is mechanical: 5–8 real questions a user might ask about the page topic, with full answers in 40–100 words each, wrapped in FAQPage / Question / Answer schema. The questions should match the literal phrasing users type into ChatGPT, not paraphrased versions. Tools like AlsoAsked, AnswerThePublic and the People-Also-Ask box on Google are the best raw sources.

Why this matters more than it used to: Google deprecated FAQ rich snippets in 2023. Most SEOs stopped shipping FAQPage schema. AI engines did not stop reading it. The result is a measurable signal asymmetry — pages with FAQPage schema have less competition for the citation slot than they used to, and the schema is what gets the page parsed cleanly. The fix is to ship FAQPage schema on every content page that has more than one possible reader question.

### Article or BlogPosting schema

Article schema is the second piece. It tells the extractor what the page is, who wrote it, when it was published, when it was updated, what the headline is, and what counts as the article body. Without it, the extractor has to guess from HTML heuristics — and guesses badly on pages with sidebars, related-content grids, comment sections, and ad units cluttering the DOM. With Article schema, the body is explicit.

The required fields are headline, author (with @type Person and a name), da
