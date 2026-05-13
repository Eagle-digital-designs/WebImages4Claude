---
name: Image Optimization
description: Applies SEO-optimized, performance-best-practice HTML to images — lazy loading, WebP format, srcset/sizes, fetchpriority, and CLS-preventing dimensions. This is the DEFAULT standard for every <img> tag written in any web project. Use proactively whenever writing or editing any HTML file that contains images. Also triggered when the user says "optimize this image", "make images load faster", "add lazy loading", "set up srcset", "convert to WebP", "responsive images", "fix LCP score", "fix Core Web Vitals", "images are hurting my SEO", "images are slow", "add a blur placeholder", or "write a picture element".
---

# Image Optimization

**These patterns are the default for every `<img>` written in any web project.** Apply them automatically — do not wait to be asked. A bare `<img src="...">` without `loading`, `width`, `height`, and a WebP `<picture>` wrapper is always incomplete.

Apply modern HTML image patterns to maximize performance, Core Web Vitals scores, and visual quality. Cover lazy loading, responsive srcset, WebP with fallback, and blur-up placeholders.

## The Non-Negotiable Defaults

Every `<img>` Claude writes must have these unless there is an explicit reason not to:

| Attribute | Default value | Why |
|-----------|--------------|-----|
| `alt` | Descriptive text (or `""` for decorative) | Accessibility + SEO |
| `width` + `height` | Intrinsic image dimensions | Prevents CLS (Google ranking factor) |
| `loading` | `"lazy"` (below fold) / `"eager"` (hero) | Defers off-screen image load |
| `decoding` | `"async"` (below fold) / `"sync"` (hero) | Frees main thread |
| `fetchpriority` | `"high"` on hero/LCP only | Signals critical resource to browser |
| `<picture>` wrapper | Always for content images | Serves WebP to modern browsers |
| `srcset` + `sizes` | When image renders at variable widths | Right-sizes image per viewport |

## Workflow

### Step 1 — Audit what's there

Look at the current `<img>` tags in the file. Check for:
- Missing `width` and `height` attributes (causes layout shift — CLS)
- Missing `loading="lazy"` on below-fold images
- Missing `srcset` / `sizes` (oversized single image)
- JPEG/PNG where WebP would be smaller
- Missing `alt` text
- No `decoding="async"` on below-fold images

### Step 2 — Apply the right pattern

Choose based on context:

| Situation | Pattern to use |
|-----------|---------------|
| Single image, no format concern | Add `loading`, `width`, `height` |
| Image has multiple size breakpoints | `srcset` + `sizes` |
| Need WebP with JPEG/PNG fallback | `<picture>` with `<source type="image/webp">` |
| Both multiple sizes AND WebP | Full `<picture>` with typed `<source>` sets |
| Above-the-fold hero | `loading="eager"`, `fetchpriority="high"`, no lazy |
| Low-quality blur-up placeholder | CSS blur + full image onload |

### Step 3 — Validate and explain

After writing the markup, confirm:
- All `<img>` have `alt`, `width`, `height`
- Lazy loading is only on below-fold images
- The hero / LCP image has `fetchpriority="high"`
- `sizes` attribute accurately reflects CSS layout widths

---

## Patterns

### Minimal — Add the essentials to an existing `<img>`

```html
<!-- Before -->
<img src="photo.jpg">

<!-- After -->
<img
  src="photo.jpg"
  alt="Descriptive text about the image"
  width="800"
  height="450"
  loading="lazy"
  decoding="async">
```

`width` and `height` prevent CLS. `loading="lazy"` defers off-screen images. `decoding="async"` frees the main thread.

---

### Responsive — `srcset` + `sizes`

Use when you have the same image at multiple resolutions:

```html
<img
  src="photo-800.jpg"
  srcset="photo-480.jpg 480w,
          photo-800.jpg 800w,
          photo-1200.jpg 1200w,
          photo-1920.jpg 1920w"
  sizes="(max-width: 640px) 100vw,
         (max-width: 1024px) 50vw,
         800px"
  alt="Descriptive alt text"
  width="800"
  height="450"
  loading="lazy"
  decoding="async">
```

**`sizes` formula:** match your CSS layout breakpoints.
- `100vw` = full viewport width
- `50vw` = half width (e.g., 2-column grid)
- `800px` = max-width constrained container

---

### Format fallback — `<picture>` with WebP + JPEG

Use when you want WebP for modern browsers, JPEG/PNG for Safari < 14 and older:

```html
<picture>
  <source
    type="image/webp"
    srcset="photo-480.webp 480w,
            photo-800.webp 800w,
            photo-1200.webp 1200w"
    sizes="(max-width: 640px) 100vw, 800px">
  <img
    src="photo-800.jpg"
    srcset="photo-480.jpg 480w,
            photo-800.jpg 800w,
            photo-1200.jpg 1200w"
    sizes="(max-width: 640px) 100vw, 800px"
    alt="Descriptive alt text"
    width="800"
    height="450"
    loading="lazy"
    decoding="async">
</picture>
```

