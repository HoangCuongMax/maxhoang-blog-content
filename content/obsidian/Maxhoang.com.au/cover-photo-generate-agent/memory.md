---
title: Blog cover generator - memory
type: project-memory
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - cover-generator
  - memory
---

# Memory - Blog cover generator

## Parent

- Main website agent: `../AGENTS.md`

## Stable paths

- Website app: `/Users/maxhoang/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/MaxHoang_Notion`
- Content vault: `/Users/maxhoang/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/maxhoang-blog-content`
- Cover agent folder: `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/cover-photo-generate-agent`
- Blog posts: `maxhoang-blog-content/content/posts`
- Generated covers: `MaxHoang_Notion/public/blog-covers`
- Generator script: `MaxHoang_Notion/scripts/generate-covers.mjs`

## Current implementation

The implementation is documented in `blog-cover-generator-implementation-plan.md`.

Expected flow:

```txt
Blog Markdown without cover
  -> generate cover PNG
  -> write /blog-covers/{slug}.png
  -> update post frontmatter
  -> website cards and metadata use generated cover
```

## Known assumptions

- First implementation focuses on blog posts.
- Generated covers are local static assets committed in the app repo.
- Existing manual image covers should remain unchanged.
- YouTube/Vimeo links in `coverImage`, `cover`, or `image` are treated as non-image values, so the generator can replace them with real static PNG covers while the post keeps its `videoUrl`.
- Existing `/blog-covers/` frontmatter values are generator-owned and can be refreshed with `npm run generate:covers -- --force`.
- Covers use a consistent Max Hoang Journal layout with deterministic accent colours based on the post slug, title, and tags.
