---
title: Blog content management - memory
type: project-memory
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - blog
  - content
  - memory
---

# Memory - Blog/content management

Content repo: `maxhoang-blog-content`

Public content areas:

- `content/posts`
- `content/awards`
- `content/events`
- `content/photos`
- `content/short-videos`
- `content/obsidian`

Private admin content areas:

- `content/Daily Journal` - Obsidian Daily Notes folder. The website includes these notes automatically and locks them behind Admin Assistant.
- `content/Templates` - Obsidian templates. `Daily Journal Post.md` is the configured Daily Notes template.

App loaders live in `MaxHoang_Notion/lib/vault.ts` and `MaxHoang_Notion/lib/content.ts`.
