# Recipe notes

Field-by-field guidance for each recipe. JSON-LD does not allow comments, so the
notes live here. Replace every placeholder value (`acme.example.com`, prices,
names, IDs) with your own, and keep the data consistent with the visible page.

## `product-offer.jsonld` — `Product` + `Offer`

- `name`, `description`, `sku`, `brand`, `image`, `url` — describe the product.
- `offers.price` is a **string**; `offers.priceCurrency` is an ISO 4217 code.
- `offers.availability` uses a schema.org URL (`InStock`, `OutOfStock`,
  `PreOrder`, …).
- `offers.priceValidUntil` signals freshness; keep it in the future.

## `service.jsonld` — `Service` + `Offer`

- For bookable or mail-in services. `provider` ties the service to your org.
- `areaServed` can be a `Country`, `State`, `City`, or `GeoCircle`.
- Include an `offers` block when the service has a fixed price.

## `faqpage.jsonld` — `FAQPage`

- Each `mainEntity` item is a `Question` with exactly one `acceptedAnswer`.
- Only mark up Q&A that is **actually visible** on the page.
- `answer.text` may contain limited HTML; keep it short and quotable.

## `breadcrumblist.jsonld` — `BreadcrumbList`

- `position` is 1-based and must be sequential.
- Every `item` should be an absolute URL.
- Mirror the breadcrumb the user actually sees.

## `article-author.jsonld` — `Article` + named `Person`

- Prefer a named `Person` author over a bare string — it connects to an identity.
- `author.sameAs` should point to authoritative profiles (LinkedIn, GitHub, ORCID).
- Set both `datePublished` and `dateModified`; update `dateModified` on real edits.
- `publisher` carries the org + logo for engines that surface attribution.

## `organization.jsonld` — `Organization`

- `sameAs` is the highest-leverage field here: link to the profiles that establish
  your entity (LinkedIn company page, GitHub org, Wikipedia/Wikidata if present).
- `contactPoint` gives agents a machine-readable way to reach support.
- Publish this once, sitewide (e.g. on the homepage).
