# Class system

Flat, BEM-like names. Two-word maximum for the base, double underscore for an element, double dash for a modifier. Webflow doesn't enforce BEM, but staying consistent makes the Style panel readable for the next person.

## Base + element + modifier

```
.card               base
.card__title        element
.card--featured     modifier
```

A class without one of those three pieces is fine. A class with more than one of each is not.

## Page-level (sections)

| Class           | Used on                  |
|-----------------|--------------------------|
| `section-hero`  | Homepage hero only       |
| `section`       | Generic section wrapper  |
| `section--md`   | Smaller vertical padding |
| `section--sm`   | Smallest vertical padding|

Don't create `section-news`, `section-games`, etc. — use `<section>` with a content-specific child class for the inner block.

## Layout primitives

| Class                | Notes |
|----------------------|-------|
| `container`          | Max-width 1320, padded gutter |
| `container--narrow`  | Max-width 840 |
| `container--read`    | Max-width 640 (long-form prose) |
| `grid-2/3/4`         | Standard responsive grids |
| `cluster`            | Inline horizontal flex with wrap |
| `stack-1…6`          | Vertical rhythm |

## Components

```
.card                generic card
.card-game           game tile (homepage + games index)
.card-game__art      gradient / image area
.card-game__body     padded content area
.card-game__brand    brand eyebrow
.card-game__title    game name (h3)
.card-game__meta     studio / platform line

.card-news           news row
.card-news__date     date + tag mono line
.card-news__title    headline (h2 or h3)
.card-news__sub      summary

.card-leader         leadership card (avatar / name / title)
.card-studio         studio card

.btn                 base
.btn--primary        Mattel Red filled
.btn--secondary      outlined
.btn--ghost          underline only

.tag                 label / chip
.tag--accent         red filled
.tag--status-live    green tinted
.tag--status-coming  blue tinted

.eyebrow             red caps mono label
.stat                stat block
.stat__value         large number
.stat__label         caption underneath

.nav, .nav__inner, .nav__logo, .nav__links, .nav__link
.footer, .footer__inner, .footer__col, .footer__bar

.form-field, .form-label, .form-input, .form-select, .form-textarea, .form-error

.filter-bar, .filter-pill
```

## Type utilities

```
.t-hero          clamp(52px, 7vw, 88px) bold display
.t-page          clamp(48px, 5vw, 72px) bold display
.t-section       clamp(40px, 4vw, 64px) bold display
.t-block         clamp(36px, 3.5vw, 56px) semibold display
.t-card-lg       32px semibold
.t-card-md       22px semibold
.t-card-sm       18px semibold
.t-body-lg       18px regular
.t-body-md       15px regular
.t-body-sm       13px regular
.t-serif         Source Serif 4, body-lg
.t-mono          JetBrains Mono caps
.t-eyebrow       11px bold mono caps red
.t-caption       11px caps muted
.prose           long-form prose container
```

## State / behaviour attributes (NOT classes)

Attributes drive JS and IX2 behaviour; classes drive style. Don't mix.

```
data-hero-rotator           root of the hero carousel
data-hero-eyebrow           bound text
data-hero-line1             bound text
data-hero-line2             bound text
data-hero-blurb             bound text
data-hero-story             href target
data-hero-dot="0|1|2"       slide selector
data-hero-status            sr-only live region

data-theme-toggle           dark mode switch
data-theme-icon-light       icon shown in light mode
data-theme-icon-dark        icon shown in dark mode

data-ix-fade-up             scroll-into-view fade-up target

data-copy="…"               copy-to-clipboard source
data-copy-label             label that flips to "Copied"

data-cookie-accept          cookie banner accept button
data-cookie-decline         cookie banner decline button

fs-cmsfilter-element="filters"
fs-cmsfilter-element="list"
fs-cmsfilter-element="reset"
fs-cmsfilter-element="empty"
fs-cmsfilter-field="status|platform|studio|tag|team|department"
fs-cmsfilter-type="any"
```

## What NOT to do

- ❌ `mds-` or `c-` prefixes. Webflow's Designer crowds them visually.
- ❌ Inline-styling tokens that should be Variables (every color, every spacing value).
- ❌ Using `<div>` for headings, even if class names approximate one.
- ❌ Renaming classes inside CMS templates — every instance of a Collection Template uses the same DOM, so renaming bleeds.
