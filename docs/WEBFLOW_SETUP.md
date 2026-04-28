# Webflow setup — step by step

Follow this end-to-end the first time. After that, lean on `LAUNCH_CHECKLIST.md` for releases.

## 0. Prereqs

- Webflow workspace with at least the **CMS** plan (CMS plan minimum for the Games + News collections; **Business** plan recommended for white-label and 3-stage staging).
- GitHub access to this Webflow source repository.
- Salesforce sandbox creds for the Zapier wiring (test before pointing at prod).

## 1. Create the site

1. New site → blank canvas.
2. Site Settings → General → set **default time zone** to America/Los_Angeles.
3. Set **password protection** ON during build; remove only at launch.

## 2. Variables

Site Settings → **Variables**.

- Recreate every entry from `webflow-variables.json`. Webflow doesn't import JSON directly; you'll create one Variable Collection per top-level key (Color, Typography / Size, Spacing / Stack, etc.).
- Switch the **Color** collection to **Modes: light / dark** so dark-mode swap is automatic.
- Bind every page-level color, type and spacing to a Variable. **Never** type a hex literal.

## 3. Fonts

Site Settings → **Fonts** → Custom Fonts.

- Upload from `assets/fonts/`:
  - `MattyMattelSans-Regular.woff2` → weight 400
  - `MattyMattelSans-SemiBold.woff2` → weight 600
  - `MattyMattelSans-Bold.woff2` → weight 700
  - `SourceSerif4-Regular.woff2` → weight 400
  - `SourceSerif4-SemiBold.woff2` → weight 600
  - `JetBrainsMono-Regular.woff2` → weight 400
  - `JetBrainsMono-Medium.woff2` → weight 500
  - `JetBrainsMono-SemiBold.woff2` → weight 600
- Set **Matty Mattel Sans** as the default body font.

## 4. CMS collections

For each of the six CSVs in `cms-collections/`:

1. CMS → **+ New Collection** with the name and field set described in `cms-collections/README.md`.
2. **Bulk import** the CSV. Map each column to its Webflow field type.
3. Confirm slugs match — the slug column is the source of truth for `/games/[slug]` and `/news/[slug]` URLs.

Order matters for **Games** and **News** since templates depend on them. **Leadership** and **Studios** can be inline only.

## 5. Pages and templates

For each file in `pages/`:

1. Recreate the structure in Webflow Designer using the class names exactly as written.
2. Bind every CMS field marked `{{Name}}`, `{{Slug}}`, etc. to the matching collection field.
3. For **collection pages** (`game-detail.html`, `news-detail.html`), create the Webflow Collection Template Page and rebuild the body inside that template.

Keep the **Nav** and **Footer** as Webflow Symbols so a single edit propagates.

## 6. Custom code

Site Settings → **Custom Code**.

- **Head Code**: paste `embeds/head-global.html` and the Organization + WebSite JSON-LD blocks from `embeds/json-ld.html`.
- **Footer Code**: paste `embeds/body-global.html`. It includes the mobile nav toggle wiring, theme toggle wiring, and required cookie banner markup.

Page-specific:
- Homepage: `embeds/hero-rotator.html` in the page-level Footer Code.
- `/games`, `/news`, and `/careers`: `embeds/finsweet-filter.html` in page-level Footer Code.
- `/press-kit` and `/brand`: `embeds/copy-to-clipboard.html` in page-level Footer Code.
- `/news/[slug]` template: NewsArticle + BreadcrumbList JSON-LD in page-level Head Code.
- `/games/[slug]` template: VideoGame + BreadcrumbList JSON-LD in page-level Head Code.

## 7. Interactions

Open IX2 → recreate every entry from `interactions/interactions.json`.

The most load-bearing one is **Section / Fade-up on scroll** — apply once, attached to the attribute selector `[data-ix-fade-up]`.

## 8. Forms

Follow `forms/zapier-salesforce.md` for the Zapier side. Webflow side requires no extra wiring beyond setting the form name and required fields.

Run the Zap against a Salesforce sandbox first. Only switch to the production queue after privacy copy, lead ownership, Slack notifications, and confirmation email senders have been approved.

## 9. SEO

- Apply per-page meta from `seo/meta-tags.json` via Page Settings → SEO Settings.
- Add 301s from `seo/redirects.json` to Site Settings → Hosting → 301 Redirects.
- Expand any legacy URL wildcard notes in `seo/redirects.json` into concrete one-off rows before launch.
- Webflow generates `/sitemap.xml` automatically; verify it includes both static pages and CMS items at `digitalstudios.mattel.com/sitemap.xml`.

## 10. Pre-launch

Run `docs/LAUNCH_CHECKLIST.md` end to end. Don't skip the accessibility section.

## 11. Launch

- Connect custom domain `digitalstudios.mattel.com`.
- Remove staging password.
- Verify Cloudflare / DNS TTL is short before flipping; restore after 24h of clean traffic.
