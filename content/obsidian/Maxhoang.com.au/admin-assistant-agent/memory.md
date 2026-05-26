---
title: Admin Assistant - memory
type: project-memory
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - admin-assistant
  - memory
---

# Memory - Admin Assistant

Use this note for stable facts about the Admin Assistant system.

## Repositories

| Role | Repository |
|---|---|
| Website app | `MaxHoang_Notion` |
| Content vault | `maxhoang-blog-content` |

## Important App Areas

| Area | Path |
|---|---|
| Chatbot/Admin UI shell | `MaxHoang_Notion/components/chatbot/ChatbotWindow.tsx` |
| Chatbot widget | `MaxHoang_Notion/components/chatbot/ChatbotWidget.tsx` |
| Admin auth routes | `MaxHoang_Notion/app/api/admin/*` |
| Daily Journal create route | `MaxHoang_Notion/app/api/daily-journal/route.ts` |
| Content refresh route | `MaxHoang_Notion/app/api/push-content/route.ts` |
| Chatbot index route | `MaxHoang_Notion/app/api/chatbot-index/route.ts` |
| Daily Journal pages | `MaxHoang_Notion/app/daily-journal/` |
| Daily Journal admin form | `MaxHoang_Notion/components/daily-journal-admin-tools.tsx` |
| Content loaders | `MaxHoang_Notion/lib/content.ts`, `MaxHoang_Notion/lib/vault.ts` |
| TinaCMS schema | `MaxHoang_Notion/tina/config.ts` |
| TinaCMS static admin | `MaxHoang_Notion/public/admin/index.html` |

## Important Content Areas

| Area | Path |
|---|---|
| Daily Journal entries | `maxhoang-blog-content/content/Daily Journal/` |
| Daily Journal template | `maxhoang-blog-content/content/Templates/Daily Journal Post.md` |
| Admin Assistant docs | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/admin-assistant-agent/` |
| Chatbot FAQs | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/faq/` |
| Project knowledge | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/project-knowledge/` |
| Tina separate repo marker | `maxhoang-blog-content/tina/` |

## Current Problem

Admin Assistant previously appeared too visually close to Anna's chat UI and had duplicate controls, including overlapping content refresh, push, tokenization, and chatbot index actions.

## Target State

Admin Assistant should be a distinct admin console with grouped actions and forms.

Daily Journal should support direct post creation after admin login, both from the Daily Journal page and from Admin Assistant.

## Implemented State

- `ChatbotWindow.tsx` now renders Admin Assistant as a separate private console without the normal Anna chat input.
- Admin controls are grouped into Daily Journal, Content, Chatbot Knowledge, and System sections.
- The old admin action panel inside `ChatMessage.tsx` was removed to avoid duplicated controls.
- `POST /api/daily-journal` creates Daily Journal Markdown posts after admin authentication.
- The Daily Journal page shows a "New Daily Journal Post" form after admin login.
- The create route writes to GitHub when `OBSIDIAN_VAULT_GITHUB_TOKEN` or `GITHUB_TOKEN` exists, otherwise it falls back to the local sibling `maxhoang-blog-content` repo.
- TinaCMS is installed in `MaxHoang_Notion` and configured as a browser Content Studio for the separate `maxhoang-blog-content` repo.
- The Admin Assistant private console includes an "Open TinaCMS Content Studio" action that opens `/admin/index.html`.
- TinaCMS collections cover Daily Journal, blog posts, presentation slides, Anna personality/rules, Admin Assistant docs, FAQs, and project knowledge.
- Local builds use `tinacms build --local --skip-cloud-checks --skip-indexing` through Node with a larger heap because the content repo is large.
