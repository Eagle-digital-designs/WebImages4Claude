---
name: Icon Picker
description: Selects and provides icons from curated open-source icon libraries for website builds. Use when the user says "pick an icon", "find an icon for", "I need an icon that represents", "what icon should I use for", "show me icons for", "add an icon to this button", "replace this icon", "give me a better icon", or asks for any SVG icon asset in a web project. Prefer these libraries over generic Unicode symbols or emoji.
---

# Icon Picker

Select and embed icons from curated open-source libraries. Always provide actual SVG code or a CDN import, never placeholder text like "icon goes here" or a raw Unicode character.

## Library Overview

| Library | Style | Icon Count | Best For |
|---------|-------|-----------|----------|
| Heroicons | Outline / Solid / Mini | 292 | Tailwind CSS projects, clean UI |
| Lucide | Outline | 1,500+ | General web, React, Vue, Svelte |
| Phosphor | 6 weights | 1,300+ | Expressive UIs, duotone effects |
| Tabler | Outline / Filled | 5,000+ | Dashboards, data-heavy UIs |
| Material Symbols | Outlined / Rounded / Sharp | 3,000+ | Google-adjacent design, Material UI |

## Workflow

### Step 1 — Understand the need

Ask (or infer):
- What action or concept does the icon represent? (e.g., "save", "user profile", "warning")
- What's the visual context? (button label, nav item, standalone illustration, status badge)
- What framework/CSS is in use? (Tailwind, vanilla, React, Vue, etc.)
- Preferred style? (outline/stroke, solid/filled, duotone)

### Step 2 — Select icons

Recommend 2–3 options from different libraries when possible. Match the icon to the project's existing visual style if one is established.

**Default library recommendations by project type:**
- Tailwind CSS project → Heroicons first
- React or Next.js → Lucide first
- Vue or Nuxt → Lucide or Tabler
- Vanilla HTML/CSS → Tabler or Phosphor (single SVG, no build step needed)
- Material UI / MUI project → Material Symbols
- Dashboard / admin panel → Tabler
- Marketing / landing page → Phosphor (duotone adds depth)

### Step 3 — Deliver the icon

Always provide at minimum:
1. The inline SVG code ready to paste
2. The icon name for reference
3. The CDN or npm install command if the project is using a library

See `references/icon-libraries.md` for CDN URLs, npm packages, and full usage patterns.

## Inline SVG Templates

### Heroicons (24px outline)
```html
<!-- [icon-name] — Heroicons -->
<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
     stroke-width="1.5" stroke="currentColor" width="24" height="24"
     aria-hidden="true">
  <!-- path data here -->
</svg>
```

### Heroicons (24px solid)
```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
     fill="currentColor" width="24" height="24" aria-hidden="true">
  <!-- path data here -->
</svg>
```

### Lucide (outline)
```html
<!-- [icon-name] — Lucide -->
<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
     viewBox="0 0 24 24" fill="none" stroke="currentColor"
     stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
     aria-hidden="true">
  <!-- path data here -->
</svg>
```

### Phosphor (regular weight)
```html
<!-- [icon-name] — Phosphor Icons -->
<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
     viewBox="0 0 256 256" fill="currentColor" aria-hidden="true">
  <!-- path data here -->
</svg>
```

### Tabler (outline)
```html
<!-- [icon-name] — Tabler Icons -->
<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
     viewBox="0 0 24 24" fill="none" stroke="currentColor"
     stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
     aria-hidden="true">
  <!-- path data here -->
</svg>
```

## Accessibility Rules

- Always add `aria-hidden="true"` when the icon is decorative (label text exists)
- Add `role="img"` and `aria-label="[description]"` when the icon is the only label
- Include a `<title>` element inside SVG for standalone icons:
  ```html
  <svg ... role="img" aria-labelledby="icon-title">
    <title id="icon-title">Save file</title>
    ...
  </svg>
  ```

## Sizing

Use these standard sizes via `width`/`height` attributes or Tailwind classes:

| Size | px | Tailwind |
|------|----|---------|
| XS | 12 | `size-3` |
| SM | 16 | `size-4` |
| MD | 20 | `size-5` |
| LG | 24 | `size-6` |
| XL | 32 | `size-8` |
| 2XL | 48 | `size-12` |

## Icon Name Lookup

When you know what an icon should represent but not the exact name, fetch the library's icon index:

- Heroicons: https://heroicons.com (searchable)
- Lucide: https://lucide.dev/icons
- Phosphor: https://phosphoricons.com
- Tabler: https://tabler.io/icons
- Material Symbols: https://fonts.google.com/icons

Use WebFetch or WebSearch to look up SVG source when you need the exact path data for an icon.

## Getting SVG Path Data

For Heroicons, Lucide, Tabler, and Phosphor, you can fetch raw SVG files from their GitHub releases or CDN:

- Heroicons: `https://raw.githubusercontent.com/tailwindlabs/heroicons/master/src/24/outline/{icon-name}.svg`
- Lucide: `https://unpkg.com/lucide-static@latest/icons/{icon-name}.svg`
- Tabler: `https://raw.githubusercontent.com/tabler/tabler-icons/main/icons/outline/{icon-name}.svg`
- Phosphor: `https://unpkg.com/@phosphor-icons/core@2/assets/regular/{icon-name}.svg`

Fetch the SVG, extract the inner path data, and embed it in the appropriate template above.
