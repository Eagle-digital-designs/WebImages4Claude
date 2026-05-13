# Color Variants Reference

## Tailwind Color Swatches (500 & 600 — primary icon weights)

| Name | 500 | 600 | Usage |
|------|-----|-----|-------|
| Slate | `#64748b` | `#475569` | Neutral UI, secondary icons |
| Gray | `#6b7280` | `#4b5563` | Neutral UI |
| Zinc | `#71717a` | `#52525b` | Cool neutral |
| Neutral | `#737373` | `#525252` | True neutral |
| Stone | `#78716c` | `#57534e` | Warm neutral |
| Red | `#ef4444` | `#dc2626` | Error, danger, delete |
| Orange | `#f97316` | `#ea580c` | Warning (warm), CTA |
| Amber | `#f59e0b` | `#d97706` | Warning, caution |
| Yellow | `#eab308` | `#ca8a04` | Highlight, notice |
| Lime | `#84cc16` | `#65a30d` | Success (bright) |
| Green | `#22c55e` | `#16a34a` | Success, confirm |
| Emerald | `#10b981` | `#059669` | Success (teal-green) |
| Teal | `#14b8a6` | `#0d9488` | Accent, active state |
| Cyan | `#06b6d4` | `#0891b2` | Info, links |
| Sky | `#0ea5e9` | `#0284c7` | Info (bright blue) |
| Blue | `#3b82f6` | `#2563eb` | Primary action |
| Indigo | `#6366f1` | `#4f46e5` | Brand, primary (purple-blue) |
| Violet | `#8b5cf6` | `#7c3aed` | Brand, creative |
| Purple | `#a855f7` | `#9333ea` | Brand, creative |
| Fuchsia | `#d946ef` | `#c026d3` | Accent, creative |
| Pink | `#ec4899` | `#db2777` | Accent, feminine |
| Rose | `#f43f5e` | `#e11d48` | Error (warm), heart |

## Dark Mode Pairs (600 light → 400 dark)

| Semantic | Light (`600`) | Dark (`400`) | Tailwind class |
|----------|--------------|-------------|----------------|
| Primary blue | `#2563eb` | `#60a5fa` | `text-blue-600 dark:text-blue-400` |
| Success green | `#16a34a` | `#4ade80` | `text-green-600 dark:text-green-400` |
| Warning amber | `#d97706` | `#fbbf24` | `text-amber-600 dark:text-amber-400` |
| Danger red | `#dc2626` | `#f87171` | `text-red-600 dark:text-red-400` |
| Info cyan | `#0891b2` | `#22d3ee` | `text-cyan-600 dark:text-cyan-400` |
| Brand violet | `#7c3aed` | `#a78bfa` | `text-violet-600 dark:text-violet-400` |
| Muted slate | `#475569` | `#94a3b8` | `text-slate-600 dark:text-slate-400` |

## Common Brand Color Presets

### Corporate / SaaS (trust, professionalism)
```css
:root {
  --icon-primary:   #2563eb;  /* blue-600 */
  --icon-success:   #16a34a;  /* green-600 */
  --icon-warning:   #d97706;  /* amber-600 */
  --icon-danger:    #dc2626;  /* red-600 */
  --icon-muted:     #64748b;  /* slate-500 */
}
```

### Creative / Agency (bold, vibrant)
```css
:root {
  --icon-primary:   #7c3aed;  /* violet-600 */
  --icon-accent:    #ec4899;  /* pink-500 */
  --icon-success:   #10b981;  /* emerald-500 */
  --icon-warning:   #f97316;  /* orange-500 */
  --icon-danger:    #f43f5e;  /* rose-500 */
  --icon-muted:     #6b7280;  /* gray-500 */
}
```

### Medical / Health (calm, trustworthy)
```css
:root {
  --icon-primary:   #0891b2;  /* cyan-600 */
  --icon-accent:    #14b8a6;  /* teal-500 */
  --icon-success:   #16a34a;  /* green-600 */
  --icon-warning:   #d97706;  /* amber-600 */
  --icon-danger:    #dc2626;  /* red-600 */
  --icon-muted:     #64748b;  /* slate-500 */
}
```

### Finance / Fintech (reliable, premium)
```css
:root {
  --icon-primary:   #1d4ed8;  /* blue-700 */
  --icon-accent:    #0d9488;  /* teal-600 */
  --icon-success:   #15803d;  /* green-700 */
  --icon-warning:   #b45309;  /* amber-700 */
  --icon-danger:    #b91c1c;  /* red-700 */
  --icon-muted:     #475569;  /* slate-600 */
}
```

### E-commerce (action-oriented, energetic)
```css
:root {
  --icon-primary:   #ea580c;  /* orange-600 */
  --icon-accent:    #dc2626;  /* red-600 */
  --icon-success:   #16a34a;  /* green-600 */
  --icon-warning:   #ca8a04;  /* yellow-600 */
  --icon-cart:      #2563eb;  /* blue-600 */
  --icon-muted:     #6b7280;  /* gray-500 */
}
```

## Duotone Color Pairs

For Phosphor duotone icons, these pairs work well (background layer at 20% opacity):

| Name | Foreground | Background (20% opacity) |
|------|-----------|--------------------------|
| Ocean | `#0284c7` sky-600 | same at 20% |
| Forest | `#15803d` green-700 | same at 20% |
| Sunset | `#ea580c` orange-600 | same at 20% |
| Berry | `#7c3aed` violet-600 | same at 20% |
| Rose | `#be123c` rose-700 | same at 20% |
| Slate | `#334155` slate-700 | same at 20% |
| Amber | `#b45309` amber-700 | same at 20% |

Two-color duotone (contrasting layers):

| Name | Foreground | Background |
|------|-----------|-----------|
| Brand highlight | `#1e3a8a` blue-900 | `#bfdbfe` blue-200 |
| Success soft | `#14532d` green-900 | `#bbf7d0` green-200 |
| Warning soft | `#78350f` amber-900 | `#fde68a` amber-200 |
| Danger soft | `#7f1d1d` red-900 | `#fecaca` red-200 |

## CSS Custom Property Full Template

Full ready-to-use icon token system:

```css
:root {
  /* Semantic tokens */
  --icon-primary:      #2563eb;
  --icon-primary-hover:#1d4ed8;
  --icon-secondary:    #64748b;
  --icon-success:      #16a34a;
  --icon-warning:      #d97706;
  --icon-danger:       #dc2626;
  --icon-info:         #0891b2;
  --icon-muted:        #94a3b8;
  --icon-inverse:      #ffffff;

  /* Duotone helper */
  --icon-duotone-opacity: 0.2;
}

@media (prefers-color-scheme: dark) {
  :root {
    --icon-primary:      #60a5fa;
    --icon-primary-hover:#93c5fd;
    --icon-secondary:    #94a3b8;
    --icon-success:      #4ade80;
    --icon-warning:      #fbbf24;
    --icon-danger:       #f87171;
    --icon-info:         #22d3ee;
    --icon-muted:        #475569;
    --icon-inverse:      #0f172a;
  }
}

/* Utility classes */
.icon-primary   { color: var(--icon-primary); }
.icon-secondary { color: var(--icon-secondary); }
.icon-success   { color: var(--icon-success); }
.icon-warning   { color: var(--icon-warning); }
.icon-danger    { color: var(--icon-danger); }
.icon-info      { color: var(--icon-info); }
.icon-muted     { color: var(--icon-muted); }
.icon-inverse   { color: var(--icon-inverse); }
```
