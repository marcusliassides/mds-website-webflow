# Launch checklist

Run this top to bottom before flipping DNS. Every box must be ticked.

## Content

- [ ] Every row in `cms-collections/games.csv` is imported into the Games CMS with correct slugs.
- [ ] All news items imported with `Date` parsed as a real Date field (not a string).
- [ ] Homepage hero rotator names match the 3 moments in `embeds/hero-rotator.html` (or are CMS-bound).
- [ ] Press kit ZIPs uploaded under `/assets/press/`. Verify each download link works from a logged-out incognito window.
- [ ] All `mailto:` links resolve to mailboxes that exist (`press@`, `partnerships@`, `accessibility@`).

## Visual + brand

- [ ] No hex literals in the Style panel. Every color is bound to a Variable; CMS Color fields are the only allowed exception.
- [ ] Font weights 400 / 600 / 700 all render — open homepage in a fresh browser, no font flash.
- [ ] Light AND dark mode look right on Home, Games, News, Game-detail, News-detail.
- [ ] Mattel Red (#EA0029) is used only for primary CTAs and impact moments — NOT for error states.
- [ ] Error state color is #C8102E (test by submitting an empty contact form).

## Accessibility

- [ ] Keyboard-only walkthrough of homepage, games, news, contact — every interactive element reachable, focus ring visible.
- [ ] axe-core (Chrome DevTools) reports zero serious / critical issues on Home, Games, News, Game-detail.
- [ ] Hero rotator pause button works; `prefers-reduced-motion: reduce` collapses all animation.
- [ ] Skip link appears on Tab from page top.
- [ ] All images have meaningful `alt` text or are marked `aria-hidden="true"` if decorative.
- [ ] All form fields have associated `<label>` elements.
- [ ] Color contrast verified for `.t-body-md` text on every surface (light + dark) at WCAG AA.

## SEO

- [ ] Per-page meta titles and descriptions match `seo/meta-tags.json`.
- [ ] OG card renders correctly when pasting the homepage URL into Slack.
- [ ] `/sitemap.xml` includes static pages + every CMS item.
- [ ] `/robots.txt` matches `seo/robots.txt`.
- [ ] All 301 redirects from `seo/redirects.json` are entered and tested.
- [ ] Legacy news URLs from analytics are covered by explicit 301 rows, or intentionally left as 404/410.
- [ ] Canonical URLs set on every page (no `staging.` or `webflow.io` slipping through).
- [ ] JSON-LD validates on Schema.org's validator for Home, a Game detail, a News detail.

## Performance

- [ ] Lighthouse mobile score ≥ 90 on Home and Games.
- [ ] Largest Contentful Paint < 2.5s on Home (3G Fast emulation).
- [ ] No layout shift on hero — key art aspect ratio reserved.
- [ ] Fonts preloaded (verify with the Network panel filtered to font files: only the 3 declared in `head-global.html` should load with `preload`).

## Forms

- [ ] Submitted a real test entry; lead arrived in Salesforce.
- [ ] Slack `#mds-inbound` notification fired.
- [ ] Honeypot blocks bot-style submission (script-fill the hidden `website` field).
- [ ] Zapier task history shows zero errors over the last 10 test runs.

## Analytics + consent

- [ ] Cookie banner DOM from `embeds/body-global.html` is present in the Footer Symbol or a global embed.
- [ ] GA4 measurement ID configured in a consent-gated snippet that loads only after `mds:consent-change` reports `detail.accepted === true` or `mds:consent-accepted` fires.
- [ ] Cookie banner appears once on first visit, suppressed after acceptance or decline.
- [ ] Consent state persists across reload (check localStorage for `mds-cookie-consent`).
- [ ] No third-party trackers fire before consent is granted.

## Cross-browser

Verify Home, Games, News, Contact in:
- [ ] Chrome (latest)
- [ ] Safari macOS (latest)
- [ ] Safari iOS 17+
- [ ] Firefox (latest)
- [ ] Edge (latest)

## Final flip

- [ ] Disable Webflow staging password.
- [ ] Update DNS A / CNAME records per Webflow Hosting guide.
- [ ] Flip CDN TTL low, monitor for 30 minutes after publish.
- [ ] Smoke-test from the production URL incognito.
- [ ] Restore CDN TTL after 24h of clean traffic.
- [ ] Notify `#mds-launches` Slack channel.
