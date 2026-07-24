# Early Steps Therapy — Website

Static one-page site for **Early Steps Therapy**, a pediatric physical therapy clinic in Pikesville, MD. Live at **[earlystepstherapy.com](https://earlystepstherapy.com)**.

## Structure

Everything is a single self-contained page — no build step, no framework.

```
index.html      The entire site: HTML + embedded CSS + embedded JS
images/         Photos, logo variants, favicons, social share card
CNAME           GitHub Pages custom-domain marker (do not delete)
.nojekyll       Disables Jekyll processing on GitHub Pages
```

Key sections in `index.html`, top to bottom: sticky header (emblem logo + name lockup, hamburger menu under 900px), arch-window hero, violet trust strip, about, conditions chips, technique cards, dark contact band (phone / address / email / evaluation CTA), footer. The `<head>` carries Open Graph + Twitter tags, canonical URL, favicons, and JSON-LD `MedicalClinic` structured data.

### Brand tokens (CSS variables at the top of the stylesheet)

| Token | Value | Use |
|---|---|---|
| `--ink` | `#38173F` | body text |
| `--violet` | `#8E2E9E` | primary brand purple |
| `--violet-deep` | `#6C1F79` | headings |
| `--sprout` | `#A5CD39` | brand green, CTAs, accents |
| `--petal` | `#FAF6FC` | page background |

Fonts: **Baloo 2** (display) and **Nunito Sans** (body) via Google Fonts.

## Editing

Edit `index.html` directly and push to `main` — GitHub Pages redeploys automatically (usually under a minute).

Things that live in more than one place when they change:

- **Phone number**: `tel:` links, the visible text, the copy-button toast text in the JS, and the JSON-LD `telephone`.
- **Address / email**: contact cards and JSON-LD.
- **Social preview image**: `images/og-image.png` (1200×630), referenced from the OG tags with an absolute URL.

## Hosting & DNS

- **Hosting**: GitHub Pages, repo `AviFried/earlysteps-website`, `main` branch root, HTTPS enforced.
- **Custom domain**: `earlystepstherapy.com` (the `CNAME` file in the repo root is what tells Pages this — deleting it detaches the domain on the next push).
- **DNS**: managed at GoDaddy (`ns51`/`ns52.domaincontrol.com`):
  - `@` A → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
  - `www` CNAME → `avifried.github.io`
  - MX/SPF for Google Workspace mail — leave untouched.

### Lesson learned (July 2026 migration)

The domain previously ran a GoDaddy **Websites + Marketing** builder site. While that product is *connected* to a domain, GoDaddy overrides the `@` and `www` answers at its own nameservers, silently ignoring what the DNS editor shows. Unpublishing the builder site released the connection, but the nameservers kept serving stale records until a DNS edit (any edit — we bumped a TTL) forced GoDaddy to re-push the zone. If DNS ever looks right in the editor but wrong in `nslookup`, that history is the first thing to check.

## Pending content (waiting on clinic)

- Hours of operation (for the site + JSON-LD `openingHoursSpecification`)
- Social media links (footer + JSON-LD `sameAs`)
- Google Business Profile URL (JSON-LD `hasMap` / get-directions link)
