# Web Image Sizing Reference

Standard dimensions, aspect ratios, and format guidance for every common image placement on a website.

---

## Hero / Banner Images

| Use Case | Recommended Size | Aspect Ratio | Notes |
|----------|-----------------|--------------|-------|
| Full-width hero | 1920×1080 | 16:9 | Cover for all desktop widths |
| Wide hero (short) | 1920×600 | 16:5 | Common for marketing sections |
| Centered hero | 1200×675 | 16:9 | Max-width container |
| Mobile hero | 750×1000 | 3:4 | Portrait crop for mobile-first |
| Split-screen hero | 960×1080 | 1:1.12 | Half-width panel |

**srcset breakpoints:** 480w, 768w, 1024w, 1440w, 1920w  
**Format:** WebP (with JPEG fallback)  
**Loading:** `loading="eager"` — hero is above the fold

---

## Cards & Thumbnails

| Use Case | Recommended Size | Aspect Ratio | Notes |
|----------|-----------------|--------------|-------|
| Blog card | 800×450 | 16:9 | Standard post thumbnail |
| Square card | 600×600 | 1:1 | Product, team, portfolio |
| Portrait card | 400×600 | 2:3 | Magazine, book, person |
| Wide card | 800×300 | 8:3 | Feature/promo banner card |
| Mini thumbnail | 200×200 | 1:1 | Sidebar, related posts |

**srcset breakpoints:** 400w, 600w, 800w  
**Format:** WebP  
**Loading:** `loading="lazy"`

---

## Team / People Photos

| Use Case | Recommended Size | Aspect Ratio | Notes |
|----------|-----------------|--------------|-------|
| Team grid headshot | 600×600 | 1:1 | Crop face to center |
| Bio page portrait | 800×1000 | 4:5 | More formal, editorial |
| Avatar / small | 128×128 | 1:1 | Nav, comment threads |
| Avatar / medium | 256×256 | 1:1 | Profile pages |
| Testimonial avatar | 80×80 | 1:1 | Used at tiny display size |

**Format:** WebP or JPEG (faces compress well)  
**Loading:** `loading="lazy"` unless above the fold

---

## Background Images

| Use Case | Recommended Size | Aspect Ratio | Notes |
|----------|-----------------|--------------|-------|
| Full-page background | 1920×1080 | 16:9 | `background-size: cover` |
| Section background | 1920×800 | 12:5 | Fixed-height section |
| Pattern / texture | 400×400 | 1:1 | Tiled via `background-repeat` |
| Subtle texture | 100×100 | 1:1 | Micro-pattern, tile |

**Format:** WebP or compressed JPEG  
**CSS:** `background-image: url(...)` — cannot use `<picture>` for format fallback  
**Workaround for WebP fallback in CSS:**
```css
.hero { background-image: url('hero.jpg'); }
@supports (background-image: url('x.webp')) {
  .hero { background-image: url('hero.webp'); }
}
```

---

## Social Media / Open Graph Images

| Platform | Required Size | Aspect Ratio | Notes |
|----------|--------------|--------------|-------|
| OG / Facebook | 1200×630 | 1.91:1 | Works for most platforms |
| Twitter / X card | 1200×628 | ~1.91:1 | Summary large image |
| Twitter / X square | 800×800 | 1:1 | Summary card |
| LinkedIn post | 1200×628 | 1.91:1 | Article header |
| Instagram feed | 1080×1080 | 1:1 | Square |
| Instagram story | 1080×1920 | 9:16 | Portrait |
| Pinterest pin | 1000×1500 | 2:3 | Tall |

**HTML meta tags:**
```html
<meta property="og:image" content="https://example.com/og-image.jpg">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:image" content="https://example.com/og-image.jpg">
```

---

## Favicon & App Icons

| Icon | Size | Format | Notes |
|------|------|--------|-------|
| Favicon (modern) | 32×32 | PNG or SVG | `<link rel="icon">` |
| Favicon (legacy) | 16×16 | ICO | Embedded in `.ico` |
| Apple Touch Icon | 180×180 | PNG | iOS home screen |
| Android Chrome | 192×192 | PNG | Manifest icon |
| Android Chrome HD | 512×512 | PNG | Splash screen |
| Windows tile | 270×270 | PNG | mstile |
| Safari Pinned Tab | Any | SVG (monochrome) | Single color only |

**Minimal `<head>` favicon block:**
```html
<link rel="icon" type="image/png" href="/favicon-32.png" sizes="32x32">
<link rel="icon" type="image/png" href="/favicon-16.png" sizes="16x16">
<link rel="apple-touch-icon" href="/apple-touch-icon.png" sizes="180x180">
<link rel="manifest" href="/site.webmanifest">
```

---

## Logo

| Use Case | Max Width | Format | Notes |
|----------|----------|--------|-------|
| Nav bar logo | 200px wide | SVG preferred | Scales perfectly |
| Footer logo | 160px wide | SVG or PNG 2× | |
| Favicon-size logo | 32×32 | PNG | Separate simplified mark |
| Email header logo | 240px wide | PNG (2× = 480px) | Retina email clients |

**Always use SVG for logos** — infinitely scalable, tiny file size, color-customizable via CSS.  
If only a raster image is available, supply 2× PNG (double the display size).

---

## Product Images

| Use Case | Recommended Size | Aspect Ratio | Notes |
|----------|-----------------|--------------|-------|
| Product grid thumb | 600×600 | 1:1 | Consistent grid layout |
| Product detail main | 1200×1200 | 1:1 | Zoom-capable |
| Product alt view | 800×800 | 1:1 | Same crop as main |
| Product on white | 800×800 | 1:1 | Cutout / pure white bg |
| Lifestyle / in-use | 1200×800 | 3:2 | Contextual |

---

## File Size Targets

| Image Role | Target File Size | Notes |
|-----------|-----------------|-------|
| Hero (1920px) | < 200 KB | WebP at 80% quality |
| Card / blog thumb | < 60 KB | WebP at 75% quality |
| Background | < 150 KB | Compress aggressively |
| Avatar / headshot | < 30 KB | Small display size |
| OG image | < 300 KB | External platforms cache it |
| Logo (SVG) | < 10 KB | Optimize SVG markup |
| Logo (PNG) | < 20 KB | Transparent PNG |

**Quick quality settings (ImageMagick / cwebp):**
```bash
# WebP conversion
cwebp -q 80 input.jpg -o output.webp

# JPEG optimization
magick input.jpg -quality 82 -sampling-factor 4:2:0 -strip output.jpg

# PNG optimization
pngquant --quality=65-80 --output output.png input.png
```

---

## CSS `object-fit` Patterns

Use these when displaying images in fixed-size containers:

```css
/* Fill container, crop to fit — most common for cards */
.card-image {
  width: 100%;
  aspect-ratio: 16 / 9;
  object-fit: cover;
  object-position: center top; /* keep faces in frame */
}

/* Contain full image, letterbox if needed — good for logos/products */
.product-image {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: contain;
  background: #f8f8f8;
}

/* Responsive hero, always fills viewport */
.hero-image {
  width: 100%;
  height: 100vh;
  max-height: 800px;
  object-fit: cover;
  object-position: center 30%; /* shift down to keep subject visible */
}
```
