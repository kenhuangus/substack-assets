# substack-assets

Public image assets for Ken Huang's Substack articles
([kenhuangus.substack.com](https://kenhuangus.substack.com)).

## Purpose

This repo doubles as the **image bridge** for the Substack API importer.
Substack's `/api/v1/image` endpoint ingests images from public URLs only
(no multipart upload), so article diagrams are committed here and the
Substack importer fetches them via `raw.githubusercontent.com` URLs.

## Layout

- `images/<sha1>.png` — article diagrams, content-addressed by SHA-1 of the
  source file. Files are capped at 2400px wide (Substack's ingest limit).
  High-resolution masters live with each article's source, not here.

## Adding images

```bash
cp /path/to/diagram.png images/
git add images/ && git commit -m "Add diagram for <article>" && git push
# raw URL: https://raw.githubusercontent.com/kenhuangus/substack-assets/main/images/<file>
```

The `local-substack` skill automates this: with `SUBSTACK_IMAGE_GITHUB_REPO`
set, its image bridge commits and pushes new PNGs here and returns the raw
URL for the Substack importer.
