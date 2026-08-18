<!--
URL: https://craftshift.com/shopify-product-page-30-point-audit-2026/
Fetch date: 2026-08-18
Source type: vendor/community blog
Research cluster: ecommerce-catalog-audit
Archived by: forge stage 2 sweep round 2 (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., covering the 8 pairs left uncovered by round 1.
-->

# Shopify product page: a 30-point audit for 2026 (the complete checklist) - Craftshift
URL: https://craftshift.com/shopify-product-page-30-point-audit-2026/
Published: 2026-05-06
Author: Umid

Shopify product page: a 30-point audit for 2026 (the complete checklist) - Craftshift

Most Shopify product pages have ten things wrong with them and none of them are obvious. The cover image is fine. The price reads correctly. The Add to Cart works. The store still under-converts because the variant selector is a dropdown, the alt text on every image says “IMG_4521,” the page is rendering 800 KB of unnecessary CSS, the JSON-LD is malformed, and AI agents like ChatGPT cannot tell that this product comes in five colors. None of it shows up on a casual look. All of it costs sales.

This is the 2026 audit we run when a merchant asks “what should I fix on my product page?” Thirty specific checks across seven categories, with the actual fix path for each (theme setting, app, custom code, or a flag in your sitemap). Run it once. Re-run quarterly. The compounding from 30 small fixes is the difference between a 1.5% conversion rate and a 3%.

This expands on our shorter 15-point optimization checklist and adds the items that became important in 2026: AI agent visibility, llms.txt, Agentic Storefronts, and structured data signals AI search engines now use. We cite our specific app where it solves a checklist item and stay app-neutral elsewhere.

## In this post

- How to run this audit
- Images and gallery (1 to 6)
- Variants and swatches (7 to 12)
- Product copy and content (13 to 17)
- Trust signals and reviews (18 to 21)
- Technical SEO and performance (22 to 26)
- AI search and agentic commerce (27 to 30)
- Quick-wins vs investments
- Frequently asked questions
- Related reading

## How to run this audit

1. Pick three product pages: a top seller, a mid-tier product, and a long-tail one. The differences between them surface bigger patterns than any single page.
2. Open each in incognito on both desktop and mobile.
3. Run through the 30 checks below. Mark each as Pass, Fail, or Skip-not-applicable.
4. Tally the failures. Fix the ones in the “quick win” tier first; plan the rest.

Budget 60 to 90 minutes for the first run. Subsequent quarters take 30 minutes once you know your weak spots.

## Images and gallery (1 to 6)

### 1. At least 5 images per product

Front, back, detail close-up, scale reference, lifestyle. Five is the floor. More is fine; less is leaving conversion on the floor. Source dimensions of 2048 x 2048, file size 100 to 300 KB after compression. Reference: Shopify product image size guide.

### 2. Each variant has at least one variant-specific image

When a customer selects “Black,” the gallery should lead with a black product photo. Not the cover image, not the white version. Check this on every variant. Shopify natively supports one image per variant.

### 3. Multiple images per variant for premium products

Lifestyle plus on-white plus detail per color. Shopify natively supports only one image per variant; for multi-image-per-variant, an app like Rubik Variant Images handles per-variant media groups, including videos and 3D models.

### 4. Every image has descriptive alt text

“Navy oversized hoodie front view” passes. “IMG_4521” or empty string fails. Alt text feeds SEO, Google Shopping, AI agent surfacing, and accessibility. Sample 10 images randomly; if more than two have weak alt text, audit the whole catalog.

### 5. Image zoom works and resolves to high-detail

Click or hover, see a clear zoom up to 2048+ pixels. If zoom is missing or pixelated, your source images are too small (Shopify activates zoom only above 800 x 800), or your theme zoom is broken. Premium fashion specifically benefits from a dedicated zoom app. Reference: premium fashion stack.

### 6. No oversized images causing slow loads

Source images above 5000 x 5000 (Shopify’s 25 MP product cap) get rejected outright; sources between 2048 and 4500 are accepted but render slow on mobile. Aim for 2048 x 2048 source. Reference: 25 MP image limit fix.

## Variants and swatches (7 to 12)

### 7. Color swatches instead of dropdowns

Color is visual; the variant picker should be too. Visual swatches reduce clicks, improve mobile UX, and outperform text dropdowns on conversion in nearly every measured study. If your theme renders Color as a dropdown, switch to swatch in the variant picker block settings (or use an app if your theme does not support it).

### 8. Swatches use real product colors, not auto-detected names

“Forest Green” should render as the actual hex code of your forest green fabric, not a generic CSS green. Map every custom color name to a real hex (or upload a fabric thumbnail) under your theme’s swatch settings.

### 9. Out-of-stock variants are clearly marked or hidden

Strikethrough or full hide. Either is fine; ambiguous (greyed without strikethrough or with no indicator at all) confuses customers. If your theme auto-selects a sold-out variant by default, fix that immediately because the customer lands on a greyed Add to Cart and bounces.

### 10. Separate-product-per-color setups linked via combined listings

If you have “Sarah Bra Black” and “Sarah Bra Olive” as separate Shopify products, link them as one shoppable group. Improves both UX and AI agent surfacing. Reference: variant grouping and AI shopping discovery. Rubik Combined Listings handles this on every plan.

### 11. Default variant is the first available, not the first in order

Shopify’s`product.selected_or_first_available_variant` Liquid object returns the first in-stock variant. Some themes use`product.variants[0]` instead, which lands customers on a sold-out variant. Check the relevant Liquid in your theme; switch to the first-available form if needed.

### 12. Size or fit guidance accessible from the page

Apparel, footwear, and accessories all benefit from a size chart or fit recommender on the product page (modal, expandable section, or inline). Returns drop measurably; conversion improves on the first visit. Reference: premium fashion stack.

## Product copy and content (13 to 17)

### 13. Product title contains the buyer’s likely search term

“Sarah Bra” is a brand-internal name. “Sarah High-Support Sports Bra” is what customers search. Pair brand name with category and key attribute in the title. Read our product title SEO guide.

### 14. Description leads with concrete specifications

“40L waterproof hiking backpack with laptop compartment” beats “Adventure Day Pack.” Marketing fluff at the top of the description loses both human readers and AI agents. Lead with materials, dimensions, key features. Personality copy can come below.

### 15. Returns, shipping, and care info on the product page

Customers want to know before buying, not after. An expandable section or accordion with shipping cost, delivery window, return window, and care instructions raises conversion and reduces support tickets.

### 16. Specs are in standardized fields, not free text

Use Shopify metafields (or your theme’s spec fields) for material, dimensions, weight, country of origin. AI agents and Google Shopping pick these up re
