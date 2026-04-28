# Images

Asset directory for static images. Webflow ingests these via Asset Manager — this folder is for the source files / placeholders before upload.

Suggested structure:

```
assets/images/
├── og/             # Open Graph cards per page
├── games/          # Per-game key art (named {slug}.webp / .jpg)
├── studios/        # Studio logos
├── leadership/     # Headshots
└── press/          # Press kit ZIPs (the actual downloadable bundles)
```

Production should serve WebP/AVIF where supported. Webflow handles responsive variants automatically once you upload at 2x.
