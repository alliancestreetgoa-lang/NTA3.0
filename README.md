# NTA Group — Corporate Website

Marketing website for **NTA Group**, a UAE-based international trading house
dealing in energy, petrochemical and agricultural commodities.

Built as a **static site** (HTML + CSS + vanilla JavaScript) — no build step,
no dependencies, deployable anywhere.

## Products showcased

1. Chemical Fertilizers Trading
2. Industrial & Liquefied Natural Gas Trading
3. Trading Refined Oil Products Abroad
4. Crude Oil Trading Abroad
5. Petrochemicals Trading
6. Grains, Cereals & Legumes Trading

## Run locally

No tooling required — open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

A local server is recommended (rather than `file://`) so fonts and images
load correctly.

## Project structure

```
index.html              # single-page site (all sections)
assets/css/styles.css   # all styling + responsive rules
assets/js/main.js       # nav, scroll reveal, counters, contact form
assets/images/          # product photos (and your logo)
```

## Customising

| What | Where |
|------|-------|
| Logo | `assets/images/` → add `logo.png`, then swap the `.brand-mark` span in `index.html` for an `<img>` (see comment in the header) |
| Brand colours | CSS variables at the top of `assets/css/styles.css` (`--green-800`, `--gold`, …) |
| Product text / images | the `.product-card` blocks in `index.html` |
| Contact details | the `.contact-details` list + `mailto:` in `index.html` / `main.js` |

> **Placeholders:** the contact email (`info@ntagroup.ae`), phone and address
> are placeholders — replace them with NTA Group's official details.

## Deploying

Any static host works (GitHub Pages, Netlify, Cloudflare Pages, or a standard
web server). For GitHub Pages, serve the repository root on the default branch.

## Contact form

The form has no backend yet — on submit it validates and opens the visitor's
email client (`mailto:`). To capture submissions server-side, connect it to a
form service (e.g. Formspree) or a small backend endpoint.
