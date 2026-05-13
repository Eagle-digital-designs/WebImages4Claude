---
name: Site Imagery Planner
description: Audits a website project and generates a complete image and icon plan — every asset needed, where it goes, what size, and where to source it. Use when the user says "plan the images for my site", "what images do I need", "audit my site's images", "create an image plan", "what icons do I need for this site", "I'm starting a new website and need to plan assets", "help me figure out all the visuals", or when beginning a new website build and visual assets haven't been decided yet.
---

# Site Imagery Planner

Audit the current project or a described website and produce a complete visual asset plan — every image and icon needed, with specs and sourcing strategy. Deliver an actionable checklist the developer can work through.

## Workflow

### Step 1 — Understand the site

If files are available, read:
- `index.html` or main page templates
- Any layout/component files that contain `<img>`, `background-image`, or icon references
- The README or any design brief

If no files exist yet, ask:
- What type of site? (portfolio, SaaS, e-commerce, blog, agency, restaurant, etc.)
- How many pages? List them.
- Is there a brand or color palette already?
- What framework? (plain HTML, React, Next.js, Vue, Astro, etc.)

### Step 2 — Identify all image placements

Walk through every page/section and identify every image slot. Categorize as:

| Category | Examples |
|----------|---------|
| **Hero** | Full-width banner, above-fold section image |
| **Section backgrounds** | Feature section, CTA band, testimonial area |
| **Content images** | Blog post images, case study screenshots |
| **Team / People** | Headshots, team grid, author avatars |
| **Product / Portfolio** | Product photos, project screenshots |
| **Logos** | Site logo, client logos, partner logos |
| **Icons** | Nav, feature cards, buttons, status indicators |
| **Illustrations** | Empty states, 404, onboarding graphics |
| **Social / SEO** | OG image, Twitter card, favicon set |

### Step 3 — Produce the asset plan

Output a structured plan with the following sections.

---

## Output Format

### Section A — Image Assets

For each image:

```
**[Location]** — [Page / Component]
- Slot: [hero / card / background / team / etc.]
- Display size: [e.g., 1920×600px at desktop, 750×500px at mobile]
- Actual file size needed: [e.g., 1920×600 source, WebP + JPEG]
- Aspect ratio: [16:9 / 1:1 / 3:2 / etc.]
- Subject: [what the image should show — be specific]
- Tone/style: [photograph / illustration / abstract / dark / light / branded]
- Source strategy: [stock (OpenVerse/Unsplash), custom photo, client-provided]
- Priority: [Critical / High / Medium / Low]
```

### Section B — Icon Set

List every distinct icon needed across the site:

```
| Location | Icon Name/Concept | Library | Style | Color |
|----------|-----------------|---------|-------|-------|
| Nav → Home | Home | Heroicons | Outline | currentColor |
| Nav → Menu | Hamburger | Heroicons | Outline | currentColor |
| Feature card 1 | [concept] | Heroicons | Outline | brand-blue |
...
```

Recommend a single consistent library for the whole site unless mixing is intentional.

### Section C — Logo & Brand Assets

List what's needed:
- Main logo (SVG)
- Favicon set (32×32, 180×180 Apple touch, 512×512 manifest)
- OG/social image (1200×630)
- Dark/light mode logo variants (if needed)

### Section D — Sourcing Checklist

Split into three columns:

**Custom / Client-Provided (must be shot or designed):**
- [ ] Team headshots (N people)
- [ ] Product photography
- [ ] Logo files from brand guide

**Stock (can source now):**
- [ ] Hero: [topic] — search OpenVerse/Unsplash for "[suggested query]"
- [ ] Section background: [topic]
- [ ] Blog placeholder: [style]

**Can be deferred (lower priority):**
- [ ] 404 illustration
- [ ] Empty state graphic
- [ ] Seasonal/promo banners

### Section E — Implementation Notes

- Which images need `fetchpriority="high"` (LCP candidates)
- Which images need art-direction (`<picture>` with different mobile/desktop crops)
- Which images should use blur-up placeholders
- Whether a CDN or image optimization service is recommended at project scale
- Any accessibility gaps (missing alt patterns to establish)

---

## Example Plan Fragment

```
SITE: Marketing SaaS landing page (5 sections, 1 page)

IMAGES:
1. Hero background
   - Location: Section #hero
   - Display: Full-width, 100vw × 70vh, ~1920×900
   - Subject: Abstract tech / network nodes, dark blue tones
   - Style: Photograph or abstract illustration, dark overlay applied in CSS
   - Source: OpenVerse — query "network technology dark blue abstract"
   - Priority: Critical (LCP candidate — fetchpriority=high)

2. Feature section — 3 illustration spots
   - Location: Section #features, cards 1–3
   - Display: 80×80px icon/illustration each
   - Subject: (1) Speed/performance, (2) Security, (3) Analytics
   - Style: Simple flat illustration or icon — match brand color
   - Source: Use Heroicons (bolt, shield-check, chart-bar) in brand color
   - Priority: High

3. Testimonials — 3 avatar photos
   - Location: Section #testimonials
   - Display: 64×64px circular crop
   - Subject: Professional headshots, diverse
   - Style: Real photography, neutral background preferred
   - Source: Unsplash — query "professional headshot portrait" (filter: person)
   - Note: Client may want real customer photos — flag as TBD
   - Priority: Medium

ICONS (full list):
Nav: home, bars-3, x-mark (menu open/close)
Hero CTA: arrow-right (button)
Features: bolt, shield-check, chart-bar (feature cards)
Footer: envelope, map-pin, phone

Recommended library: Heroicons (outline, 24px) — matches Tailwind

LOGO & BRAND:
- [ ] SVG logo from client (or design one)
- [ ] Favicon: export 32×32 PNG from logo mark
- [ ] Apple touch icon: 180×180 PNG
- [ ] OG image: 1200×630 — branded, with tagline text overlay

PRIORITY ORDER:
1. Hero background (blocks above-fold render)
2. Logo + favicon (identity)
3. Icons (can use Heroicons placeholders immediately)
4. Feature illustrations (high visibility)
5. Testimonial avatars (can use placeholder circles initially)
6. OG image (for launch day, not blocking dev)
```

---

## Quick-Start: Starting With No Files

When the user describes a site from scratch, generate a minimal starter asset plan immediately without asking too many questions. Use these defaults:

- **Icons:** Heroicons (outline) unless they mention a specific framework preference
- **Photos:** OpenVerse as primary source (no key needed)
- **Hero:** Always flag as critical / LCP
- **OG image:** Always include — easy to miss until launch
- **Favicon:** Always include the full set (32, 180, 192, 512)

Offer to immediately source the stock images and fetch icons for any item in the plan.
