<!--
URL: https://patrickstox.com/technical-seo/on-page/structured-data/commerce/product-schema/
Fetch date: 2026-08-18
Source type: community post
Research cluster: ecommerce-catalog-audit
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# Product Schema

URL: https://patrickstox.com/technical-seo/on-page/structured-data/commerce/product-schema/
First published: 2026-06-27. Last updated: 2026-07-18. Level: Advanced.
Author: Patrick Stox (individual technical SEO practitioner site)

How to implement schema.org/Product markup for Google's product snippet and merchant listing rich results: required vs. recommended properties, the availability enum, why Product schema isn't the same as a Merchant Center feed, and how to fix common Search Console errors.

Summary: Product markup (usually JSON-LD) makes a product page eligible for two distinct Google experiences: product snippets (price/reviews on any product page, `priceCurrency` only recommended, `price: 0` allowed) and merchant listings (transactional pages, requiring `image`, `offers`, and a `price` greater than 0 with `priceCurrency`). Minimum for a product snippet: `name` plus at least one of `offers`/`review`/`aggregateRating`. A merchant listing needs `offers` outright, not as one option among three. The biggest trap is conflating this on-page markup with a Google Merchant Center feed, a separate system with a separate validator; Google reconciles them, and price/availability must match across markup, feed, and checkout, or Google flags a mismatch. Valid markup only earns eligibility; Google's systems still decide whether to show the result.

Evidence cited by the source: "For the current product-snippet feature, Product requires name plus at least one of review, aggregateRating or offers." (Scope: product snippets. Confidence: high. Verified: 2026-07-16, against Google's product snippet structured-data documentation.)

## What Product schema does: two experiences, not one

Google splits Product markup into two rich-result experiences with different strictness:

- Merchant listings: for pages where the product can be purchased directly, emphasizing full shopping details (price, availability, shipping, returns). Stricter requirements.
- Product snippets: for non-transactional or general product pages, emphasizing reviews and price. Lighter requirements.

Google's own framing, as quoted by the source: "Two markup types exist: Product snippets for non-purchase pages, emphasizing reviews, and Merchant listings for purchase pages, highlighting product details like sizing and shipping." Same `schema.org/Product` vocabulary underneath; the difference is which properties Google requires for each. Passing generic schema.org validation does not by itself establish Google rich-result eligibility, because schema.org defines the vocabulary while Google separately defines which properties it supports and requires for each experience.

Scoping rule, quoted from Google: "product rich results only support pages that focus on a single product (or multiple variants of the same product)." A category page ("shoes in our shop") is not a product; for a line of variants, use `ProductGroup` markup instead.

## Required vs. recommended properties

Minimum for a product snippet (Google's lighter experience): `Product.name`, plus at least one of `offers`, `review`, or `aggregateRating`. That "one of three" flexibility is specific to product snippets. A merchant listing always needs `offers`; Google's own required-property table lists `name`, `image`, and `offers` as required, full stop, with no either/or.

Product level:

| Property | Product snippet | Merchant listing |
| --- | --- | --- |
| `name` | Required | Required |
| `image` | Recommended | Required |
| `offers` | (one of offers/review/rating) | Required |
| `description` | Recommended | Recommended |
| `sku` | Recommended | Recommended |
| `gtin`/`mpn` | Recommended | Recommended |
| `brand` | Recommended | Recommended (`brand.name`) |
| `aggregateRating` | Recommended | Recommended |
| `review` | Recommended | Recommended |

Offer level (`offers`, an `Offer` object):

| Property | Product snippet | Merchant listing |
| --- | --- | --- |
| `price` | Required (`0` allowed for free items) | Required (must be > 0) |
| `priceCurrency` | Recommended | Required |
| `availability` | Recommended | Recommended |
| `priceValidUntil` | Recommended | Recommended |
| `itemCondition` | Recommended | Recommended |
| `hasMerchantReturnPolicy` | (not listed) | Recommended |
| `shippingDetails` | (not listed) | Recommended |
| `url` | Recommended | Recommended |

The two rules the source flags as most commonly missed: for merchant listings, "merchant listing experiences require a price greater than zero" (product snippets tolerate `0`); and `priceCurrency` is required for merchant listings but only "currently recommended" for basic product snippets.

Required/recommended split verified directly by the author against Google's Product snippet and Merchant listing structured-data documentation as of 2026-07-18; the author notes these tables can change and should be rechecked against the live Google pages before relying on them for a launch.

[Fetch truncated here; the source's sections on the `availability` enum, the Product-vs-Merchant-Center-feed distinction, common Search Console errors, and validation steps were referenced in the summary and evidence blocks above but their full body text was not captured in this fetch.]

Cross-reference: this source's required/recommended split for merchant listings (name, image, offers required; description/sku/gtin/mpn/brand recommended) matches and corroborates the split already recorded from a prior-archived Anglera source in this cluster (`raw/www-anglera-com-blog-enriched-data-to-page-checklist.md`), giving that split two independent sources rather than one.
