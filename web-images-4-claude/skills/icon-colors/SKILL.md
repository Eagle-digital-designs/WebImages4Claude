---
name: Icon Colors
description: Generates color variants of SVG icons for website builds. Use when the user says "make the icon blue", "change icon color", "icon in different colors", "create a color variant of this icon", "themed icons", "icon color palette", "match the icon to the brand", "dark mode icon", "icon with two colors", "duotone icon", or when applying a color scheme to icons across a project.
---

# Icon Colors

Apply colors to SVG icons using inline SVG properties, CSS custom properties, or Tailwind classes. Handle single-color, duotone, and multi-color variants.

## Core Concepts

SVG icons use three color vectors:
- `fill` — fills solid shapes
- `stroke` — draws outline paths
- `currentColor` — inherits from CSS `color` property (most flexible)

Most modern icon libraries default to `currentColor`, which means setting CSS `color` on a parent element controls the icon color automatically.

## Workflow

### Step 1 — Identify current icon structure

Check whether the SVG uses:
- `fill="currentColor"` → controlled by CSS `color`
- `stroke="currentColor"` → controlled by CSS `color`
- Hard-coded hex values → must be replaced
- Multiple `<path>` elements with different opacities → duotone pattern

### Step 2 — Determine color target

Ask or infer:
- What color(s) should the icon be?
- Is this a one-off or applied to all icons in the project?
- Does the project use Tailwind, CSS variables, or plain hex?
- Is dark mode support needed?

### Step 3 — Apply the color

See patterns below. Always prefer `currentColor` over hard-coded hex in the SVG — keep color control at the CSS level.

## Color Patterns

### Pattern 1 — CSS color class (Tailwind)

For `currentColor`-based icons, wrap in a span or apply the class to the SVG directly:

```html
<!-- Blue icon -->
<svg class="text-blue-600" ...>...</svg>

<!-- Red icon -->
<svg class="text-red-500" ...>...</svg>

<!-- Inherits parent text color -->
<button class="text-white hover:text-blue-300">
  <svg ...>...</svg>
  Save
</button>
```

### Pattern 2 — CSS custom properties (design tokens)

```css
:root {
  --icon-primary: #2563eb;    /* blue-600 */
  --icon-secondary: #64748b;  /* slate-500 */
  --icon-success: #16a34a;    /* green-600 */
  --icon-warning: #d97706;    /* amber-600 */
  --icon-danger: #dc2626;     /* red-600 */
  --icon-muted: #94a3b8;      /* slate-400 */
}

@media (prefers-color-scheme: dark) {
  :root {
    --icon-primary: #60a5fa;   /* blue-400 */
    --icon-secondary: #94a3b8; /* slate-400 */
    --icon-success: #4ade80;   /* green-400 */
    --icon-warning: #fbbf24;   /* amber-400 */
    --icon-danger: #f87171;    /* red-400 */
    --icon-muted: #475569;     /* slate-600 */
  }
}
```

Apply to icons:
```html
<svg style="color: var(--icon-primary)" ...>...</svg>
```
Or with a utility class:
```css
.icon-primary { color: var(--icon-primary); }
.icon-danger  { color: var(--icon-danger); }
```

### Pattern 3 — Duotone (two-color)

Duotone uses one color at two opacity levels. Structure:

```html
<svg viewBox="0 0 256 256" aria-hidden="true">
  <!-- Background layer — same color, reduced opacity -->
  <path fill="#2563eb" opacity="0.2" d="[background-path]"/>
  <!-- Foreground layer — full opacity -->
  <path fill="#2563eb" d="[foreground-path]"/>
</svg>
```

With CSS variables for theming:
```html
<svg style="--icon-color: #2563eb" viewBox="0 0 256 256">
  <path fill="var(--icon-color)" opacity="0.2" d="..."/>
  <path fill="var(--icon-color)" d="..."/>
</svg>
```

