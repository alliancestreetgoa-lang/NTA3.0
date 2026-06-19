# NTA Group — Corporate Website

Marketing website for **NTA Group**, a UAE-based international trading house
dealing in energy, petrochemical and agricultural commodities.

Built as a **static site** (HTML + CSS + vanilla JavaScript) — no build step,
no dependencies, deployable anywhere. Three pages: **Home**, **About**, **Contact**.

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
index.html              # home (hero, products, why, reach, CTA)
about.html              # company story, mission/vision, values
contact.html            # contact details + enquiry form
assets/css/styles.css   # all styling + responsive rules
assets/js/main.js       # nav, scroll reveal, counters, contact form
assets/images/          # product photos + logo.svg
.github/workflows/      # GitHub Pages auto-deploy
```

> Header/footer markup is repeated in all three HTML files — edit them together.

## Customising

| What | Where |
|------|-------|
| Logo | Replace `assets/images/logo.svg` (or change the `<img class="brand-logo">` src in all three pages) |
| Brand colours | CSS variables at the top of `assets/css/styles.css` (`--green-800`, `--gold`, …) |
| Product text / images | the `.product-card` blocks in `index.html` |
| Contact details | the `.contact-details` list + `mailto:` in `index.html` / `main.js` |

> **Placeholders:** the contact email (`info@ntagroup.ae`), phone and address
> are placeholders — replace them with NTA Group's official details.

## Deploying

A GitHub Actions workflow (`.github/workflows/deploy.yml`) auto-deploys to
**GitHub Pages** on every push to `main` or the working branch. Enable it once:
**repo Settings → Pages → Source: GitHub Actions**. The site then publishes at
`https://<user>.github.io/NTA3.0/`.

Any other static host also works (Netlify, Cloudflare Pages, or a standard web
server) — just serve the repository root.

## Contact form

The form has no backend yet — on submit it validates and opens the visitor's
email client (`mailto:`). To capture submissions server-side, connect it to a
form service (e.g. Formspree) or a small backend endpoint.
