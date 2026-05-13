# WebImages4Claude

A Claude Code plugin for web developers and designers. Sources free, properly-licensed images from the open web, delivers real SVG icons from curated libraries, and automatically enforces performance and SEO best practices on every image in your project.

## Install

**Claude Cowork (desktop):** drag and drop `web-images-4-claude.plugin` onto the app window → click Accept.

**Claude Code (CLI):**
```bash
claude plugin install ./web-images-4-claude.plugin
```

## What's inside

| Skill | Say... | Gets you |
|-------|--------|---------|
| `image-search` | "find a free image of..." | Photos from OpenVerse, Wikimedia, Unsplash, Pexels, Pixabay with embed HTML + attribution |
| `icon-picker` | "give me a better icon for..." | SVG code from Heroicons, Lucide, Phosphor, Tabler, or Material Symbols |
| `icon-colors` | "make the icons match my brand" | CSS custom properties, Tailwind classes, duotone, dark mode variants |
| `image-optimization` | *(automatic)* | Lazy loading, WebP `<picture>`, srcset/sizes, fetchpriority — applied to every `<img>` by default |
| `bulk-image-upgrade` | "fix all my images" | Scans the entire project and upgrades every `<img>` to the full optimization standard |
| `site-imagery-planner` | "plan all the images for my site" | Complete asset plan: every image slot, icon list, sourcing checklist, priorities |

A **PostToolUse hook** silently watches every file write and flags any `<img>` tag missing optimization attributes — no setup needed.

## Optional API keys

Works without any keys via OpenVerse and Wikimedia. For higher-quality stock photos, add to `.env`:

```env
UNSPLASH_ACCESS_KEY=your_key_here
PEXELS_API_KEY=your_key_here
PIXABAY_API_KEY=your_key_here
```

→ **Full documentation:** [web-images-4-claude/README.md](web-images-4-claude/README.md)

## License

MIT — [Eagle Digital Designs](https://github.com/Eagle-digital-designs)
