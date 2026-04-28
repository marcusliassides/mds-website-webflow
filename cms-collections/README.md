# CMS Collections

Field types for each collection, ready to recreate in Webflow CMS. Match the column → field mapping when importing the seed CSV.

## Games

| Column            | Webflow field type | Notes |
|-------------------|--------------------|-------|
| Name              | Plain Text         | Display name |
| Slug              | Slug               | URL-safe |
| Code              | Plain Text         | Internal code (LV-01, MGS-01, LIC-03…) |
| Brand             | Option (multi)     | UNO, Hot Wheels, MOTU, etc. — use Reference if you create a Brand collection |
| Studio            | Plain Text         | Comma-separated for co-dev partners |
| Platform          | Plain Text         | Comma-separated display/filter string, e.g. "iOS, Android" |
| PlatformJsonArray | Plain Text         | JSON array string for VideoGame JSON-LD, e.g. `["iOS","Android"]` |
| Status            | Option             | Live, Coming |
| Window            | Plain Text         | "May 2026", empty for live |
| Color             | Color              | Hex literal — used as accent in card art |
| Summary           | Rich Text          | One-paragraph blurb |
| Featured          | Switch             | Surfaces on homepage rotator |
| PlayUrl           | Link               | Optional; bind the "Play now" CTA and hide the CTA when empty |

**Page**: `/games/[slug]` → `pages/game-detail.html`.

## News

| Column      | Webflow field type |
|-------------|--------------------|
| Title       | Plain Text |
| Slug        | Slug |
| Tag         | Option (Announcement, Partnership, Launch, Strategy, Corporate) |
| Date        | Date |
| DateIso     | Plain Text         | ISO 8601 date for JSON-LD/meta, e.g. `2026-03-31T00:00:00-07:00` |
| Byline      | Plain Text |
| RelatedGames | Multi-reference to Games (optional) |
| Summary     | Rich Text (1 paragraph) |
| SummaryPlain | Plain Text         | Plain-text summary for meta descriptions and OG tags |
| Body        | Rich Text |

**Page**: `/news/[slug]` → `pages/news-detail.html`.

## Studios

| Column   | Webflow field type |
|----------|--------------------|
| Name     | Plain Text |
| Slug     | Slug |
| Location | Plain Text |
| Kind     | Option (First-party, First-party development, Development partner, Creator Platforms partner) |
| Note     | Rich Text |

**Page**: rendered inline on `/studios` (no per-studio detail page).

## Leadership

| Column   | Webflow field type |
|----------|--------------------|
| Name     | Plain Text |
| Slug     | Slug |
| Title    | Plain Text |
| Scope    | Plain Text |
| Initials | Plain Text (avatar fallback) |
| Order    | Number |

**Page**: rendered inline on `/about`.

## Careers

| Column           | Webflow field type |
|------------------|--------------------|
| Title            | Plain Text |
| Slug             | Slug |
| Team             | Option |
| TeamFilter       | Plain Text         | Normalized Finsweet tokens for team buckets |
| Location         | Plain Text |
| LocationFilter   | Plain Text         | Normalized city/remote token for Finsweet |
| Type             | Option (Full-time, Contract, Part-time) |
| Department       | Option |
| DepartmentFilter | Plain Text         | Normalized department bucket for Finsweet |
| ApplyUrl         | Link |

**Page**: rendered inline on `/careers` with Finsweet filter on Team / Department / Location.

For Finsweet filtering, render normalized hidden field values in collection items:
`status`, `platform`, `studio`, `tag`, `team`, `department`, `location`, and optional `game`.
Use comma-separated filter input values for groups such as `iOS, Android`; item text may use
spaces or the CMS display string as long as every token is present.

## Press Kit Assets

| Column       | Webflow field type |
|--------------|--------------------|
| Title        | Plain Text |
| Slug         | Slug |
| Description  | Rich Text |
| Format       | Plain Text ("ZIP · 24 MB") |
| FileCount    | Plain Text ("18 files") |
| DownloadFile | File (uploaded ZIP) |

**Page**: rendered inline on `/press-kit`.
