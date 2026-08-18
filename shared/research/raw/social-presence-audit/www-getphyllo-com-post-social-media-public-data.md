<!--
URL: https://www.getphyllo.com/post/social-media-public-data
Fetch date: 2026-08-18
Source type: vendor blog
Research cluster: social-presence-audit
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# Social Media Public Data: What You Actually Get
URL: https://www.getphyllo.com/post/social-media-public-data
Published: 2026-08-11
Author: Ronak Shah, Growth at Phyllo

Content current as of July 2026, per the source's own statement.

## What counts as social media public data?

Anything visible without authentication. The practical test given: open a private browser window, visit the profile, and whatever is visible is public data. Whatever is not visible is not public data, "and no vendor changes that."

Three broad categories, across platforms generally:

| Category | Examples | Useful for |
| --- | --- | --- |
| Profile data | Username, name, bio, profile picture, website, follower and following counts, post count | Discovery, screening, competitor benchmarking |
| Post data | Caption, hashtags, media type, media URL, permalink, timestamp, public like and comment counts, Reels view count | Content analysis, campaign tracking, social listening |
| Derived metrics | Likes per post, comments per post, engagement rate, posting frequency, caption length | Ranking and filtering, trend analysis |

Explicitly named as NOT on the public list: impressions, reach, saves, shares, profile visits, and audience breakdown. Every metric the source says a brand actually uses to judge a campaign performance sits behind the account holder's own login.

## Instagram's three official public-data surfaces (each narrower than its name suggests)

### Surface 1: Hashtag Search (Meta's formal name: Instagram Public Content Access)

Enumerated allowed uses only: discovering content tied to a hashtag campaign, understanding public sentiment around a brand, identifying contest/sweepstakes entrants, customer support, audience management.

Gated behind the `instagram_basic` permission plus the Instagram Public Content Access feature, both granted through Meta App Review, plus business verification, and possibly additional signed contracts.

| Limit | Detail |
| --- | --- |
| Unique hashtags | 30 per rolling 7-day period, per Instagram Business or Creator account |
| Recency | Returns only media published within 24 hours of the query |
| Pagination | Maximum 50 results per page, cursor-based |
| Usernames | Cannot be requested as a field; the API returns the post, not the poster |
| PII | Responses contain no personally identifiable information |
| Stories | Not supported for hashtag search |
| Emojis | Emoji hashtags not supported |
| Sensitive terms | Hashtags Meta deems sensitive/offensive return a generic error |
| Writes | Cannot comment on hashtagged media discovered this way |

The username restriction is called out as reshaping what products can be built on this surface: it supports a hashtag feed, volume measurement, and caption sentiment analysis, but not creator discovery, because the API will not identify whose post is whose.

### Surface 2: Business Discovery

The only official route to read another account's public profile data. Two conditions commonly missed: it requires the auditor's OWN authenticated Instagram Business account and access token (so "no authentication" is never actually true even for this "public" surface), and the TARGET account must itself be a Professional account (Business or Creator); personal accounts return nothing at all through this surface.

### Surface 3: oEmbed

Returns embed HTML for a public post or Reel. Useful for displaying content on a third-party site, not a data source, and should not be confused with an API.

## The five things no public source returns, regardless of platform or vendor

| Missing | Why | What people substitute, and the risk |
| --- | --- | --- |
| Impressions and reach | Rendered only inside the creator's own analytics | Estimated reach modelled from followers and engagement; fine if labelled as an estimate, misleading if resold as measured |
| Audience demographics | Released to the account owner only | Inferred demographics from follower sampling; directionally useful, not defensible as fact |
| Stories performance | Expires in 24 hours, never publicly archived | Nothing substitutes; public data has no Stories layer at all |
| Saves, shares, profile visits | Private engagement signals | Likes and comments used as a proxy, which misses the formats that actually drive discovery |
| Earnings and monetisation | Never rendered on any public surface | Rate-card estimates only; no public source holds real payout data |

The source frames this as "a structural boundary, not a difficulty curve": no amount of scraping sophistication or vendor cleverness closes this gap through Meta's own official surfaces, because Meta deliberately does not expose these fields to anyone but the account holder.

## Practical mapping for an unauthenticated Instagram audit

Even Meta's own "public" API surfaces (Hashtag Search, Business Discovery) require the auditor to hold their own authenticated Instagram Business account and token; there is no purely anonymous, zero-authentication official API path to another account's data on Instagram. A genuinely unauthenticated audit (a plain browser visit to a public profile, matching what this plugin's own no-login default path would see) is limited to whatever the source's "private browser window" test surfaces: profile data (username, bio, follower/following counts, post count) and the visible post history (captions, visible like/comment counts, media). Engagement RATE as opposed to raw counts, and anything in the "five things" table above, requires the account's own authenticated analytics view, which is exactly the class of data this plugin's per-platform opt-in prompt is designed to gate.

## Gaps in the archived fetch

The archived text is cut off partway through the "What do the calls actually look like?" section (a code sample for the Hashtag Search two-step resolve-then-read flow), before it reaches any equivalent code sample or field list for the Business Discovery surface, and before any discussion of Facebook or LinkedIn equivalents (this source is Instagram-specific throughout the surviving text).
