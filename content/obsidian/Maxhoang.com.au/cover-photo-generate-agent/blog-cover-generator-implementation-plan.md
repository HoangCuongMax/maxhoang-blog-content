---
title: Blog Cover Image Generator Implementation Plan
type: implementation-plan
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - cover-generator
---

# Blog Cover Image Generator Implementation Plan

## Summary

Implement and maintain a standalone cover generator in `MaxHoang_Notion` that creates missing 1200x630 blog cover images and links them from post frontmatter.

## Key Changes

- Dependencies in `MaxHoang_Notion`: `gray-matter`, `fast-glob`, `satori`, `sharp`, and `reading-time`.
- `generate:covers` npm script runs `node scripts/generate-covers.mjs`.
- Generator script: `MaxHoang_Notion/scripts/generate-covers.mjs`.
- Generate images into `MaxHoang_Notion/public/blog-covers/{slug}.png`.
- Update affected markdown posts with `coverImage: /blog-covers/{slug}.png`.
- Add `mediaAltText` for generated covers.

## Generator Behavior

- Scan local posts from `../maxhoang-blog-content/content/posts/**/*.md`.
- Generate a cover only when `coverImage`, `cover`, and `image` are missing, empty, set to `auto`, or contain a video URL rather than a real image cover.
- Treat existing `/blog-covers/` values as generator-owned assets that can be refreshed with `--force`.
- Skip posts with existing real image URLs or local image paths.
- Read `title`, `description` or `excerpt`, `date`, `tags`, `slug`, cover fields, and optional `coverTemplate`.
- Use the frontmatter slug, falling back to a title slug.
- Use one consistent `max-journal` visual system.
- Map legacy `clean-tech`, `dark-ai`, and `minimal-editorial` template names to `max-journal`.
- Choose deterministic accent colours from the slug, title, and tags.
- Do not overwrite existing generated PNGs unless run with `--force`.
- Skip posts with `published: false`.

## Site Integration

- Keep the existing blog UI structure.
- Use current `coverImage` parsing in `lib/vault.ts`.
- Update `app/blog/[slug]/page.tsx` metadata so generated covers are used for Open Graph and Twitter cards.

## Test Plan

- Run `npm run generate:covers`.
- Confirm PNGs exist in `MaxHoang_Notion/public/blog-covers`.
- Confirm missing-cover posts now contain `coverImage: /blog-covers/{slug}.png`.
- Confirm posts with existing manual covers are unchanged.
- Run `npm run lint`.
- Run `npm run build`.
- Start the dev server and verify homepage cards, blog detail covers, and Open Graph metadata.

## Assumptions

- Only blog posts are in scope for this first implementation.
- Generated covers are committed with the Next app under `public`.
- The generator is a local script, not a runtime API route.
