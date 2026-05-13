---
name: Bulk Image Upgrade
description: Scans a project for every image tag and upgrades all of them to SEO-optimized, performance-best-practice HTML. Use when the user says "optimize all images", "fix all my img tags", "run the image optimizer", "apply lazy loading everywhere", "audit all images in the project", "upgrade my images to WebP", "my PageSpeed score is low", "fix my Core Web Vitals", "images are hurting my SEO", or when starting a new website build and wanting image best practices applied from the start.
---

# Bulk Image Upgrade

Scan the entire project for `<img>` tags and upgrade every one to the current performance and SEO standard. Apply lazy loading, `width`/`height` (CLS prevention), `srcset`/`sizes` where applicable, and `<picture>` WebP wrappers.

## Why This Matters for SEO

Google's Core Web Vitals are a direct ranking factor. Three of the six metrics are image-related:

| Metric | Image factor | Fix |
|--------|-------------|-----|
| LCP (Largest Contentful Paint) | Slow hero image load | `fetchpriority="high"`, no lazy on hero |
| CLS (Cumulative Layout Shift) | Missing `width`/`height` | Always set dimensions |
| FID / INP | Decode blocking main thread | `decoding="async"` on below-fold images |

PageSpeed Insights will also flag: missing lazy loading, oversized images, no next-gen format (WebP), and render-blocking resources.

---

## Workflow

### Step 1 — Scan for all images

Use Grep to find every `<img>` tag across HTML, JSX, TSX, Vue, Astro, Svelte, and template files:

```
Search pattern: <img
File types: *.html, *.htm, *.jsx, *.tsx, *.vue, *.astro, *.svelte, *.njk, *.hbs, *.ejs, *.php
```

Collect all matches with file paths and line numbers.

### Step 2 — Audit each `<img>` tag

For every tag found, check for these issues. Record which are missing:

| Attribute | Required | Exception |
|-----------|----------|-----------|
| `alt` | Always | None — empty `alt=""` is valid for decorative images but must be explicit |
| `width` + `height` | Always | Not needed if parent uses `aspect-ratio` CSS and explicit dimensions |
| `loading="lazy"` | All below-fold images | Hero / LCP image — must use `loading="eager"` |
| `decoding="async"` | All below-fold images | Hero image |
| `fetchpriority="high"` | LCP / hero image only | All other images |
| `srcset` + `sizes` | Images that render at variable widths | Fixed-size icons, avatars at one size |
| `<picture>` WebP wrapper | All content images | SVG images, inline data URIs |

### Step 3 — Identify the LCP image

The hero image (first large `<img>` in the DOM, or the one inside `.hero`, `#hero`, `[data-hero]`, or the first `<section>`) is the likely LCP element. It gets special treatment:
- `loading="eager"` (not lazy)
- `fetchpriority="high"`
- `decoding="sync"` (paint immediately)

If uncertain, ask the user which image is the hero before fixing.

### Step 4 — Report findings

Before making any changes, output a summary table:

```
IMAGE AUDIT SUMMARY
────────────────────────────────────────────────
File                       | Issues found
────────────────────────────────────────────────
index.html (line 14)       | missing: loading, width, height, alt
index.html (line 28)       | missing: loading, decoding
about.html (line 7)        | missing: width, height
components/Card.jsx (ln 3) | missing: loading, srcset, sizes
────────────────────────────────────────────────
Total: 4 images across 3 files — 8 issues

Hero image identified: index.html line 14 (.hero section)
  → Will use loading="eager" fetchpriority="high" instead of lazy
```

Then ask:
> "Fix all of these now? I'll apply the standard optimization template to each, using the image's existing `src` to infer dimensions where possible. [Yes / Show me each one first / Skip a specific file]"

### Step 5 — Apply fixes

For each `<img>` that needs upgrading, apply the correct pattern.

#### Standard below-fold image (most images)

```html
<!-- BEFORE -->
<img src="photo.jpg" alt="Team photo">

<!-- AFTER -->
<picture>
  <source type="image/webp"
    srcset="photo-480.webp 480w, photo-800.webp 800w, photo-1200.webp 1200w"
    sizes="(max-width: 640px) 100vw, (max-width: 1024px) 50vw, 800px">
  <img
    src="photo.jpg"
    srcset="photo-480.jpg 480w, photo-800.jpg 800w, photo-1200.jpg 1200w"
    sizes="(max-width: 640px) 100vw, (max-width: 1024px) 50vw, 800px"
    alt="Team photo"
    width="800"
    height="533"
    loading="lazy"
    decoding="async">
</picture>
```

#### Hero / LCP image (first major image above fold)

