# Media Management

Elementeer gives AI agents full control over the WordPress media library — upload images, sideload stock photos, manage metadata, audit unused files, and (on Advanced tier) generate images with AI.

## Uploading Media

Upload images and files directly from your agent:

```
Upload this image to the media library: https://example.com/hero-banner.jpg
```

The agent calls `elementeer_upload_media` with the file URL. Supported input types:

- **URL** — the agent downloads the file and uploads it
- **Base64** — inline file data (for generated or clipboard content)
- **File path** — local filesystem path (CLI mode only)

```json
{
  "file": "https://example.com/hero-banner.jpg",
  "filename": "hero-banner.jpg",
  "title": "Homepage Hero Banner",
  "alt": "Team collaborating in modern office",
  "caption": "Our team at work"
}
```

!!! info "Upload destinations"
    Uploaded files go to the standard WordPress media library. Elementeer uses
    WordPress's built-in media handling — images get thumbnails generated at all
    registered sizes.

## Stock Image Sideload

Elementeer integrates with Openverse to find and import Creative Commons-licensed stock photography:

```
Find a stock photo of a modern office workspace and add it to the media library.
```

The agent:

1. Calls `elementeer_search_stock_images` with the search query
2. Lists matching images with titles, authors, and licenses
3. Calls `elementeer_sideload_image` to download and import the selected image
4. Automatically generates CC attribution in the image caption

```json
{
  "query": "modern office workspace",
  "license_type": "commercial"
}
```

Stock image sources include Openverse, Unsplash, Pexels, and Pixabay. Only images with licenses permitting commercial use and modification are returned by default.

!!! tip "Auto-attribution"
    Sideloaded stock images automatically include proper Creative Commons attribution
    in the caption field. You don't need to manage attribution manually.

## Image Metadata

Manage alt text, titles, and captions at scale:

```
Add descriptive alt text to all images on the homepage that are missing it.
```

The agent:

1. Calls `elementeer_list_media` to find images
2. Identifies images missing alt text
3. Updates each with `elementeer_update_media`

### Batch Metadata Updates

Fix missing metadata across up to 50 images at once:

```
Update alt text for these images: image-1.jpg = "Happy customer testimonial", 
image-2.jpg = "Software dashboard screenshot", image-3.jpg = "Team photo 2026"
```

The agent uses `elementeer_update_media_batch` for bulk updates.

## Media Audit

Find unused and unoptimized media:

```
Audit the media library for unused files and images missing alt text.
```

The audit reports:

- **Orphaned media:** Files not attached to any post or page
- **Unused in Elementor:** Media in the library but not referenced in any Elementor template or page
- **Missing alt text:** Images without accessibility descriptions
- **Oversized files:** Images exceeding recommended dimensions for web use
- **Format recommendations:** Suggestions to convert PNG to WebP, optimize JPEGs

## AI Image Generation (Advanced Tier)

On the Advanced tier, Elementeer integrates with AI image generation:

```
Generate a hero background image: abstract geometric pattern in brand colors, 1920x1080.
```

The agent calls `elementeer_generate_image` with a prompt and dimensions:

```json
{
  "prompt": "Abstract geometric pattern in purple and indigo, clean modern design, suitable for hero background",
  "width": 1920,
  "height": 1080,
  "style": "abstract-geometric"
}
```

Generated images are automatically:
1. Added to the WordPress media library
2. Thumbnails generated at all registered sizes
3. Available for use in Elementor templates and pages

## Media Library Organization

Elementeer can organize media by moving files between months, updating attachment metadata, and managing image taxonomies if you're using a media category plugin.
