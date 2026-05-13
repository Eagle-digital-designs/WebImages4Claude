# web-images-4-claude

A Claude Code plugin for web developers and designers. Stop settling for generic icons and placeholder images — this plugin finds properly-licensed photos from the open web, delivers real SVG icon code from curated libraries, and automatically enforces performance and SEO best practices on every image in your project.

---

## What It Does

| Capability | What you say | What happens |
|-----------|-------------|-------------|
| Find free images | "find an image of a mountain sunset" | Searches OpenVerse, Wikimedia, Unsplash, Pexels, Pixabay and returns embed-ready HTML with attribution |
| Pick icons | "give me a better icon for this save button" | Selects from 10,000+ icons across 5 MIT-licensed libraries; delivers the actual SVG code |
| Color icons | "make all the nav icons slate blue with a dark mode variant" | Generates CSS custom properties, Tailwind classes, duotone, or gradient color patterns |
| Optimize images | automatic on every file write | Applies lazy loading, WebP format, srcset/sizes, fetchpriority, and CLS-preventing dimensions to every `<img>` |
| Batch upgrade | "fix all my images" / "my PageSpeed score is low" | Scans the entire project, audits every `<img>`, and upgrades all of them in one pass |
| Plan site visuals | "plan all the images I need for this site" | Produces a complete asset plan: every image slot, icon list, sourcing strategy, and prioritized checklist |

---

## Installation

### Option A — Claude Cowork (desktop app)

1. Download `web-images-4-claude.plugin` from this repository's releases (or build it — see below)
2. Drag and drop the `.plugin` file onto the Cowork window
3. A preview card appears — click **Accept**
4. Done. The skills are available immediately in any project

### Option B — Claude Code CLI

```bash
claude plugin install ./web-images-4-claude.plugin
```

Verify it installed:

```bash
claude plugin list
```

### Building the plugin from source

If you cloned this repo and want to build the `.plugin` file yourself:

**Mac / Linux:**
```bash
cd web-images-4-claude
zip -r ../web-images-4-claude.plugin . -x "*.DS_Store"
```

**Windows (PowerShell):**
```powershell
Push-Location web-images-4-claude
Compress-Archive -Path ".\*" -DestinationPath "$env:TEMP\web-images-4-claude.zip" -Force
Pop-Location
Copy-Item "$env:TEMP\web-images-4-claude.zip" ".\web-images-4-claude.plugin" -Force
```

---

## Setup: Optional API Keys

The plugin works out of the box with no configuration — OpenVerse and Wikimedia Commons are free, require no account, and cover millions of images.

For higher-quality stock photography from Unsplash, Pexels, and Pixabay, add free API keys to your project's `.env` file:

```env
UNSPLASH_ACCESS_KEY=your_key_here
PEXELS_API_KEY=your_key_here
PIXABAY_API_KEY=your_key_here
```

> Never commit `.env` to version control. Add it to `.gitignore`.

Get free keys at:
- **Unsplash** — https://unsplash.com/developers (50 req/hour free)
- **Pexels** — https://www.pexels.com/api/ (200 req/hour free)
- **Pixabay** — https://pixabay.com/api/docs/ (100 req/minute free)

---

## Skills

### `image-search` — Find free open-use images

Searches multiple sources and returns images with embed HTML, direct URL, license info, and attribution text.

**Trigger phrases:**
- "find an image of [topic]"
- "get a free stock photo for my hero section"
- "source an image of [subject] for my website"
- "I need a background image of [topic]"
- "find open-use photos of [subject]"

**Sources searched (in priority order):**

| Source | Key required | License |
|--------|-------------|---------|
| OpenVerse | No | CC / CC0 |
| Wikimedia Commons | No | CC / Public Domain |
| Unsplash | Yes | Unsplash License (free commercial use) |
| Pexels | Yes | Pexels License (free commercial use) |
| Pixabay | Yes | Pixabay License (free commercial use) |

**Example output:**
```
Photo by Jane Smith on Unsplash
License: Unsplash License (free, no attribution required)
URL: https://unsplash.com/photos/...

<img src="https://images.unsplash.com/photo-..." 
     alt="Mountain landscape at sunset"
     width="1920" height="1280"
     loading="lazy" decoding="async">
```

---

### `icon-picker` — Get SVG icons from curated libraries

Selects the right icon for the job and delivers ready-to-embed SVG code — no copy-pasting from websites, no npm installs required unless you want them.

