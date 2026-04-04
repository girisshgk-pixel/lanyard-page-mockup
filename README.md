# Badge-A-Minit — Polyester Lanyard Product Page Revamp

> **Status: Proposed Recommendations — Nothing implemented or live on badge-a-minit.com.au**
> This repository is a staging reference for developer handoff, stakeholder review, and QA planning only.

---

## 🔗 Live Preview Links

| Page | URL |
|------|-----|
| Product Page Mockup | [girisshgk-pixel.github.io/lanyard-page-mockup/](https://girisshgk-pixel.github.io/lanyard-page-mockup/) |
| Developer Implementation Notes | [girisshgk-pixel.github.io/lanyard-page-mockup/dev-notes.html](https://girisshgk-pixel.github.io/lanyard-page-mockup/dev-notes.html) |

---

## 📋 Project Overview

This repo contains a fully designed and annotated mockup for the revamp of the
[Polyester Lanyard (Silk Screen Printing)](https://badge-a-minit.com.au/product/polyester-lanyard-silk-screen-printing)
product page on **badge-a-minit.com.au** — part of a broader SEO and CRO uplift programme
targeting all product pages listed under `/products/lanyards`.

The work covers page layout, image gallery UX, structured data, on-page SEO, mobile-first responsiveness,
and a full developer notes document that justifies every proposed change with before/after code diffs.

**Prepared by:** Girish Kumar — E-Commerce SEO Manager
**Brand:** Badge-A-Minit (badge-a-minit.com.au)
**Date:** April 2026
**Scope:** `/products/lanyards` — product pages only

---

## 📁 Repository Files

```
/
├── index.html          ← Product page mockup (full proposed design)
├── dev-notes.html      ← Developer implementation notes (14 sections, 24 changes)
└── README.md           ← This file
```

---

## 🎯 What This Proposes (Summary)

### UX & Conversion Rate Optimisation
- **Sticky left panel** — product image, title, price, size/colour selector, and Order Now CTA fixed to viewport while content scrolls on the right (Amazon-style layout)
- **1080×1080 product image viewer** — vertical thumbnail strip (6 shots: wide, fabric, male mockup, female mockup, hook detail, logo close-up) with full-screen zoom modal on click
- **Live bulk price calculator** — slider from 100–2,000 units with real-time unit price, total, and savings display; volume discount banner reveals at 250+ units
- **8 colour swatches** — Green, Navy, Red, Black, Purple, Orange, Silver, Charcoal; updates main image, alt text, and title dynamically on selection

### SEO & Structured Data
- **6 JSON-LD schemas** added to `<head>`: BreadcrumbList, Product (with Merchant Centre fields), ItemList (all 8 SKU variants), FAQPage, LocalBusiness, ImageGallery
- **Critical Merchant Centre fix** — all 8 product variants now include `image`, `description`, `brand`, and `mpn` fields (was flagged as 1 critical + 4 non-critical errors per variant in Google Rich Results Test)
- **Full OG + Twitter/X card tags** — `og:type = "product"` with price, availability, and 1080×1080 image
- **Strict H1→H2→H3 heading hierarchy** — 1× H1 (product title), 11× H2 (section titles), 21× H3 (feature cards, step titles, FAQ questions)
- **FAQ questions in H3** + `aria-expanded` + `itemprop` microdata (belt-and-braces with JSON-LD FAQPage)
- **Dynamic canonical** — JS script strips UTM params, `fbclid`, `gclid`, `colour`, `width`, `side` before writing the canonical tag

### Programmatic Alt Text & Title
Every thumbnail and the main product image use the agreed format:
```
Alt:   "A wide-shot photo of [Product Name] placed on a white background
        for visual understanding. Explore and Buy Now from [Brand Name]."

Title: "Wide-Shot View of [Product Name] with a minimum order of [X] units
        starts at $[x.xx] per unit. Buy Now from [Brand Name]."
```
Both update dynamically via JS when the user switches shot type or colour.

### Mobile-First Responsive (5 Breakpoints)
| Breakpoint | Target | Key behaviour |
|---|---|---|
| 0–479px | iPhone SE, small Android | Single col, sticky bar on, header nav hidden |
| 480–767px | iPhone 14, Pixel 7 | Single col, thumbs vertical, sticky bar on |
| 768–899px | iPad Mini, tablets | Single col, no sticky bar |
| 900–1099px | 13" laptop | Two-col 380px/1fr, no sticky bar |
| 1100px+ | Desktop | Full 520px/1fr sticky grid |

**Mobile sticky order bar** (fixed bottom, mobile only): product thumbnail · product name · units selected · live unit price · **Order Now** button — syncs live with sidebar calculator state. Uses `env(safe-area-inset-bottom)` for iPhone home indicator clearance.

### Meta & Robots
```html
<!-- Staging: noindex/nofollow with full SERP preview -->
<meta name="robots" content="noindex, nofollow,
  max-snippet:-1, max-image-preview:large, max-video-preview:-1">
```
> ⚠️ Change to `index, follow` before production deployment. Keep max-preview directives.

### Minimum Order Quantity
Updated throughout page copy, schema, and calculator to **250 units**.

---

## 🏗️ URL Architecture Decision — Colour & Option Variants

Two approaches documented. **Option 1 is proposed as default.**

### Option 1 — Query Parameters + Canonical Strip ✅ Default
```
/product/polyester-lanyard-silk-screen-printing?colour=green&width=1cm&side=single
```
The dynamic canonical script strips `colour`, `width`, `side`, and `variant` parameters
so Google always indexes the clean base URL. Zero duplicate content risk.
Colour and option data is communicated via the `color` and `size` fields in Product schema.

### Option 3 — Separate Colour URLs 🔭 Future (if search demand warrants)
```
/product/polyester-lanyard-silk-screen-printing/green
/product/polyester-lanyard-silk-screen-printing/navy-blue
```
Upgrade only when GSC shows 100+ monthly impressions for colour-specific queries
**and** unique photography per colour is available. Each colour page requires its own
Product schema, ImageGallery, FAQPage additions, and canonical.

---

## 📝 Developer Implementation Notes

The `dev-notes.html` file is a full developer handoff document with **14 sections and 24 proposed changes**,
each presented as a two-column card: justification notes on the left, before/after HTML/CSS/JS code diffs on the right.

### Sections covered

| # | Section | Key Decision |
|---|---------|-------------|
| 1 | Page Layout | Sticky panel + scrollable content grid |
| 2 | Image Gallery | 1080×1080 viewer, vertical thumbs, 6 shot types |
| 3 | Alt & Title Text | Programmatic per-shot format, JS-updated on switch |
| 4 | Heading Hierarchy | H1→H2→H3, FAQ questions in H3 |
| 5 | Bulk Calculator | Live pricing engine, savings trigger |
| 6 | Structured Data | 6 JSON-LD schemas |
| 7 | OG + Twitter Tags | `og:type = "product"` with price/availability |
| 8 | Robots & Canonical | noindex staging + dynamic canonical script |
| 9 | Merchant Listings | Critical error fix — image/description/brand per variant |
| 10 | FAQ Schema | H3 + JSON-LD + itemprop + aria-expanded |
| 11 | Mobile-First Layout | 5 breakpoints + mobile sticky order bar |
| 12 | Dev Notes Responsive | Dev notes page itself made mobile-friendly |
| 13 | URL Strategy | Option 1 (query params) vs Option 3 (colour slugs) |
| 14 | Dual-Option Decisions | 3 further Option 1 vs Option 3 architecture choices |

### Status key used in the notes

| Badge | Meaning |
|-------|---------|
| 🟢 Proposed | Recommended — ready for developer implementation |
| 🟡 Pending URL Access | Needs live page data before finalising (shipping/returns URLs) |

---

## ⚙️ Pending Items Before Production

The following require data from live Badge-A-Minit pages before the structured data can be finalised:

| Item | Source URL | Schema Field |
|------|-----------|-------------|
| Shipping transit times & rates | `/shipping-options` | `shippingDetails` in Product schema |
| Delivery handling times | `/delivery-information` | `handlingTime` in `ShippingDeliveryTime` |
| Return policy category | `/terms-and-conditions` | `hasMerchantReturnPolicy` in Product schema |

> These pages returned 403 errors during build. Values are estimated in the current schema.
> Confirm actual policy before production deployment and update accordingly.

---

## 🧪 Testing This Mockup

### Rich Results Test
Test the structured data against Google's Rich Results Test:
```
https://search.google.com/test/rich-results?url=https://girisshgk-pixel.github.io/lanyard-page-mockup/
```

### Mobile Responsive
Open Chrome DevTools → Toggle Device Toolbar and test at:
- 375px (iPhone SE)
- 390px (iPhone 14)
- 414px (Pixel 7)
- 768px (iPad Mini)
- 1024px (iPad Pro / small laptop)

### Accessibility
Run against Lighthouse in Chrome DevTools → check Accessibility score.
All images have explicit `alt` and `title`. All interactive elements have `aria-*` attributes.
FAQ accordion toggles `aria-expanded`. Colour swatches use `role="radio"` + `aria-checked`.

---

## 🚀 Deployment Instructions (When Approved)

1. **Replace** the existing product page template in WordPress/WooCommerce with the content from `index.html`
2. **Remove** `noindex, nofollow` from the robots meta tag → replace with `index, follow`
3. **Keep** `max-snippet:-1, max-image-preview:large, max-video-preview:-1`
4. **Add** `colour`, `width`, `side`, `variant` to the canonical strip parameter list in the theme's canonical script
5. **Upload** the 5 additional product images (fabric close-up, male mockup, female mockup, hook detail, logo close-up) at 1080×1080px and update `src` URLs in the thumbnail strip and ImageGallery schema
6. **Verify** shipping, delivery, and returns policy schema fields against live pages
7. **Re-test** in Google Rich Results Test after deployment

---

## 📞 Contact

**Girish Kumar** — E-Commerce SEO Manager
**Brand:** Badge-A-Minit · 56a Prospect Road, Prospect SA 5082 · (08) 8363 1655

---

*This repository and its contents are for internal review and developer handoff only.
All proposed changes are pending client and developer approval before implementation.*