```html
<!-- BEFORE -->
<img src="hero.jpg" class="hero-img">

<!-- AFTER -->
<picture>
  <source type="image/webp"
    srcset="hero-768.webp 768w, hero-1200.webp 1200w, hero-1920.webp 1920w"
    sizes="100vw">
  <img
    src="hero.jpg"
    srcset="hero-768.jpg 768w, hero-1200.jpg 1200w, hero-1920.jpg 1920w"
    sizes="100vw"
    class="hero-img"
    alt="[descriptive text — ask user if missing]"
    width="1920"
    height="1080"
    loading="eager"
    fetchpriority="high"
    decoding="sync">
</picture>
```

#### Small fixed-size image (avatar, logo, icon-image)

No srcset needed — it renders at one size. Still add WebP wrapper:

```html
<!-- BEFORE -->
<img src="avatar.jpg">

<!-- AFTER -->
<picture>
  <source type="image/webp" srcset="avatar.webp">
  <img
    src="avatar.jpg"
    alt="[person name]"
    width="64"
    height="64"
    loading="lazy"
    decoding="async">
</picture>
```

#### React / JSX (Next.js without next/image)

```jsx
// BEFORE
<img src={photoUrl} />

// AFTER — vanilla JSX
<picture>
  <source type="image/webp" srcSet={`${photoUrl.replace('.jpg', '.webp')}`} />
  <img
    src={photoUrl}
    alt={altText}
    width={800}
    height={533}
    loading="lazy"
    decoding="async"
  />
</picture>

// AFTER — Next.js (preferred)
import Image from 'next/image'
<Image src={photoUrl} alt={altText} width={800} height={533} />
```

#### Vue / Nuxt

```vue
<!-- AFTER — vanilla Vue -->
<picture>
  <source type="image/webp" :srcset="photoUrl.replace('.jpg', '.webp')" />
  <img :src="photoUrl" :alt="altText" width="800" height="533"
       loading="lazy" decoding="async" />
</picture>

<!-- AFTER — Nuxt (preferred) -->
<NuxtImg :src="photoUrl" :alt="altText" width="800" height="533" />
```

---

## Inferring Dimensions

When `width` and `height` are unknown:

1. **Check the `src` path** — if the filename contains dimensions (e.g., `photo-800x533.jpg`), use those
2. **Check CSS** — if the image has a CSS class with explicit dimensions, use those
3. **Use common defaults by context:**
   - Hero: `width="1920" height="1080"` (16:9)
   - Card thumb: `width="800" height="450"` (16:9)
   - Avatar: `width="64" height="64"` (1:1)
   - Team photo: `width="600" height="600"` (1:1)
4. **If genuinely unknown:** add a `TODO` comment and set a reasonable aspect-ratio placeholder; ask the user to confirm

Do not invent dimensions that could cause noticeable layout shift. It is better to mark as TODO than to guess wrong.

---

## Inferring `sizes`

Match the CSS layout:

| Layout context | `sizes` value |
|----------------|--------------|
| Full-width (no container) | `100vw` |
| Max-width container (e.g., `max-w-7xl`) | `(max-width: 1280px) 100vw, 1280px` |
| 2-column grid | `(max-width: 768px) 100vw, 50vw` |
| 3-column grid | `(max-width: 640px) 100vw, (max-width: 1024px) 50vw, 33vw` |
| Sidebar layout (content ~70%) | `(max-width: 768px) 100vw, 70vw` |
| Fixed-width card (e.g., 400px) | `(max-width: 480px) 100vw, 400px` |
| Avatar / thumbnail | `64px` (or whatever the fixed display size is) |

If the CSS isn't readable (e.g., using an external CSS file), use `(max-width: 768px) 100vw, 50vw` as a safe default and note it in a comment.

---

## WebP File Naming Convention

Assume WebP versions exist at the same path with `.webp` extension:
- `photo.jpg` → `photo.webp`
- `images/hero.png` → `images/hero.webp`
- `photo-800.jpg` → `photo-800.webp`

If WebP versions do not exist, add a `<!-- TODO: generate WebP version -->` comment and note it in the summary. Do not add a `<source type="image/webp">` pointing at a file that doesn't exist.

---

## After Fixing

Report what was changed:

```
UPGRADE COMPLETE
────────────────────────────────────────────────
✓ 4 images upgraded across 3 files
✓ Hero image (index.html:14) set to eager/high-priority
✓ 3 images wrapped in <picture> for WebP support
✓ All images now have width, height, loading, decoding

TODO (requires your action):
⚠ Generate WebP versions for: photo.jpg, team.jpg, card-bg.jpg
  Run: for f in *.jpg; do cwebp -q 80 "$f" -o "${f%.jpg}.webp"; done
⚠ Confirm alt text for: index.html:28 (set placeholder "Image")
⚠ Confirm hero image dimensions — set to 1920×1080, verify correct
────────────────────────────────────────────────
```