Change the color with a single variable update.

### Pattern 4 — Two distinct colors

For icons with semantically different parts:
```html
<svg viewBox="0 0 24 24">
  <path fill="#1e293b" d="[base shape]"/>        <!-- slate-900 body -->
  <path fill="#2563eb" d="[accent element]"/>    <!-- blue-600 accent -->
</svg>
```

CSS custom property version:
```css
.icon-branded {
  --icon-base: var(--color-slate-900);
  --icon-accent: var(--color-brand-blue);
}
```
```html
<svg class="icon-branded">
  <path fill="var(--icon-base)" d="..."/>
  <path fill="var(--icon-accent)" d="..."/>
</svg>
```

### Pattern 5 — Gradient fill

```html
<svg viewBox="0 0 24 24">
  <defs>
    <linearGradient id="icon-grad" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#6366f1"/>   <!-- indigo-500 -->
      <stop offset="100%" stop-color="#8b5cf6"/>  <!-- violet-500 -->
    </linearGradient>
  </defs>
  <path fill="url(#icon-grad)" d="..."/>
</svg>
```

Note: gradient IDs must be unique per page. Use a descriptive prefix: `id="icon-grad-[icon-name]"`.

## Tailwind Color Reference

Common icon colors by semantic role:

| Role | Light mode | Dark mode | Tailwind classes |
|------|-----------|-----------|-----------------|
| Primary action | `#2563eb` | `#60a5fa` | `text-blue-600 dark:text-blue-400` |
| Secondary / muted | `#64748b` | `#94a3b8` | `text-slate-500 dark:text-slate-400` |
| Success | `#16a34a` | `#4ade80` | `text-green-600 dark:text-green-400` |
| Warning | `#d97706` | `#fbbf24` | `text-amber-600 dark:text-amber-400` |
| Danger / error | `#dc2626` | `#f87171` | `text-red-600 dark:text-red-400` |
| Info | `#0891b2` | `#22d3ee` | `text-cyan-600 dark:text-cyan-400` |
| Brand purple | `#7c3aed` | `#a78bfa` | `text-violet-600 dark:text-violet-400` |
| Neutral / default | `#374151` | `#d1d5db` | `text-gray-700 dark:text-gray-300` |
| White (on dark bg) | `#ffffff` | `#ffffff` | `text-white` |

See `references/color-variants.md` for full Tailwind 500/600 color swatches and brand color presets.

## Batch Coloring Multiple Icons

When applying a consistent icon color scheme across a site:

1. Set a CSS class on the icon container or SVG elements
2. Use `currentColor` everywhere — never hard-code hex inside SVGs
3. Control all colors through CSS variables on `:root`

```css
/* Single source of truth */
:root {
  --icon-nav: #374151;
  --icon-nav-active: #2563eb;
  --icon-nav-hover: #1d4ed8;
}

.nav-icon { color: var(--icon-nav); }
.nav-icon:hover, .nav-item.active .nav-icon {
  color: var(--icon-nav-active);
}
```

```html
<nav>
  <a href="/" class="nav-item active">
    <svg class="nav-icon" ...>...</svg>
    Home
  </a>
  <a href="/about" class="nav-item">
    <svg class="nav-icon" ...>...</svg>
    About
  </a>
</nav>
```

## Dark Mode

When dark mode is required, always define both modes:

```css
/* Tailwind dark mode variant */
<svg class="text-slate-700 dark:text-slate-200" ...>...</svg>

/* Or CSS prefers-color-scheme */
:root { --icon-color: #374151; }
@media (prefers-color-scheme: dark) { :root { --icon-color: #e2e8f0; } }
```

For icons that need to invert on dark backgrounds, use CSS `filter`:
```css
.icon-auto-invert {
  filter: invert(0);
}
@media (prefers-color-scheme: dark) {
  .icon-auto-invert { filter: invert(1); }
}
```
This only works reliably for pure black/white icons.
