# Image Attribution Guide

## When Attribution Is Required

| Source | Attribution Required | Commercial Use |
|--------|---------------------|----------------|
| CC0 / Public Domain | Never | Yes |
| Unsplash License | No (encouraged) | Yes |
| Pexels License | No (encouraged) | Yes |
| Pixabay License | No (encouraged) | Yes |
| CC BY 4.0 | Yes | Yes |
| CC BY-SA 4.0 | Yes, share-alike | Yes |
| CC BY-ND 4.0 | Yes | Yes |
| CC BY-NC 4.0 | Yes | **No** |
| CC BY-NC-SA 4.0 | Yes | **No** |
| CC BY-NC-ND 4.0 | Yes | **No** |

## Attribution Templates

### HTML Comment (unobtrusive, for internal tracking)
```html
<!-- Image: "[Title]" by [Author] ([Source]) — [License] — [URL] -->
<img src="..." alt="..." loading="lazy">
```

### Visible Attribution (required for CC BY, recommended for others)
```html
<figure>
  <img src="..." alt="..." loading="lazy">
  <figcaption>
    Photo by <a href="[author-url]" target="_blank" rel="noopener">[Author Name]</a>
    on <a href="[source-url]" target="_blank" rel="noopener">[Source]</a>
  </figcaption>
</figure>
```

### Unsplash Standard Attribution
```html
<!-- Photo by [Photographer] on Unsplash — https://unsplash.com/photos/[id] -->
```
Or visibly: `Photo by [Name] on Unsplash`

### Wikimedia Commons Attribution
```html
<!-- "[Title]" by [Author], [License abbreviation], via Wikimedia Commons -->
<!-- Source: https://commons.wikimedia.org/wiki/File:[filename] -->
```

### OpenVerse Attribution
Use the pre-formatted `attribution` field from the API response — it includes all required elements in the correct format.

## Footer Attribution Block

For sites using many CC-licensed images, a single footer block is acceptable:

```html
<section id="image-credits" aria-label="Image credits">
  <h2>Image Credits</h2>
  <ul>
    <li>"Mountain Sunrise" by Jane Doe, CC BY 4.0, via Wikimedia Commons</li>
    <li>Hero photo by John Smith on Unsplash</li>
    <li>Background texture via Pixabay (Pixabay License)</li>
  </ul>
</section>
```

## What Makes a Valid CC Attribution

A valid CC BY attribution must include:
1. **Title** — the image's name (if available)
2. **Author** — the creator's name or username
3. **Source** — a URL back to the original
4. **License** — the full license name or URL (e.g., "CC BY 4.0" or link to creativecommons.org)
5. **Changes** — note if you modified the image (cropped, filtered, etc.)

## Share-Alike (SA) Warning

CC BY-SA images require that any derivative work (cropping, compositing, color adjusting) also be released under CC BY-SA. This means:
- Using a CC BY-SA image as a website background is fine (no derivative)
- Compositing it with other elements to create a new image creates a derivative — that new image must be CC BY-SA

Always warn the user when they select a CC BY-SA image for composite use.
