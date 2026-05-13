# Icon Library Reference

## Heroicons

**By:** Tailwind Labs  
**License:** MIT  
**Site:** https://heroicons.com  
**GitHub:** https://github.com/tailwindlabs/heroicons

### Variants
- `24/outline` — 24×24, stroke-based (stroke-width 1.5)
- `24/solid` — 24×24, filled
- `20/solid` — 20×20, filled (compact UI)
- `16/solid` — 16×16, filled (inline text)

### CDN (unpkg)
```html
<!-- No CDN for individual icons — use npm or raw GitHub URLs -->
```

### Raw SVG URLs
```
https://raw.githubusercontent.com/tailwindlabs/heroicons/master/src/24/outline/{name}.svg
https://raw.githubusercontent.com/tailwindlabs/heroicons/master/src/24/solid/{name}.svg
https://raw.githubusercontent.com/tailwindlabs/heroicons/master/src/20/solid/{name}.svg
```

### NPM (React)
```bash
npm install @heroicons/react
```
```jsx
import { ArrowRightIcon } from '@heroicons/react/24/outline'
```

### NPM (Vue)
```bash
npm install @heroicons/vue
```
```vue
import { ArrowRightIcon } from '@heroicons/vue/24/outline'
```

### Key Icon Names (Common UI)
`arrow-right`, `arrow-left`, `chevron-down`, `chevron-up`, `chevron-right`, `x-mark`, `check`, `plus`, `minus`, `magnifying-glass`, `bars-3`, `user`, `user-circle`, `bell`, `cog-6-tooth`, `pencil`, `trash`, `document`, `folder`, `home`, `heart`, `star`, `share`, `link`, `external-link`, `eye`, `eye-slash`, `lock-closed`, `lock-open`, `shield-check`, `exclamation-triangle`, `information-circle`, `question-mark-circle`, `check-circle`, `x-circle`, `photo`, `film`, `chat-bubble-left`, `envelope`, `phone`, `map-pin`, `calendar`, `clock`, `sun`, `moon`, `globe-alt`, `cloud`, `arrow-up-tray`, `arrow-down-tray`, `clipboard`

---

## Lucide

**By:** Community (fork of Feather Icons)  
**License:** ISC  
**Site:** https://lucide.dev  
**GitHub:** https://github.com/lucide-icons/lucide

### Style
Single style — consistent 2px stroke, 24×24 viewBox. Clean, modern outline style.

### CDN (single icons)
```html
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>
<i data-lucide="arrow-right"></i>
<script>lucide.createIcons();</script>
```

### Raw SVG URLs
```
https://unpkg.com/lucide-static@latest/icons/{name}.svg
```

### NPM (React)
```bash
npm install lucide-react
```
```jsx
import { ArrowRight, Search, User } from 'lucide-react'
```

### NPM (Vue)
```bash
npm install lucide-vue-next
```

### Key Icon Names (1,500+ available — searchable at lucide.dev/icons)
`arrow-right`, `arrow-left`, `chevron-down`, `x`, `check`, `plus`, `minus`, `search`, `menu`, `user`, `user-circle`, `bell`, `settings`, `edit`, `trash-2`, `file`, `folder`, `home`, `heart`, `star`, `share-2`, `link`, `external-link`, `eye`, `eye-off`, `lock`, `unlock`, `shield`, `alert-triangle`, `info`, `help-circle`, `check-circle`, `x-circle`, `image`, `video`, `message-circle`, `mail`, `phone`, `map-pin`, `calendar`, `clock`, `sun`, `moon`, `globe`, `cloud`, `upload`, `download`, `copy`, `log-in`, `log-out`, `refresh-cw`, `loader`, `zap`, `trending-up`, `bar-chart-2`, `pie-chart`, `layers`, `grid`, `list`, `layout`, `package`, `shopping-cart`, `credit-card`, `dollar-sign`

---

## Phosphor Icons

**By:** Phosphor Icons  
**License:** MIT  
**Site:** https://phosphoricons.com  
**GitHub:** https://github.com/phosphor-icons/core

### Variants (6 weights)
- `thin` — 0.75px stroke equivalent
- `light` — 1px stroke
- `regular` — balanced (default)
- `bold` — heavy stroke
- `fill` — solid fill
- `duotone` — two-layer with opacity (distinctive style)

