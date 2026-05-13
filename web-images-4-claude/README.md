# web-images-4-claude

A Claude Code plugin for web developers and designers. It replaces generic placeholder images and overused default icons with free, properly-licensed assets from curated sources — and gives you full control over icon color theming.

## What It Does

### Image Search
Finds free, open-use photos and illustrations from Unsplash, Pexels, Pixabay, Wikimedia Commons, and OpenVerse. Works without API keys (via Wikimedia and OpenVerse), and supports keyed access for higher-quality results. Always provides proper attribution when required by the license.

**Trigger phrases:** "find an image of...", "get a stock photo for...", "source free images for my site", "I need a background image"

### Icon Picker
Selects icons from Heroicons, Lucide, Phosphor, Tabler, and Material Symbols — all MIT/Apache-licensed libraries with thousands of icons. Delivers actual SVG code ready to embed, matched to your project's framework (React, Vue, Tailwind, vanilla HTML).

**Trigger phrases:** "pick an icon for...", "find me an icon that represents...", "I need an icon for this button", "give me a better icon than the default"

### Icon Colors
Applies color to icons using CSS custom properties, Tailwind classes, or inline SVG attributes. Handles single-color, duotone, and multi-color variants with full dark mode support.

**Trigger phrases:** "make the icon blue", "change icon color", "create a color variant", "themed icons", "dark mode icon colors"

## Setup

### Optional: Configure Image API Keys

For best image results, add these to your project's `.env` file (never commit this):

```
UNSPLASH_ACCESS_KEY=your_key_here
PEXELS_API_KEY=your_key_here
PIXABAY_API_KEY=your_key_here
```

Get free API keys at:
- https://unsplash.com/developers
- https://www.pexels.com/api/
- https://pixabay.com/api/docs/

The plugin works without keys using Wikimedia Commons and OpenVerse as fallback sources.

## Skills

| Skill | Description |
|-------|-------------|
| `image-search` | Search and embed free open-use images |
| `icon-picker` | Select and embed SVG icons from curated libraries |
| `icon-colors` | Apply and theme icon colors for website builds |

## License

MIT — Eagle Digital Designs
