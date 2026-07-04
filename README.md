# agentwerke-web

The public marketing website for **Agentwerke by Isartor AI** — the
**Governed Lights-Out Software Factory** — served at **https://agentwerke.de**.

Product copy is derived from the product repository
([isartor-ai/agentwerke](https://github.com/isartor-ai/agentwerke)); the user
manual lives separately at **https://docs.agentwerke.de**.

## Stack

Static and framework-free: semantic HTML, one CSS file, and a small
progressive-enhancement script. **No build step, no toolchain, no runtime** — the
site is ultra-fast and trivially cacheable on any static/CDN host.

**Brand.** Colors, typography, the `[]` logo mark, and the sharp-cornered
industrial styling mirror the Agentwerke product UI: cyan `#00dce5` brand + lime
`#c3f400` accent on a near-black `#0e0e0f` canvas, with **Inter** (body) and
**JetBrains Mono** (marks, labels, chips), loaded from Google Fonts (the only
external request).

```
.
├── index.html            # the full single-page site (all sections)
├── robots.txt
├── sitemap.xml
├── CNAME                 # agentwerke.de (GitHub Pages custom domain)
├── assets/
│   ├── styles.css        # design system: dark-first, light theme, responsive
│   ├── main.js           # theme toggle, mobile menu, scroll-reveal, year
│   ├── favicon.svg
│   └── og-image.svg      # Open Graph / social preview
└── .github/workflows/pages.yml
```

## Local development

No dependencies — just serve the folder over HTTP so relative asset paths and the
JSON-LD resolve correctly.

```bash
python3 -m http.server 5173   # → http://localhost:5173
# or: npx serve .
```

## Deployment

`.github/workflows/pages.yml` publishes the repo root to GitHub Pages on every
push to `main` (and on manual `workflow_dispatch`) via the official Actions
pipeline (`configure-pages` → `upload-pages-artifact` → `deploy-pages`).

One-time setup:

1. **Settings → Pages → Build and deployment → Source = "GitHub Actions".**
2. **Custom domain** — `CNAME` pins `agentwerke.de`. Configure DNS:
   - Apex `agentwerke.de` → four GitHub Pages `A` records:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
     (add matching `AAAA` records for IPv6, or an `ALIAS`/`ANAME` at the apex).
   - `www.agentwerke.de` → `CNAME` to `isartor-ai.github.io`.
3. Tick **Enforce HTTPS** once the certificate is issued.

Any other static host works too (Netlify / Vercel / Cloudflare Pages / S3+CDN):
publish the repo root, no build command.

## Before launch — founder review checklist

Search the source for `REVIEW:` comments. Currently:

- **Contact / access address** — `mailto:hello@agentwerke.de` is a placeholder on
  the "Request access" and "Contact" links. Replace with the real address or a form.
- **Docs link target** — point "Read the docs" at `https://docs.agentwerke.de`.
- **GitHub repo link** — repository links point to `isartor-ai/agentwerke`.
- **OG image** — `og-image.svg` is vector; export a 1200×630 PNG if broader
  social-preview coverage is needed and update the `og:image` / `twitter:image` URLs.