### CDN (all icons via web component)
```html
<script src="https://unpkg.com/@phosphor-icons/web@2/src/index.js" type="module"></script>
<ph-arrow-right></ph-arrow-right>
<ph-arrow-right weight="bold"></ph-arrow-right>
<ph-arrow-right weight="duotone"></ph-arrow-right>
```

### Raw SVG URLs
```
https://unpkg.com/@phosphor-icons/core@2/assets/regular/{name}.svg
https://unpkg.com/@phosphor-icons/core@2/assets/bold/{name}.svg
https://unpkg.com/@phosphor-icons/core@2/assets/fill/{name}.svg
https://unpkg.com/@phosphor-icons/core@2/assets/duotone/{name}.svg
```

### NPM (React)
```bash
npm install @phosphor-icons/react
```
```jsx
import { ArrowRight, MagnifyingGlass } from '@phosphor-icons/react'
// <ArrowRight size={24} weight="duotone" />
```

### Duotone SVG Structure
Duotone icons have two paths — use opacity on the background layer:
```html
<svg viewBox="0 0 256 256" fill="currentColor">
  <path d="..." opacity="0.2"/>  <!-- background layer, 20% opacity -->
  <path d="..."/>                 <!-- foreground layer, full opacity -->
</svg>
```
Set both paths to the same `fill` color; the opacity creates the two-tone effect.

---

## Tabler Icons

**By:** Tabler / codecalm  
**License:** MIT  
**Site:** https://tabler.io/icons  
**GitHub:** https://github.com/tabler/tabler-icons

### Variants
- Outline (default) — 2px stroke, 24×24 viewBox
- Filled — available for subset of icons

### CDN (sprite sheet approach)
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css">
<i class="ti ti-arrow-right"></i>
```

### Raw SVG URLs
```
https://raw.githubusercontent.com/tabler/tabler-icons/main/icons/outline/{name}.svg
https://raw.githubusercontent.com/tabler/tabler-icons/main/icons/filled/{name}.svg
```

### NPM (React)
```bash
npm install @tabler/icons-react
```
```jsx
import { IconArrowRight, IconSearch } from '@tabler/icons-react'
```

### Tabler-specific naming (note: uses underscores in web font, hyphens in SVG files)
Icon names use hyphens in file names: `icon-name.svg`

---

## Material Symbols (Google)

**By:** Google  
**License:** Apache 2.0  
**Site:** https://fonts.google.com/icons  
**GitHub:** https://github.com/google/material-design-icons

### Variants
- Outlined
- Rounded
- Sharp

### CDN (variable font — recommended)
```html
<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" rel="stylesheet">
<span class="material-symbols-outlined">home</span>
```

Adjust the variable font axes:
- `opsz` 20–48 (optical size)
- `wght` 100–700 (weight)
- `FILL` 0–1 (0 = outline, 1 = filled)
- `GRAD` -50–200 (grade/contrast)

### CSS for filled variant
```css
.material-symbols-outlined {
  font-variation-settings: 'FILL' 1, 'wght' 400, 'GRAD' 0, 'opsz' 24;
}
```

### Icon Names
Use lowercase with underscores: `home`, `search`, `arrow_forward`, `close`, `menu`, `person`, `settings`, `edit`, `delete`, `add`, `check`, `star`, `favorite`, `share`, `notifications`, `lock`, `visibility`, `visibility_off`, `shopping_cart`, `download`, `upload`, `image`, `calendar_today`, `schedule`, `location_on`, `email`, `phone`, `language`, `dark_mode`, `light_mode`

---

## Choosing Between Libraries

| Situation | Recommendation |
|-----------|---------------|
| Tailwind project | Heroicons — designed by same team |
| React SPA | Lucide React — tree-shakeable, active community |
| Vue project | Lucide Vue Next or Tabler |
| Vanilla HTML, no bundler | Phosphor web components or Tabler webfont |
| Need 4,000+ icons | Tabler |
| Need duotone / decorative icons | Phosphor |
| Material UI / Google design | Material Symbols |
| Need variable weight icons | Material Symbols (variable font) |
| Marketing / landing page | Phosphor (bold or duotone stand out) |
| Dashboard / data tables | Tabler (dense, consistent) |
