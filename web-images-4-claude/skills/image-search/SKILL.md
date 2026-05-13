---
name: Image Search
description: Searches for and sources free open-use images from the internet for website projects. Use when the user says "find an image", "search for a photo", "get a stock photo", "source images for my site", "I need a free image of", "find me a background image", "find open-use images", or asks to locate any visual asset for a web project.
---

# Image Search

Search for free, open-use images from multiple sources. Prioritize sources that require no API key, then fall back to key-authenticated APIs when keys are available.

## Source Priority

1. **OpenVerse** (no key required) — CC-licensed images from 700M+ works
2. **Wikimedia Commons** (no key required) — public domain and CC images
3. **Unsplash** (key required, env: `UNSPLASH_ACCESS_KEY`) — high quality photography
4. **Pexels** (key required, env: `PEXELS_API_KEY`) — curated stock photos and video
5. **Pixabay** (key required, env: `PIXABAY_API_KEY`) — photos, vectors, illustrations

## Workflow

### Step 1 — Gather requirements

Ask (or infer from context):
- **Topic/subject** — what should the image show?
- **Style** — photograph, illustration, vector, icon, texture, pattern?
- **Orientation** — landscape, portrait, square?
- **Dominant color** — optional, helps narrow results
- **License need** — commercial use? modification allowed?

### Step 2 — Search sources

Try sources in priority order. Use WebFetch to call APIs directly.

**OpenVerse (no key):**
```
GET https://api.openverse.org/v1/images/?q={query}&license_type=commercial&page_size=10
```
Add `&orientation=landscape|portrait|square` if specified.
Add `&filter_dead=true` to skip broken links.

**Wikimedia Commons (no key):**
```
GET https://commons.wikimedia.org/w/api.php?action=query&list=search&srsearch={query}&srnamespace=6&srlimit=10&format=json&origin=*
```
Then fetch file info for each result:
```
GET https://commons.wikimedia.org/w/api.php?action=query&titles=File:{filename}&prop=imageinfo&iiprop=url|extmetadata&format=json&origin=*
```

**Unsplash (key required):**
```
GET https://api.unsplash.com/search/photos?query={query}&per_page=10&orientation={orientation}&client_id={UNSPLASH_ACCESS_KEY}
```

**Pexels (key required):**
```
GET https://api.pexels.com/v1/search?query={query}&per_page=10&orientation={orientation}
Authorization: {PEXELS_API_KEY}
```

**Pixabay (key required):**
```
GET https://pixabay.com/api/?q={query}&image_type=photo&per_page=10&key={PIXABAY_API_KEY}
```

### Step 3 — Present results

Show 3–5 of the best matches. For each result, provide:

```
**[Descriptive title]**
Source: Unsplash / Pexels / OpenVerse / Wikimedia / Pixabay
Photographer/Author: [name if available]
License: [CC0 / CC BY / CC BY-SA / Unsplash License / Pexels License]
Preview URL: [direct image URL — thumbnail or full]
Page URL: [source page for attribution]

HTML embed:
<img src="[direct-url]" alt="[descriptive alt text]" loading="lazy">

Attribution (if required):
Photo by [Author] on [Source] — [page URL]
```

### Step 4 — Offer next steps

After presenting results, ask:
- "Want me to embed one of these in your project?"
- "Need a different style or subject?"
- "Want me to search for more options?"

If the user picks an image, insert the `<img>` tag at the appropriate location in the file and add attribution in a comment if the license requires it.

## License Rules

| License | Free to use | Commercial OK | Must attribute |
|---------|-------------|---------------|----------------|
| CC0 / Public Domain | Yes | Yes | No |
| Unsplash License | Yes | Yes | No (encouraged) |
| Pexels License | Yes | Yes | No (encouraged) |
| CC BY | Yes | Yes | Yes |
| CC BY-SA | Yes | Yes | Yes (share-alike) |
| CC BY-NC | Yes | No | Yes |

Never serve images with CC BY-NC for commercial projects without warning the user.

## Handling No API Keys

If the user hasn't configured API keys and OpenVerse/Wikimedia results are thin:
1. Suggest Unsplash/Pexels as excellent free options with easy key signup
2. Point them to `references/image-apis.md` for setup instructions
3. Offer to try a broader search query on the keyless sources

## Quality Checks

Before recommending an image:
- Confirm the URL is accessible (check HTTP status via WebFetch)
- Verify the license matches the project's needs
- Ensure the image is relevant — don't stretch to fill a quota
- Prefer high-resolution originals over compressed thumbnails when embedding
