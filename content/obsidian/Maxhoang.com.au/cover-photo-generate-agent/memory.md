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
- Planned generated covers: `MaxHoang_Notion/public/blog-covers`
- Planned generator script: `MaxHoang_Notion/scripts/generate-covers.mjs`

## Current plan

The current implementation plan is documented in `blog-cover-generator-implementation-plan.md`.

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
- Existing manual covers should remain unchanged.
