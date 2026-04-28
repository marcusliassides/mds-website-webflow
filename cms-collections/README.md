# CMS Collections

Field types for each collection, ready to recreate in Webflow CMS. Match the column → field mapping when importing the seed CSV.

## Games

| Column   | Webflow field type | Notes |
|----------|--------------------|-------|
| Name     | Plain Text         | Display name |
| Slug     | Slug               | URL-safe |
| Code     | Plain Text         | Internal code (LV-01, MGS-01, LIC-03…) |
| Brand    | Option (multi)     | UNO, Hot Wheels, MOTU, etc. — use Reference if you create a Brand collection |
| Studio   | Plain Text         | Comma-separated for co-dev partners |
| Platform | Plain Text         | "iOS · Android" — string, not multi |
| Status   | Option             | Live, Coming, Announced |
| Window   | Plain Text         | "May 2026", empty for live |
| Color    | Color              | Hex literal — used as accent in card art |
| Summary  | Rich Text          | One-paragraph blurb |
| Featured | Switch             | Surfaces on homepage rotator |

**Page**: `/games/[slug]` → `pages/game-detail.html`.

## News

| Column   | Webflow field type |
|----------|--------------------|
| Title    | Plain Text |
| Slug     | Slug |
| Tag      | Option (Announcement, Partnership, Launch, Strategy, Corporate) |
| Date     | Date |
| Byline   | Plain Text |
| Summary  | Rich Text (1 paragraph) |
| Body     | Rich Text |

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

| Column     | Webflow field type |
|------------|--------------------|
| Title      | Plain Text |
| Slug       | Slug |
| Team       | Option |
| Location   | Plain Text |
| Type       | Option (Full-time, Contract, Part-time) |
| Department | Option |
| ApplyUrl   | Link |

**Page**: rendered inline on `/careers` with Finsweet filter on Team / Department / Location.

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
