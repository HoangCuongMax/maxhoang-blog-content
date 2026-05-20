---
title: Code cleanup refactor - memory
type: project-memory
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - refactor
  - memory
---

# Memory - Code cleanup and refactor

App repo: `MaxHoang_Notion`

Current structure:

- `app/` - routes and API endpoints.
- `components/` - reusable and feature UI.
- `lib/` - content loading, metadata, helpers, chatbot, GitHub, mail.
- `scripts/` - local automation.

Known cleanup targets:

- Keep generated/OS files out of Git.
- Keep shared metadata and content helpers in `lib/`.
- Keep feature-specific UI in feature folders when a component family grows.
