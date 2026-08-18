<!--
URL: https://schema.org/Product
Fetch date: 2026-08-18
Source type: official docs
Research cluster: ecommerce-catalog-audit
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# Product - Schema.org Type

URL: https://schema.org/Product
Canonical URL: https://schema.org/Product
Equivalent Class: fibo-fnd-pas-pas:Product, unece:TradeProduct
Usage: 10M+ domains (Google, monthly aggregation, July 2026)

Definition: "Any offered product or service. For example: a pair of shoes; a concert ticket; the rental of a car; a haircut; or an episode of a TV show streamed online."

## Properties from Product (selected, as captured)

| Property | Expected Type | Description |
| --- | --- | --- |
| additionalProperty | PropertyValue | A property-value pair representing an additional characteristic of the entity, e.g. a product feature or another characteristic for which there is no matching property in schema.org. Publishers should be aware that applications designed to use specific schema.org properties (e.g. `width`, `color`, `gtin13`) will typically expect that data to be provided using those dedicated properties, not the generic property/value mechanism. |
| aggregateRating | AggregateRating | The overall rating, based on a collection of reviews or ratings, of the item. |
| asin | Text or URL | An Amazon Standard Identification Number (ASIN), a 10-character alphanumeric unique identifier assigned by Amazon.com and its partners for product identification within the Amazon organization. This is a definition for how to include ASINs in Schema.org data, not a definition of ASINs in general. |
| audience | Audience | An intended audience, i.e. a group for whom something was created. Supersedes `serviceAudience`. |
| award | Text | An award won by or for this item. Supersedes `awards`. |
| brand | Brand or Organization | The brand(s) associated with a product or service, or the brand(s) maintained by an organization or business person. |
| category | CategoryCode or PhysicalActivityCategory or Text or Thing or URL | A category for the item. Greater signs or slashes can be used to informally indicate a category hierarchy. |
| color | Text | The color of the product. |
| colorSwatch | ImageObject or URL | A color swatch image, visualizing the color of a Product. Should match the textual description specified in the `color` property. Can be a URL or a fully described ImageObject. |
| countryOfAssembly | Text | The place where the product was assembled. |
| countryOfLastProcessing | Text | The place where the item (typically Product) was last processed and tested before importation. |
| countryOfOrigin | Country | The country of origin of the product (interpretation varies by context and product type). |
| depth | Distance or QuantitativeValue | The depth of the item. |
| displayLocation | Place | The location at which an item can be viewed or experienced in-person. |
| funding | Grant | A Grant that directly or indirectly provides funding or sponsorship for this item. |
| gtin | Text or URL | A Global Trade Item Number (GTIN). GTINs identify trade items, including products and services, using numeric identification codes. A correct `gtin` value should be a valid GTIN: an all-numeric string of 8, 12, 13, or 14 digits, or a "GS1 Digital Link" URL based on such a string, with a valid GS1 check digit. Left-padding of gtin values is not required or encouraged. The `gtin` property generalizes the earlier `gtin8`, `gtin12`, `gtin13`, and `gtin14` properties. |
| gtin12 | Text | The GTIN-12 code: a 12-digit GS1 Identification Key composed of a U.P.C. Company Prefix, Item Reference, and Check Digit. |
| gtin13 | Text | The GTIN-13 code, equivalent to 13-digit ISBN codes and EAN UCC-13. Former 12-digit UPC codes can be converted to GTIN-13 by adding a preceding zero. |
| gtin14 | Text | The GTIN-14 code. |
| gtin8 | Text | The GTIN-8 code, also known as EAN/UCC-8 or 8-digit EAN. |
| hasAdultConsideration | AdultOrientedEnumeration | Used to tag an item as intended or suitable for consumption or use by adults only. |
| hasCertification | Certification | Certification information about a product, organization, service, place, or person. |
| hasEnergyConsumptionDetails | EnergyConsumptionDetails | Defines the energy efficiency category ("class"/"rating") for a product per an international energy-efficiency standard. |
| hasGS1DigitalLink | URL | The GS1 digital link associated with the object. Should only contain the Application Identifiers (AIs) relevant to the entity and the correct granularity (e.g. a serial-number AI `21` link should only be present on `IndividualProduct` instances). |

[Fetch truncated here; the remainder of the Product property table (hasMeasurement, hasMerchantReturnPolicy, itemCondition, keywords, mobileUrl, model, offers, positiveNotes, productID, size, additionalType, identifier, itemOffered, and inherited Thing/CreativeWork properties) was captured in part in an earlier archived source but not re-verified line-by-line against the live page in this fetch; treat the field list above as authoritative for the fields shown, and defer to the live schema.org/Product page for any field not listed here.]

Note on authority: this is schema.org's own canonical type definition and is the ultimate source of truth for what a `Product` property means and what type it expects. It does NOT state which properties Google requires for a given rich-result feature (product snippet vs. merchant listing); that eligibility layer is defined separately by Google Search Central (see the patrickstox.com and prior-archived Anglera sources in this cluster for the required/recommended split Google applies on top of this vocabulary).
