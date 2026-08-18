<!--
URL: https://junto.fr/en/blog/cro-audit
Fetch date: 2026-08-18
Source type: vendor blog
Research cluster: visual-funnel-audit
Archived by: forge stage 2 sweep round 2 (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., covering the 8 pairs left uncovered by round 1.
-->

# CRO Audit Framework: 4 Steps Before You Touch a Page
URL: https://junto.fr/en/blog/cro-audit
Published: 2026-08-10

CRO Audit Framework: 4 Steps Before You Touch a Page

# CRO Audit: The Framework We Run Before Touching a Page

Etienne Alcouffe Monday, August 10, 2026

A practitioner CRO audit framework: verify your data first, research real user behavior, map friction by funnel stage, and prioritize what to test.

Questions?

Most conversion audits start in the wrong place: on the page. Someone screenshots the homepage, annotates it with best-practice violations, and delivers the result as a CRO audit. The button color gets debated. The real problems — a checkout that double-counts transactions, a form that mobile users abandon at the same field every time, a value proposition that answers a question nobody asked — never make it into the document.

This is the CRO audit framework we run before recommending a single change to a page. It follows a fixed order for a reason: each stage depends on the one before it. Skip the first step and everything downstream becomes guesswork with charts attached.

## What a CRO Audit Actually Covers

A conversion rate optimization audit is a structured diagnosis of why visitors who could convert don't. Done properly, it answers four questions in sequence:

1. Can the data be trusted?
2. What are users actually doing, and what do they want?
3. Where, exactly, does the funnel lose them?
4. Which fixes deserve effort first?

Notice what's missing from that list: opinions about design trends, a screenshot tour of competitor sites, heuristics applied without evidence. Those things can inform an audit. They cannot replace one. An audit that opens with "add trust badges" before anyone has verified that the analytics counts orders correctly is decoration, not diagnosis.

The output is not a redesign brief either. It is a prioritized backlog of testable hypotheses, each tied to evidence, each with a clear way to measure whether the change worked. More on that at the end.

## Step One: The Analytics Trust Check

Every audit starts with an uncomfortable question: is the data telling the truth? The answer is no more often than anyone likes to admit, which is why skipping this step invalidates everything that follows. If your conversion rate is computed from broken inputs, every heatmap insight and every funnel analysis inherits the error.

The checks worth running before anything else:

- Conversion definitions. What counts as a conversion, and does everyone agree? A "lead" that includes newsletter signups tells a different story than one restricted to demo requests. Ambiguity here poisons prioritization later.
- Duplicate and phantom events. Purchase events that fire on page refresh, form submissions counted twice by competing tags, thank-you pages reachable from old email links. Each one inflates the numerator.
- Consent and data loss. Since consent banners became standard, a meaningful share of sessions is simply invisible to analytics, and the invisible share is not randomly distributed. If your consent setup is misconfigured, you may be optimizing for the subset of users who click "accept" fastest. The compliance side of this has its own traps, covered in detail in this guide to GDPR and marketing.
- Cross-domain and payment redirects. Checkouts that pass through a payment provider and return often break session attribution, making your best channel look like "referral: stripe.com".
- Back-office reconciliation. The single most revealing test: do analytics transactions match the order database? If the gap is large or unstable, fix measurement before touching conversion.

This step regularly changes the entire diagnosis. When we rebuilt the measurement layer for Les cours de Julie, an online learning platform, the opt-in rate was multiplied by seven, tracked conversions rose 34%, and tracking data finally aligned 100% with the back office. The site had not changed. The picture of the site had. Any audit run on the old data would have hunted for a conversion problem that was actually a measurement problem.

If your tracking has never been formally validated, treat that as the first deliverable of the audit, not a footnote. It is the core of what a web analytics agency does before any optimization work begins.

## Step Two: Research — What Users Do, and Why

With trustworthy numbers, the next layer is behavioral. Analytics tells you where people leave; it rarely tells you why. That gap is filled by three complementary sources.

### Heatmaps and scroll maps

Heatmaps show attention, not intent, so read them for anomalies rather than confirmation. The patterns that matter: clicks on elements that are not clickable (users expect something there), heavy interaction with elements that lead nowhere useful, and scroll maps showing that the content answering the visitor's main objection sits below the point where most people stop. A pricing answer at 80% scroll depth on a page where attention dies at 50% is a finding. A hot spot on your main CTA is not.

### Session replays

Replays are the closest thing to sitting behind the user. The discipline is sampling: watch sessions filtered to a specific failure, such as visitors who reached checkout and left, or mobile users who spent more than a minute on the form. Watching random sessions produces anecdotes. Watching failure cohorts produces patterns: the coupon field that sends people off-site to hunt for codes, the error message that appears off-screen on mobile, the date picker that resets on validation errors.

### User intent

The most underused research source is what visitors say and search. On-site search queries reveal vocabulary gaps between your navigation and your customers' heads. Post-purchase or exit surveys, even with modest response counts, surface objections no heatmap can show. Support tickets and sales-call notes tell you which questions the site fails to answer. If visitors keep asking about delivery times in chat, the funnel has a delivery-time problem regardless of what the click data says.

Intent research also protects you from a classic audit failure: optimizing a page for the wrong job. A landing page receiving comparison-stage traffic from ads needs different content than the same page receiving brand traffic, which is why serious conversion work always looks at traffic sources alongside page behavior.

## Step Three: The Friction Inventory, Stage by Stage

Now, and only now, does the audit look at pages. The method is a systematic walk through the funnel, logging every point of friction against the evidence gathered in step two. Working stage by stage keeps the inventory honest: it forces attention onto the steps where drop-off is measured, not the pages that are most fun to critique.

For an e-commerce funnel, the stages typically break down like this:

- Entry. Does the landing experience match the promise that brought the visitor? Message mismatch between ad and page is one of the most common and most fixable sources of bounce.
- Discovery. Category pages, filters, on-site search. Can a vi
