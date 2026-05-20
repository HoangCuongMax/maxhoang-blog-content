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
