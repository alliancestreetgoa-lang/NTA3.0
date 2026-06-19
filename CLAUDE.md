# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A marketing website for **NTA Group**, a UAE-based international commodity
trading house (energy, petrochemicals, agriculture). It is a **static site**
with **no build system, no package manager, and no dependencies** — three HTML
pages, one CSS file, and one vanilla JS file. There is nothing to compile or
install.

## Running & previewing

```bash
python3 -m http.server 8000      # then open http://localhost:8000
```

Serve over HTTP rather than opening `file://` so Google Fonts and the image
assets resolve correctly. There is no test suite, linter, or CI configured.

## Architecture

Three HTML pages share one stylesheet and one script:

- `index.html` — home. Sections: header → hero → stats → about → products → why
  → reach → contact CTA band → footer. The products `#products`, why `#why`, and
  reach `#reach` ids are the in-page nav anchors linked from other pages as
  `index.html#products` etc.
- `about.html` — company story, mission/vision, values.
- `contact.html` — contact cards + the full enquiry form.
- `assets/css/styles.css` — all styling. **Design tokens live in `:root`** at
  the top (colours, radius, shadows, fonts). Change the palette there, not inline.
  Responsive breakpoints are at the bottom (`920px`, `560px`).
- `assets/js/main.js` — one IIFE handling: sticky-header scroll state, the mobile
  menu toggle, `IntersectionObserver`-based scroll reveals, animated stat
  counters, and the contact form. No framework. The same file loads on every page.

**Header and footer markup is duplicated** across the three HTML files (there is
no templating). When you change the nav, logo, or footer, **update all three
pages** to keep them in sync.

The logo is `assets/images/logo.png` (the official NTA Group wordmark, white
background removed to transparency). It is shown inside a white `.brand-chip`
in every header and footer so its blue/green/orange stays legible over the dark
green backgrounds. Because the wordmark already reads "NTA GROUP", there is no
separate brand text. To change the logo, replace that file (transparent PNG/SVG
recommended); to resize, adjust `.brand-logo` height in the CSS.

## Conventions that matter

- **Scroll-reveal:** any element given the class `reveal` starts hidden and
  animates in when scrolled into view (`main.js` adds `.in`). New content that
  should animate must include `class="reveal"`.
- **Header colour inversion:** the header is transparent over the hero and turns
  solid (`.scrolled`) on scroll. Styles use `.site-header:not(.scrolled)` to
  flip text/logo to white over the hero — preserve this pattern when editing the
  header so nav links stay legible in both states.
- **Stat counters:** numbers animate from a `data-count` attribute; a `%`/`+`
  suffix goes in an adjacent `.stat-suffix` span. Non-numeric stats (e.g. `24/7`)
  simply omit `data-count`.
- **Products:** each product is a `.product-card` with a numbered badge
  (`.product-num`, 01–06) and an image in `assets/images/product-*.png`. Keep the
  number/image/title in sync if reordering.
- **Header colour inversion needs a dark backdrop:** because the header is
  transparent until scrolled, every page starts with a dark hero (`.hero` on
  home, `.page-hero` on inner pages) so the white nav text is legible. A new page
  must begin with one of these, or the header text will be invisible at the top.

## Deployment

`.github/workflows/deploy.yml` publishes the site to **GitHub Pages** on push to
`main` or `claude/claude-md-docs-b020qn` (whole repo root is the artifact).
Pages must be enabled once in the repo settings (Settings → Pages → Source:
GitHub Actions).

## Known placeholders (replace with real data, don't invent)

- Contact email `info@ntagroup.ae`, phone `+971 00 000 0000`, and address are
  placeholders in both `index.html` and the `mailto:` handler in `main.js`.
- Stats (markets served, continents, etc.) are illustrative.
- The contact form has **no backend** — it validates client-side and opens the
  visitor's email client via `mailto:`. Wiring a real endpoint (form service or
  backend) is the natural next step.

## Design intent

"Natural + modern" for a UAE government-facing audience: deep forest green
(`--green-800`) with warm gold (`--gold`) accents, serif headings (Marcellus)
over a sans body (Inter), generous whitespace, restrained motion. Keep edits
within this system — reach for the existing CSS variables and section patterns
rather than introducing new colours, fonts, or one-off styles.
