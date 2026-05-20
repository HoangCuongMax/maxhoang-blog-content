# Blog Cover Image Generator Implementation Plan

## Summary

Create a living markdown plan in this folder, then implement a standalone cover generator in `MaxHoang_Notion` that creates missing 1200x630 blog cover images and links them from post frontmatter.

## Key Changes

- Add dependencies to `MaxHoang_Notion`: `gray-matter`, `fast-glob`, `satori`, `sharp`, and `reading-time`.
- Add `generate:covers` as an npm script that runs `node scripts/generate-covers.mjs`.
- Create `MaxHoang_Notion/scripts/generate-covers.mjs`.
- Generate images into `MaxHoang_Notion/public/blog-covers/{slug}.png`.
- Update affected markdown posts with `coverImage: /blog-covers/{slug}.png`.

## Generator Behavior

- Scan local posts from `../maxhoang-blog-content/content/posts/**/*.md`.
- Generate a cover only when `coverImage`, `cover`, and `image` are missing, empty, or set to `auto`.
- Skip posts with existing real cover URLs, YouTube cover values, or local image paths.
- Read `title`, `description` or `excerpt`, `date`, `tags`, `slug`, cover fields, and optional `coverTemplate`.
- Use the frontmatter slug, falling back to a title slug.
- Support `clean-tech`, `dark-ai`, and `minimal-editorial` templates.
- Choose a missing `coverTemplate` deterministically from the slug.
- Do not overwrite existing generated PNGs unless run with `--force`.

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
