---
title: MaxHoang.com.au website - memory
type: project-memory
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - memory
---

# Memory - MaxHoang.com.au website

Use this note for stable facts: repos, paths, architecture, content model, and sub-agent map. Update it only when the system, locations, or responsibilities actually change.

## Repositories

| Role | Repository |
|---|---|
| Website / Next.js app | `https://github.com/HoangCuongMax/MaxHoang_Notion` |
| Content database / Obsidian vault | `https://github.com/HoangCuongMax/maxhoang-blog-content` |

## Local paths

- **Workspace root:** `/Users/maxhoang/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog`
- **Website app:** `/Users/maxhoang/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/MaxHoang_Notion`
- **Content vault:** `/Users/maxhoang/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/maxhoang-blog-content`
- **Website agent folder:** `maxhoang-blog-content/content/obsidian/Maxhoang.com.au`

## High-level architecture

```txt
Markdown content vault
  -> MaxHoang_Notion data/content loaders and scripts
  -> Next.js app routes and components
  -> maxhoang.com.au public website
```

Feature-specific pipelines are documented in sub-agent folders.

## Main sub-agents

| Area | Folder | Notes |
|---|---|---|
| Accessibility review | `accessibility-review-agent/` | Keyboard, labels, media alt text, reduced motion, contrast, and semantic HTML. |
| Blog/content management | `blog-content-management-agent/` | Public content workflow, Markdown frontmatter, publishing rules, and content loaders. |
| Code cleanup/refactor | `code-cleanup-refactor-agent/` | Maintainability, dead-code cleanup, naming, helper placement, and reviewable refactors. |
| Personal chatbot / Anna | `personal-chatbot-agent/` | RAG chatbot, persona, UI, API, embeddings, and chatbot-specific workflow. |
| Blog cover generator | `cover-photo-generate-agent/` | Generated blog covers, cover metadata rules, image script planning. |
| Motion effects | `motion-effect-agent/` | Website Motion animation work and reduced-motion expectations. |
| Performance optimisation | `performance-optimisation-agent/` | Data fetching, bundle size, rendering, media, and build output. |
| SEO and metadata | `seo-metadata-agent/` | Route metadata, Open Graph/Twitter previews, titles, and descriptions. |
| Sidebar navigation | `side-bar-navigation-agent/` | Sidebar component, navigation data, collapse/mobile behaviour, and sidebar actions. |
| UI/UX improvement | `ui-ux-improvement-agent/` | Layout, responsive polish, visual hierarchy, and empty states. |

## Website app areas

Common app areas in `MaxHoang_Notion`:

- `app/` - Next.js App Router pages and API routes.
- `components/` - shared UI and feature components.
- `components/chatbot/` - Anna chatbot UI.
- `components/workspace-sidebar.tsx` - website sidebar navigation.
- `components/ui/sidebar.tsx` - sidebar primitive/provider.
- `lib/` - content loading, chatbot helpers, and shared utilities.
- `lib/metadata.ts` - shared website metadata helpers.
- `scripts/` - local automation such as indexing or generation scripts.
- `public/` - static assets served by the site.

## Content areas

Common content areas in `maxhoang-blog-content/content`:

- `posts/` - blog posts.
- `awards/` - awards and recognition.
- `events/` - event entries.
- `obsidian/` - notes, internal planning, learning references, and agent folders.

Publishing depends on the site's frontmatter and loader rules. Internal agent notes should stay unpublished unless intentionally turned into public content.

## Changelog

- **2026-05-20:** Introduced website-level agent folder for MaxHoang.com.au and formalized sub-agent reporting.
