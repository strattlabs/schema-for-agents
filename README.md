# schema-for-agents

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE) · [strattlabs.com](https://strattlabs.com)

A copy-paste **cookbook of JSON-LD recipes** that make commerce and content sites
legible and citable to AI agents and answer engines — plus (planned) a small
validator that flags the omissions that most often break structured data.

`schema.org` is vast and easy to get subtly wrong. This repo is a focused,
opinionated subset: the handful of types that actually move the needle for
agent/AI-engine legibility, written correctly, ready to adapt.

> **Status:** scaffold / v0. The recipes below are real and usable today. The
> validator is specified here and not yet built — see [Roadmap](#roadmap).

## What's here

Ready-to-adapt recipes in [`recipes/`](recipes/):

| Recipe | Type | Use it for |
| ------ | ---- | ---------- |
| [`product-offer.jsonld`](recipes/product-offer.jsonld) | `Product` + `Offer` | Product pages: name, price, availability, currency. |
| [`service.jsonld`](recipes/service.jsonld) | `Service` + `Offer` | Bookable / mail-in services with a price and area served. |
| [`faqpage.jsonld`](recipes/faqpage.jsonld) | `FAQPage` | Q&A blocks agents can quote directly. |
| [`breadcrumblist.jsonld`](recipes/breadcrumblist.jsonld) | `BreadcrumbList` | Site hierarchy and where a page sits in it. |
| [`article-author.jsonld`](recipes/article-author.jsonld) | `Article` + named `Person` | Authored content with `sameAs` identity + freshness dates. |
| [`organization.jsonld`](recipes/organization.jsonld) | `Organization` | Entity authority: `sameAs` links, logo, contact point. |

See [`recipes/README.md`](recipes/README.md) for field-by-field notes on each.

## How to use a recipe

1. Copy the recipe's JSON.
2. Replace the placeholder values (`acme.example.com`, prices, names) with yours.
3. Embed it in the page `<head>` (or before `</body>`) inside a script tag:

```html
<script type="application/ld+json">
  { "@context": "https://schema.org", "@type": "Product", "...": "..." }
</script>
```

One JSON-LD block per logical entity. Keep the data consistent with what's visible
on the page — agents and answer engines penalize structured data that disagrees
with the rendered content.

## Why this matters for agents

Agents and AI answer engines lean on structured data to understand *what* a page
is about and *whether they can trust it*. The recipes here target the signals that
matter most:

- **Commerce legibility** — `Product`/`Offer`/`Service` make price, availability,
  and currency machine-readable instead of buried in markup.
- **Citability** — `FAQPage` and authored `Article` markup give engines clean,
  attributable snippets to quote.
- **Identity & authority** — named `Person` authorship and `Organization.sameAs`
  connect your content to known entities, which is exactly the entity-graph signal
  answer engines use to decide who to cite.
- **Freshness** — `dateModified` tells engines the content is current.

## What this is

This repo is **pure, public `schema.org`**: copy-paste JSON-LD recipes that help a
site *declare* structured data about itself. It pairs naturally with the
[agent-readiness-manifest](../agent-readiness-manifest) declaration spec.

## Roadmap

The planned `schema-for-agents` validator (Node/TS, pnpm) will lint embedded or
standalone JSON-LD for the omissions we see most often:

- missing `@context` / `@type`;
- `Offer` without `priceCurrency` or `availability`;
- `Article` without `dateModified` or a named `author`;
- `Organization` / `Person` without `sameAs`;
- `BreadcrumbList` items missing `position` or `item`;
- structured-data values that contradict the visible page (best-effort).

It will be **advisory**: it recommends the fix and links to the recipe. Until
then, the recipes stand alone.

## License

[MIT](LICENSE) © 2026 Stratt Labs. The recipes are meant to be copied freely.

---

## Part of the Stratt Labs toolkit for the agentic web

Small, standards-friendly tools from [Stratt Labs](https://strattlabs.com):

- [agent-readiness-manifest](https://github.com/strattlabs/agent-readiness-manifest)
  — an open declaration spec for agent discovery.
- [llms-txt-kit](https://github.com/strattlabs/llms-txt-kit) — generate and
  validate `llms.txt` / `llms-full.txt` files.
- [webmcp-starter](https://github.com/strattlabs/webmcp-starter) — a minimal
  WebMCP reference page.
