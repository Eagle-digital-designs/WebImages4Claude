# Image API Reference

## OpenVerse (No Key Required)

**Base URL:** `https://api.openverse.org/v1/`

### Search Images
```
GET /images/?q={query}
```

| Parameter | Values | Notes |
|-----------|--------|-------|
| `q` | string | Search query |
| `license_type` | `commercial`, `modification` | Filter by allowed use |
| `license` | `cc0`, `pdm`, `by`, `by-sa`, `by-nc` | Specific license |
| `orientation` | `landscape`, `portrait`, `square` | |
| `size` | `small`, `medium`, `large` | |
| `image_type` | `photo`, `illustration`, `digitized_artwork` | |
| `filter_dead` | `true` | Skip broken image links |
| `page_size` | 1–500 | Results per page (default 20) |

### Response Fields
- `id` — unique identifier
- `title` — image title
- `url` — direct image URL
- `thumbnail` — thumbnail URL
- `foreign_landing_url` — source page for attribution
- `creator` — author name
- `creator_url` — author profile
- `license` — license code (e.g., `cc0`, `by`)
- `license_version` — e.g., `4.0`
- `attribution` — pre-formatted attribution string

**No authentication required.** Rate limit: 100 req/min unauthenticated.

---

## Wikimedia Commons (No Key Required)

**Base URL:** `https://commons.wikimedia.org/w/api.php`

### Search Files
```
GET ?action=query&list=search&srsearch={query}&srnamespace=6&srlimit=10&format=json&origin=*
```
`srnamespace=6` restricts to the File namespace.

### Get Image Info
```
GET ?action=query&titles=File:{filename}&prop=imageinfo&iiprop=url|extmetadata|mime&format=json&origin=*
```

Useful `extmetadata` fields: `LicenseShortName`, `AttributionRequired`, `Artist`, `ImageDescription`, `DateTimeOriginal`

### Direct File URL Pattern
`https://commons.wikimedia.org/wiki/Special:FilePath/{filename}`

**No authentication required.** Licensed under CC or public domain.

---

## Unsplash API (Key Required)

**Sign up:** https://unsplash.com/developers  
**Free tier:** 50 requests/hour  
**Env var:** `UNSPLASH_ACCESS_KEY`

### Search Photos
```
GET https://api.unsplash.com/search/photos
  ?query={query}
  &per_page=10
  &orientation=landscape|portrait|squarish
  &color=black_and_white|black|white|yellow|orange|red|purple|magenta|green|teal|blue
  &client_id={UNSPLASH_ACCESS_KEY}
```

### Response Fields
- `urls.full` — full resolution
- `urls.regular` — 1080px
- `urls.small` — 400px
- `urls.thumb` — 200px
- `links.html` — page URL for attribution
- `user.name` — photographer name
- `user.links.html` — photographer profile

**License:** Unsplash License — free for commercial use, no attribution required (but encouraged).  
**Attribution format:** `Photo by [name] on Unsplash`

---

## Pexels API (Key Required)

**Sign up:** https://www.pexels.com/api/  
**Free tier:** 200 requests/hour, 20,000/month  
**Env var:** `PEXELS_API_KEY`

### Search Photos
```
GET https://api.pexels.com/v1/search
  ?query={query}
  &per_page=10
  &orientation=landscape|portrait|square
  &size=large|medium|small
  &color={hex or color name}

Header: Authorization: {PEXELS_API_KEY}
```

### Response Fields
- `photos[].src.original` — original resolution
- `photos[].src.large` — W1880
- `photos[].src.medium` — W1280
- `photos[].src.small` — W640
- `photos[].url` — page URL for attribution
- `photos[].photographer` — photographer name
- `photos[].photographer_url` — photographer profile

**License:** Pexels License — free for commercial use, no attribution required (but encouraged).  
**Attribution format:** `Photo by [name] on Pexels`

---

## Pixabay API (Key Required)

**Sign up:** https://pixabay.com/api/docs/  
**Free tier:** 100 requests/minute  
**Env var:** `PIXABAY_API_KEY`

### Search Images
```
GET https://pixabay.com/api/
  ?q={query}
  &image_type=photo|illustration|vector|all
  &orientation=horizontal|vertical|all
  &category=fashion|nature|backgrounds|science|education|people|...
  &colors=grayscale|transparent|red|orange|yellow|green|turquoise|blue|lilac|pink|white|gray|black|brown
  &per_page=10
  &key={PIXABAY_API_KEY}
```

### Response Fields
- `hits[].webformatURL` — web-optimized image
- `hits[].largeImageURL` — large version
- `hits[].pageURL` — source page for attribution
- `hits[].user` — uploader name
- `hits[].tags` — comma-separated tags
- `hits[].imageWidth`, `hits[].imageHeight`

**License:** Pixabay License — free for commercial use, no attribution required.

---

## Setting Up API Keys in Claude Code

Add to your project's `.env` file (never commit this file):
```
UNSPLASH_ACCESS_KEY=your_key_here
PEXELS_API_KEY=your_key_here
PIXABAY_API_KEY=your_key_here
```

Or set them as environment variables in your shell before starting Claude Code:
```bash
export UNSPLASH_ACCESS_KEY=your_key_here
export PEXELS_API_KEY=your_key_here
export PIXABAY_API_KEY=your_key_here
```
