# web-images-4-claude — Roadmap

Tracks completed features and planned future development.

---

## Released — v0.1.0

**Core plugin scaffolding**

- `image-search` skill — searches OpenVerse, Wikimedia, Unsplash, Pexels, Pixabay; provides embeddable HTML + attribution
- `icon-picker` skill — selects from Heroicons, Lucide, Phosphor, Tabler, Material Symbols; delivers ready SVG
- `icon-colors` skill — applies color via CSS custom properties, Tailwind classes, inline SVG, duotone, gradients
- References: image API docs, attribution guide, icon library guide, color variant swatches

## Released — v0.2.0 (this session)

**Depth, embedded assets, and new skills**

- `common-icons-heroicons.md` — 30 most-used Heroicons with full SVG path data embedded (no network fetch needed)
- `image-sizing.md` — standard dimensions and aspect ratios for every web image context
- `image-optimization` skill — srcset, WebP `<picture>`, lazy loading, blur-up placeholder, LCP/CWV guidance
- `site-imagery-planner` skill — full site audit: catalogues every image/icon slot, produces sourcing checklist

---

## Planned — v0.3.0

**MCP server for authenticated API access**

Current limitation: the image-search skill instructs Claude to call APIs via WebFetch, but Pexels requires an `Authorization` header that WebFetch may not support. A lightweight MCP server solves this cleanly.

**Tasks:**
- [ ] Build a Node.js MCP stdio server (`image-api-server.js`)
- [ ] Expose tools: `search_unsplash`, `search_pexels`, `search_pixabay`
- [ ] Read API keys from environment variables at runtime
- [ ] Return structured results (url, thumbnail, attribution, license)
- [ ] Add `.mcp.json` entry pointing at the server
- [ ] Document server setup in README (npm install, env var config)
- [ ] Update `image-search` SKILL.md to prefer MCP tools over WebFetch when available

**Estimated effort:** Medium (2–3 hours)

---

## Planned — v0.4.0

**Color palette extraction**

Allow Claude to extract a color palette from an existing image (logo, hero photo, brand asset) and automatically generate matching icon colors, CSS custom properties, and Tailwind config entries.

**Tasks:**
- [ ] Add a `color-extractor` skill
  - Accept a local image path or URL
  - Use a Node.js script (via Bash tool) with `sharp` + `color-thief-node` to extract 5–8 dominant colors
  - Classify colors into roles (primary, secondary, accent, neutral, background)
  - Output: CSS custom property block, Tailwind `extend.colors` config, suggested icon color assignments
- [ ] Add `scripts/extract-colors.js` script bundled in plugin
- [ ] Reference the color roles in `icon-colors` skill for automatic brand matching

**Estimated effort:** Medium-high (3–4 hours)

---

## Planned — v0.5.0

**SVG sprite sheet generation**

For projects that use many icons, individual inline SVGs create repetition and bloat. Generate a single `icons.svg` sprite sheet and a `<use>` reference pattern.

**Tasks:**
- [ ] Add an `icon-sprite` skill
  - Accept a list of icon names + libraries
  - Fetch each SVG from CDN
  - Combine into a single `<svg>` with `<symbol id="icon-name">` elements
  - Write to `public/icons.svg` (or wherever static assets live)
  - Output a `<use>` helper snippet for each icon
- [ ] Add a Bash script helper `scripts/build-sprite.sh`
- [ ] Document in README

**Estimated effort:** Medium (2–3 hours)

---

## Planned — v0.6.0

**OG / Social media image generation**

Generate Open Graph images (1200×630) programmatically from a template — branded, with dynamic title text, without needing a design tool.

**Tasks:**
- [ ] Add an `og-image-generator` skill
  - Accept: page title, tagline, brand color, logo path
  - Use a Node.js script with `sharp` or `satori` (React → SVG → PNG) to composite the image
  - Write output to `public/og/[page-slug].png`
  - Output the `<meta>` tags ready to paste into `<head>`
- [ ] Bundle `scripts/generate-og.js`
- [ ] Provide 2–3 OG image layout templates (centered, left-aligned, hero-style)
- [ ] Add to `site-imagery-planner` as an automatic output for every page planned

**Estimated effort:** High (4–6 hours — satori or sharp compositing has complexity)

---

## Planned — v0.7.0

**Image placeholder / skeleton system**

During development, placeholder images with correct aspect ratios prevent layout thrash and make mockups look complete.

**Tasks:**
- [ ] Add a `placeholder-images` skill
  - Generate SVG placeholders at any size with aspect ratio, label text, and color
  - Output as inline SVG data URI (no external service dependency)
  - Support: solid color, hatched pattern, blur, gradient fills
  - Optionally use https://placecats.com / https://picsum.photos for realistic Lorem Picsum placeholders
- [ ] Add a `skeleton-loader` skill
  - Generate CSS skeleton screen patterns for image containers
  - Match the skeleton to the image's display size and shape

**Estimated effort:** Low (1–2 hours)

---

## Planned — v1.0.0

**Design system integration**

Tie all the plugin's capabilities together into a project-level design system for images and icons.

**Tasks:**
- [ ] Add a `design-system-imagery` skill
  - Reads or generates a `imagery-tokens.json` file with: icon library, icon size scale, color tokens, standard image sizes, blur placeholder policy
  - All other skills reference this file for consistent output
- [ ] Add Figma plugin bridge (export icon choices back to Figma variables)
- [ ] Add Storybook stories template for icon components
- [ ] Support for custom icon libraries (point at a local SVG folder)

**Estimated effort:** High (ongoing, likely multi-session)

---

## Known Issues / Backlog

| Issue | Priority | Notes |
|-------|----------|-------|
| Pexels API requires Authorization header — WebFetch may drop it | High | Blocked until v0.3.0 MCP server |
| Pixabay key must be in URL query param — visible in logs | Medium | MCP server will move it server-side |
| `common-icons-heroicons.md` only covers Heroicons — Lucide/Tabler versions missing | Medium | Add in a follow-up |
| `site-imagery-planner` has no automated file scanner yet — relies on Claude reading files | Medium | Could add a Grep-based audit in a future version |
| No test for API key presence before attempting keyed search | Low | Add detection + graceful fallback message |
| Image URLs from OpenVerse occasionally return 404 (filter_dead helps but not 100%) | Low | Add URL liveness check before recommending |

---

## Ideas Parking Lot

These are raw ideas not yet scoped:

- **AI image prompt generator** — given a website section description, generate optimized prompts for Midjourney/DALL-E/Stable Diffusion to create custom hero/section images
- **Accessibility audit** — scan all `<img>` in a project for missing or low-quality alt text; suggest improvements
- **Image CDN config helper** — generate Cloudinary, Imgix, or Cloudflare Images transform URLs for any image on the site
- **Dark mode image switcher** — automatically create CSS media-query `<source>` blocks for dark/light image variants
- **Lucide icon cheat sheet** — embedded SVG paths for top 30 Lucide icons (parallel to the Heroicons reference)
- **Tabler icon cheat sheet** — same for Tabler
- **Copyright watchdog** — scan a codebase for hotlinked images from sources that may have license issues
