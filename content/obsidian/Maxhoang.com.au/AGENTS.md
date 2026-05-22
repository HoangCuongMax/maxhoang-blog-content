---
title: MaxHoang.com.au website - agents router
type: agents-router
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - website-agent
---

# AGENTS - MaxHoang.com.au website

**Start every session** about the Max Hoang Journal / MaxHoang.com.au website by reading these three notes **in order**:

1. **`agent-instruction.md`** - Website-wide product direction, behaviour, quality bar, and safety rules.
2. **`memory.md`** - Repos, paths, architecture, content model, and stable implementation facts.
3. **`work-instruction.md`** - Commands, Git workflow, verification, and how sub-agents report work.

## Website code structure to know

The runnable website app is the **MaxHoang_Notion** Next.js repo. The Markdown/content source is the **maxhoang-blog-content** repo. Use this map before choosing a sub-agent or editing code:

| Area | Path | What to check |
|---|---|---|
| App router | `MaxHoang_Notion/app/` | Pages, layouts, route groups, API routes, metadata, and global route behaviour. |
| Shared components | `MaxHoang_Notion/components/` | Reusable UI, page sections, chatbot components, sidebar, cards, controls, and visual patterns. |
| Chatbot UI | `MaxHoang_Notion/components/chatbot/` | Anna launcher, chat window, messages, input, avatar, source buttons, and chatbot interaction states. |
| Sidebar navigation | `MaxHoang_Notion/components/workspace-sidebar.tsx` and `MaxHoang_Notion/components/ui/sidebar.tsx` | Main navigation links, collapse/mobile behaviour, provider state, and sidebar accessibility. |
| Shared logic | `MaxHoang_Notion/lib/` | Content loaders, metadata helpers, GitHub/project utilities, chatbot helpers, and shared utilities. |
| Chatbot logic | `MaxHoang_Notion/lib/chatbot/` | RAG types, embedder, retriever contract, JSON retriever, and chat completion rules. |
| Metadata | `MaxHoang_Notion/lib/metadata.ts` | Shared website metadata, Open Graph/Twitter helpers, and route metadata patterns. |
| Scripts | `MaxHoang_Notion/scripts/` | Local automation such as chatbot indexing, cover generation, and content-related scripts. |
| Static assets | `MaxHoang_Notion/public/` | Images, generated assets, icons, and files served directly by the site. |
| Generated chatbot index | `MaxHoang_Notion/data/chatbot-embeddings.json` | Generated RAG embeddings consumed by the chatbot JSON retriever. |
| Global styling | `MaxHoang_Notion/app/globals.css` | Theme tokens, typography, layout primitives, chatbot/sidebar styling, and global CSS. |
| Package commands | `MaxHoang_Notion/package.json` | `dev`, `lint`, `build`, `typecheck`, indexing, and generation scripts. |

## Content structure to know

| Area | Path | What to check |
|---|---|---|
| Blog posts | `maxhoang-blog-content/content/posts/` | Public post Markdown, frontmatter, slugs, cover fields, tags, and publishing status. |
| Awards | `maxhoang-blog-content/content/awards/` | Award entries and recognition content used by the public site. |
| Events | `maxhoang-blog-content/content/events/` | Event entries, dates, descriptions, images, and publishing status. |
| Obsidian notes | `maxhoang-blog-content/content/obsidian/` | Internal notes, learning references, and agent docs; do not expose drafts/private notes. |
| Website agent docs | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/` | Website-wide agent router, instructions, memory, workflow, sub-agents, and work log. |

## Routing work to sub-agents

- Chatbot, RAG, persona, answer quality, and source UI: `personal-chatbot-agent/`.
- Public Markdown publishing, frontmatter, and content loaders: `blog-content-management-agent/`.
- Sidebar links, navigation, collapse/mobile behaviour, and sidebar accessibility: `side-bar-navigation-agent/`.
- Metadata, titles, descriptions, Open Graph, and previews: `seo-metadata-agent/`.
- Layout polish, responsive hierarchy, empty states, and visual quality: `ui-ux-improvement-agent/`.
- Keyboard access, labels, alt text, reduced motion, contrast, and semantics: `accessibility-review-agent/`.
- Motion/animation and reduced-motion behaviour: `motion-effect-agent/`.
- Bundle size, rendering, media, data fetching, and build-output performance: `performance-optimisation-agent/`.
- Maintainability, unused code, naming, and behaviour-preserving refactors: `code-cleanup-refactor-agent/`.
- Blog cover generation workflow, cover metadata, scripts, and generated images: `cover-photo-generate-agent/`.

## Sub-agents

Each subfolder under this folder is a focused sub-agent. Before working in a sub-agent folder, read this main website agent first, then read that sub-agent's local `AGENTS.md`.

| Sub-agent | Folder | Responsibility |
|---|---|---|
| Accessibility review | `accessibility-review-agent/` | Keyboard access, labels, media alt text, reduced motion, contrast, and semantic HTML. |
| Anna chatbot | `personal-chatbot-agent/` | Website chatbot, RAG, persona, chat UI, and chatbot docs. |
| Blog/content management | `blog-content-management-agent/` | Public Markdown workflow, publishing rules, frontmatter, and content loaders. |
| Code cleanup/refactor | `code-cleanup-refactor-agent/` | Maintainability, unused-code cleanup, naming, helper placement, and behaviour-preserving refactors. |
| Cover photo generator | `cover-photo-generate-agent/` | Blog cover generation workflow, cover scripts, metadata, and image output rules. |
| Motion effects | `motion-effect-agent/` | Website animation, Motion usage, reduced-motion behaviour, and animation work notes. |
| Performance optimisation | `performance-optimisation-agent/` | Data fetching, bundle size, rendering, media, and build-output performance review. |
| SEO and metadata | `seo-metadata-agent/` | Page metadata, Open Graph/Twitter cards, titles, descriptions, and preview images. |
| Sidebar navigation | `side-bar-navigation-agent/` | Website sidebar, navigation links, collapse/mobile behaviour, actions, and sidebar accessibility. |
| UI/UX improvement | `ui-ux-improvement-agent/` | Layout consistency, responsive polish, page hierarchy, empty states, and visual quality. |

**Reporting rule:** sub-agents log detailed work in their own `work-log.md` when present, then add or update a short website-level entry in this folder's **`work-log.md`** when the work changes website behaviour, implementation, or agent structure.

This folder lives under the content vault: `maxhoang-blog-content/content/obsidian/Maxhoang.com.au`. The runnable website app is **not** here; it is in the **MaxHoang_Notion** Next.js repo (see `memory.md`).