Note: `<source>` handles the format selection; `<img>` is the required fallback and must carry `alt`, `width`, `height`.

---

### Art direction — `<picture>` with different crops per breakpoint

Use when mobile gets a portrait crop and desktop gets a landscape crop:

```html
<picture>
  <!-- Mobile: portrait crop -->
  <source
    media="(max-width: 767px)"
    srcset="photo-mobile-750x1000.webp"
    type="image/webp">
  <source
    media="(max-width: 767px)"
    srcset="photo-mobile-750x1000.jpg">

  <!-- Desktop: landscape crop -->
  <source
    srcset="photo-desktop-1920x800.webp"
    type="image/webp">

  <!-- Fallback -->
  <img
    src="photo-desktop-1920x800.jpg"
    alt="Descriptive alt text"
    width="1920"
    height="800"
    loading="eager"
    fetchpriority="high">
</picture>
```

---

### Hero / LCP image — above the fold

The Largest Contentful Paint element must **not** be lazy-loaded:

```html
<img
  src="hero-1200.jpg"
  srcset="hero-768.jpg 768w,
          hero-1200.jpg 1200w,
          hero-1920.jpg 1920w"
  sizes="100vw"
  alt="Hero image: [description]"
  width="1920"
  height="1080"
  loading="eager"
  fetchpriority="high"
  decoding="sync">
```

- `loading="eager"` — load immediately, don't defer
- `fetchpriority="high"` — tell the browser this is critical
- `decoding="sync"` — decode before next paint (avoids flash)

---

### Blur-up placeholder

Show a tiny blurred version while the full image loads:

```html
<div class="img-wrap">
  <!-- Inline base64 tiny placeholder (10px wide, same crop) -->
  <img
    class="img-placeholder"
    src="data:image/jpeg;base64,/9j/4AAQSkZJRgAB..."
    aria-hidden="true"
    alt="">
  <!-- Full image loads on top -->
  <img
    class="img-full"
    src="photo-800.jpg"
    alt="Descriptive alt text"
    width="800"
    height="450"
    loading="lazy"
    decoding="async">
</div>
```

```css
.img-wrap {
  position: relative;
  overflow: hidden;
}
.img-placeholder {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: blur(20px);
  transform: scale(1.1); /* hide blur edge artifacts */
  transition: opacity 0.3s;
}
.img-full {
  display: block;
  width: 100%;
  height: auto;
}
.img-full.loaded ~ .img-placeholder {
  opacity: 0;
}
```

```js
document.querySelectorAll('.img-full').forEach(img => {
  if (img.complete) img.classList.add('loaded');
  else img.addEventListener('load', () => img.classList.add('loaded'));
});
```

Generate a base64 placeholder: `cwebp -q 1 -resize 10 0 input.jpg -o - | base64`

---

### CSS background image — no `<picture>` available

```css
.hero {
  background-image: url('hero.jpg');
  background-size: cover;
  background-position: center;
}

/* WebP for browsers that support it */
@supports (background-image: url('x.webp')) {
  .hero { background-image: url('hero.webp'); }
}

/* Responsive background (media queries for file size) */
@media (max-width: 768px) {
  .hero { background-image: url('hero-mobile.jpg'); }
  @supports (background-image: url('x.webp')) {
    .hero { background-image: url('hero-mobile.webp'); }
  }
}
```

---

## Checklist

Apply this to every `<img>` in a project:

- [ ] `alt` attribute present (empty `alt=""` for purely decorative images)
- [ ] `width` and `height` attributes set to the intrinsic image dimensions
- [ ] `loading="lazy"` on all below-fold images
- [ ] `loading="eager"` + `fetchpriority="high"` on the hero / LCP image
- [ ] `srcset` + `sizes` if the image renders at different widths across breakpoints
- [ ] `<picture>` with WebP `<source>` if WebP versions are available
- [ ] File size within targets (see `references/image-sizing.md`)
- [ ] `decoding="async"` on below-fold images
- [ ] No missing dimensions on `<source>` elements inside `<picture>`

---

## Framework-Specific Notes

### Next.js
Use `next/image` — it handles srcset, WebP conversion, lazy loading, and placeholder blur automatically:
```jsx
import Image from 'next/image'
<Image src="/photo.jpg" alt="..." width={800} height={450} />
```

### Nuxt / Vue
Use `@nuxt/image` or `<NuxtImg>` — same automatic optimization as Next.js.

### Astro
Use `<Image>` from `astro:assets` — handles WebP conversion and srcset generation at build time.

### Gatsby
Use `gatsby-plugin-image` with `GatsbyImage` component.

### Vanilla HTML
Generate WebP and multiple sizes at build time with `sharp` (Node.js) or `imagemagick`. Use the `<picture>` + `srcset` patterns above manually.