**Trigger phrases:**
- "pick an icon for [concept]"
- "find me an icon that represents [idea]"
- "I need an icon for this button"
- "give me a better icon than the default"
- "show me icons for [navigation / features / status / etc.]"
- "replace this icon with something better"

**Libraries available:**

| Library | Style | Icons | Best for |
|---------|-------|-------|---------|
| [Heroicons](https://heroicons.com) | Outline / Solid | 292 | Tailwind CSS projects |
| [Lucide](https://lucide.dev) | Outline | 1,500+ | React, Vue, general web |
| [Phosphor](https://phosphoricons.com) | 6 weights + duotone | 1,300+ | Expressive UI, marketing pages |
| [Tabler](https://tabler.io/icons) | Outline / Filled | 5,000+ | Dashboards, data-heavy UI |
| [Material Symbols](https://fonts.google.com/icons) | Outlined / Rounded / Sharp | 3,000+ | Material UI, Google-adjacent design |

**Example output:**
```html
<!-- magnifying-glass — Heroicons outline -->
<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
     stroke-width="1.5" stroke="currentColor" width="24" height="24"
     aria-hidden="true">
  <path stroke-linecap="round" stroke-linejoin="round"
    d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z"/>
</svg>
```

For the 30 most common Heroicons, path data is embedded directly in the plugin — no network fetch needed.

---

### `icon-colors` — Apply colors to icons

Controls icon color at the CSS level. Never hard-codes hex values inside SVGs — keeps all color control in your stylesheet so theming stays maintainable.

**Trigger phrases:**
- "make the icon [color]"
- "change icon color to [color / brand color]"
- "create a color variant of this icon"
- "themed icons matching my brand"
- "dark mode icon colors"
- "icon color palette for the whole site"
- "duotone icon"

**Patterns supported:**
- **Tailwind classes** — `text-blue-600 dark:text-blue-400`
- **CSS custom properties** — `var(--icon-primary)` with `:root` and `@media (prefers-color-scheme: dark)` blocks
- **Inline SVG** — direct `fill` / `stroke` attribute replacement
- **Duotone** — two-layer SVG with opacity (Phosphor-style)
- **Gradient fill** — `<linearGradient>` / `<radialGradient>` inside `<defs>`

**Example — full icon token system:**
```css
:root {
  --icon-primary:  #2563eb;
  --icon-success:  #16a34a;
  --icon-warning:  #d97706;
  --icon-danger:   #dc2626;
  --icon-muted:    #94a3b8;
}
@media (prefers-color-scheme: dark) {
  :root {
    --icon-primary:  #60a5fa;
    --icon-success:  #4ade80;
    --icon-warning:  #fbbf24;
    --icon-danger:   #f87171;
    --icon-muted:    #475569;
  }
}
```

---

### `image-optimization` — SEO-optimized images by default

This skill is applied **automatically** whenever Claude writes any HTML file containing images. You do not need to ask for it.

Every `<img>` Claude writes will include:

| Attribute | Default | Why it matters |
|-----------|---------|---------------|
| `alt` | Descriptive text | Accessibility + SEO ranking signal |
| `width` + `height` | Intrinsic dimensions | Prevents Cumulative Layout Shift (Google ranking factor) |
| `loading="lazy"` | All below-fold images | Defers off-screen image loads, speeds up initial paint |
| `loading="eager"` | Hero / LCP image | Loads the above-fold image immediately |
| `fetchpriority="high"` | Hero / LCP image only | Tells the browser this is the most critical resource |
| `decoding="async"` | Below-fold images | Frees the main thread during decode |
| `<picture>` + WebP `<source>` | All content images | Serves WebP to modern browsers, JPEG/PNG as fallback |
| `srcset` + `sizes` | Variable-width images | Serves correctly-sized file per viewport |

**Example output for a hero image:**
```html
<picture>
  <source type="image/webp"
    srcset="hero-768.webp 768w, hero-1200.webp 1200w, hero-1920.webp 1920w"
    sizes="100vw">
  <img
    src="hero.jpg"
    srcset="hero-768.jpg 768w, hero-1200.jpg 1200w, hero-1920.jpg 1920w"
    sizes="100vw"
    alt="Hero description"
    width="1920" height="1080"
    loading="eager"
    fetchpriority="high"
    decoding="sync">
</picture>
```

**Trigger phrases** (in addition to automatic behavior):
- "optimize this image"
- "make images load faster"
- "fix my LCP score"
- "fix Core Web Vitals"
- "images are hurting my SEO"
- "add lazy loading"
- "set up srcset"

---

### `bulk-image-upgrade` — Fix all images in a project at once

Scans every HTML, JSX, TSX, Vue, Astro, Svelte, and PHP file in the project and upgrades every `<img>` to the full optimization standard.

**Trigger phrases:**
- "optimize all images"
- "fix all my img tags"
- "run the image optimizer"
- "upgrade my images to WebP"
- "my PageSpeed score is low"
- "fix Core Web Vitals"
- "audit all images in the project"

**What it does:**
1. Greps the project for every `<img>` tag
2. Audits each one for missing attributes (alt, width/height, loading, fetchpriority, srcset, WebP wrapper)
3. Identifies the hero / LCP image automatically
4. Shows a summary of all issues before touching anything
5. Applies the correct pattern per context (hero, card, avatar, React/Vue/vanilla)
6. Reports what was changed and lists any TODOs requiring your action (e.g. generating WebP files)

**Example summary output:**
```
IMAGE AUDIT SUMMARY
────────────────────────────────────────────────
index.html (line 14)       → missing: loading, width, height, WebP wrapper
index.html (line 28)       → missing: loading, decoding
about.html (line 7)        → missing: width, height
components/Card.jsx (ln 3) → missing: loading, srcset, sizes
────────────────────────────────────────────────
Hero identified: index.html:14 — will use eager + fetchpriority=high

Fix all now? [Yes / Show me each first / Skip a file]
```

---

### `site-imagery-planner` — Plan every visual asset before you build

Audits your project files (or takes a description of a planned site) and produces a complete image and icon plan — every slot, every spec, where to source each asset, and what order to tackle them.

**Trigger phrases:**
- "plan the images for my site"
- "what images do I need for this project"
- "audit my site's images"
- "I'm starting a new website and need to plan all the visuals"
- "create an image plan"
- "what icons do I need for this site"

**Output includes:**
- Every image placement (hero, section backgrounds, cards, team photos, OG image, favicons)
- Dimensions, aspect ratio, and file format for each
- Sourcing strategy: stock, client-provided, or custom
- Complete icon list with recommended library, style, and color
- Logo and brand asset checklist
- Prioritized sourcing checklist (what to tackle first)

---

## Automatic Hook

The plugin installs a **PostToolUse hook** that runs silently after every `Write` or `Edit` operation. It checks whether the file you just wrote contains any `<img>` tags missing optimization attributes and surfaces a compact notice:

```
⚠ Image optimization: index.html:28
  Missing: loading, width/height, WebP wrapper
  Fix: run /bulk-image-upgrade or apply image-optimization to this file
```

If everything is correctly optimized, the hook outputs nothing.

---

## Plugin Structure

```
web-images-4-claude/
├── .claude-plugin/
│   └── plugin.json                          # Plugin manifest (v0.3.0)
├── hooks/
│   └── hooks.json                           # PostToolUse image watchdog hook
├── skills/
│   ├── image-search/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── image-apis.md                # Full API docs: endpoints, params, response fields
│   │       ├── attribution-guide.md         # License rules + attribution HTML templates
│   │       └── image-sizing.md              # Dimensions/aspect ratios for every web context
│   ├── icon-picker/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── icon-libraries.md            # CDN URLs, npm packages, framework usage
│   │       └── common-icons-heroicons.md    # Embedded SVG paths for 30 most-used Heroicons
│   ├── icon-colors/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── color-variants.md            # Tailwind swatches, brand presets, duotone pairs
│   ├── image-optimization/
│   │   └── SKILL.md                         # Default standard applied to every <img> written
│   ├── bulk-image-upgrade/
│   │   └── SKILL.md                         # Project-wide image audit and upgrade
│   └── site-imagery-planner/
│       └── SKILL.md                         # Full site visual asset planning
├── ROADMAP.md                               # Planned features (v0.4–v1.0)
└── README.md
```

---

## Roadmap

| Version | Feature |
|---------|---------|
| v0.4.0 | Color palette extraction — pull CSS tokens from an existing logo or image |
| v0.5.0 | SVG sprite sheet generator — combine all site icons into one file |
| v0.6.0 | OG image generator — programmatic 1200×630 branded social images per page |
| v0.7.0 | Image placeholder / skeleton system for development |
| v1.0.0 | Design system integration — unified imagery token file all skills share |

See [ROADMAP.md](ROADMAP.md) for full details and the known-issues backlog.

---

## License

MIT — [Eagle Digital Designs](https://github.com/Eagle-digital-designs)
