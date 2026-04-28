# MDS Website — Webflow

Code-first Webflow implementation of `digitalstudios.mattel.com`. This repo holds the design tokens, CMS schemas, page templates, custom embeds, and SEO config that drive the build inside the Webflow Designer.

The reference Next.js site lives at `../mdswebsite/`. This project is its visual-tool counterpart — same content, same brand, built so a marketing operator can edit it without touching code.

## Layout

```
mds-website-webflow/
├── webflow-variables.json   # Design tokens for Webflow Variables
├── cms-collections/         # CMS schemas + seed CSVs
├── embeds/                  # Custom code blocks ready to paste
├── styles/                  # CSS reference (variables, type, components, utilities)
├── pages/                   # Semantic HTML templates per page
├── assets/                  # Fonts, placeholder images, OG card
├── seo/                     # Meta, redirects, robots, sitemap
├── interactions/            # IX2 specs
├── forms/                   # Form integration wiring
└── docs/                    # Build guide, class system, launch checklist
```

## Setup (Webflow Designer)

1. **Create site** — start with a blank canvas at `digitalstudios.mattel.com`.
2. **Variables** — open Site Settings → Variables. Import `webflow-variables.json` (or recreate manually using the values in `styles/variables.css`).
3. **Fonts** — upload the four families from `assets/fonts/`. Set Matty Mattel Sans as the default body font. Wire weights 400/600/700.
4. **CMS** — create the eight collections defined in `cms-collections/`. Import each CSV through Webflow's bulk importer.
5. **Pages** — for each file in `pages/`, recreate the structure in Webflow using the documented class system (`docs/CLASS_SYSTEM.md`). The HTML files are reference, not export.
6. **Embeds** — paste the snippets from `embeds/` into Site Settings → Custom Code (head/body) or onto specific pages (hero rotator, Finsweet filter).
7. **Interactions** — build the IX2 triggers per `interactions/interactions.json`.
8. **Forms** — wire the contact and press inquiry forms to Zapier per `forms/zapier-salesforce.md`.
9. **SEO** — apply per-page meta from `seo/meta-tags.json` and add the redirects from `seo/redirects.json` to Site Settings → Hosting → 301 Redirects.
10. **Pre-launch** — run through `docs/LAUNCH_CHECKLIST.md`.

## Conventions

- BEM-like flat class names: `section-hero`, `card-game`, `card-game__title`.
- All color, type, and spacing decisions live in Webflow Variables. No hex literals on individual elements.
- CMS-bound text is wrapped in semantic tags (`<h1>`, `<p>`) with class names — never raw `<div>` text.
- Every page has a JSON-LD block. Templates in `embeds/json-ld.html`.
- Reduced-motion and focus-ring CSS is global; see `embeds/head-global.html`.

## Source of truth

Content originates in the Next.js site at `../mdswebsite/content/`. When CMS values change in Webflow, update the seed CSVs here so the two stay legible side by side.
