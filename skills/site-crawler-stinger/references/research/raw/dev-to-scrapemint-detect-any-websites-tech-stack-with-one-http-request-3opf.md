<!--
URL: https://dev.to/scrapemint/detect-any-websites-tech-stack-with-one-http-request-3opf
Fetch date: 2026-08-18
Source type: community post
Research cluster: platform-fingerprinting
Archived by: forge stage 2 sweep (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc. build sequence step 6.
-->

# Detect Any Website's Tech Stack With One HTTP Request - DEV Community
URL: https://dev.to/scrapemint/detect-any-websites-tech-stack-with-one-http-request-3opf
Published: 2026-07-03

Detect Any Website's Tech Stack With One HTTP Request - DEV Community

BuiltWith charges $295 a month. Wappalyzer retired its open source rule set. But most tech stack detection needs exactly one HTTP request per site, no browser, and a signature list you can read in one sitting. Here is how it works.

## Three evidence channels

A single homepage response carries three independent signals:

1. The HTML. Vendors host their scripts on their own domains, and those URLs are unambiguous. If the page references`cdn.shopify.com`, it is a Shopify store. If it loads`js.hs-scripts.com`, HubSpot is installed. Frameworks leave globals and attributes:`__NEXT_DATA__` is Next.js,`__NUXT__` is Nuxt,`ng-version=` is Angular,`data-sveltekit` is Svelte.

2. The response headers. Hosting and CDN rarely show in HTML at all, but headers give them away:`cf-ray` is Cloudflare,`x-vercel-id` is Vercel,`x-nf-request-id` is Netlify,`x-amz-cf-id` is CloudFront,`x-served-by: cache-...` is Fastly. Platforms leak too:`x-shopify-stage`,`x-wix-request-id`,`x-powered-by: WP Engine`.

3. The cookies. Server languages hide behind proxies, but session cookie names survive:`PHPSESSID` is PHP,`laravel_session` is Laravel,`csrftoken` is Django,`ASP.NET_SessionId` is ASP.NET.

## Precision beats recall

The classic mistake is matching product names in page text, which flags every blog post that mentions WordPress as a WordPress site. The fix is to only match things that cannot appear in prose: vendor asset URLs, header names, cookie names, unique JavaScript globals. A signature like`/wp-content/` or`static1.squarespace.com` is boring and almost never wrong, and boring is what you want when each false positive pollutes a lead list.

```
const SIGNATURES = [
  { name: 'Shopify', category: 'ecommerce',
    html: ['cdn.shopify.com'], header: [['x-shopify-stage', '']] },
  { name: 'Next.js', category: 'framework',
    html: ['__next_data__', '/_next/static/'] },
  { name: 'Laravel', category: 'server', cookie: ['laravel_session'] },
];

```

Lowercase the HTML once, lowercase the header values once, and detection is a substring scan: about 100 signatures against 600KB of HTML runs in single digit milliseconds.

## What one request cannot see

Be honest about the blind spots. Tools loaded only on inner pages (a checkout-only payment SDK) will not show on the homepage. Fully client-rendered pages can hide HTML signatures, though headers and cookies still work. And sites behind aggressive bot protection will not respond at all, so record`reachable: false` and move on rather than retrying into a block.

## Why this beats a browser

A Playwright-based detector sees more (runtime globals, late-loaded scripts), but costs 100x the compute and gets blocked 10x as often. For the main commercial use case, segmenting lead lists by technology ("which of these 2000 domains run Shopify?"), the one-request version answers correctly for the overwhelming majority of sites at a price where the question is worth asking at scale.

## If you want it as a service

I packaged this as a pay per use actor: domains in, one JSON row per site out (CMS, ecommerce, analytics, marketing, framework, hosting, payments, with evidence), and you pay only for sites that yield detections: https://apify.com/scrapemint/website-tech-stack-detector

It is built to pair with a contact scraper on the same domain list: who to email from one, what they run from the other, joined on domain.

Are you sure you want to hide this comment? It will become hidden in your post, but will still be visible via the comment's permalink.

Hide child comments as well

Confirm

For further actions, you may consider blocking this person and/or reporting abuse

We're a place where coders share, stay up-to-date and grow their careers.

Log in Create account
