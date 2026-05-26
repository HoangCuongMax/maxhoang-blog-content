---
title: Admin Assistant - work instruction
type: work-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - admin-assistant
  - workflow
---

# Work Instruction - Admin Assistant

## Start Here

1. Read `../AGENTS.md`.
2. Read this folder's `AGENTS.md`, `agent-instruction.md`, and `memory.md`.
3. Inspect the current app code in `MaxHoang_Notion`.

## Implementation Checklist

- Find all Admin Assistant controls in `components/chatbot/ChatbotWindow.tsx`.
- Remove duplicate controls and rename unclear actions.
- Separate Admin Assistant layout from Anna's public chat layout.
- Add Daily Journal post creation UI behind admin login.
- Add or update API routes needed to create Daily Journal Markdown files.
- Revalidate `/daily-journal` after creating a post.
- Keep `.env` and secrets out of commits.

## Verification

Run from `MaxHoang_Notion`:

```bash
npm.cmd run typecheck
npm.cmd run lint
npm.cmd run build
```

Manually verify:

- locked users cannot create Daily Journal posts
- unlocked admin can see "Create new post"
- post creation writes the expected Markdown/frontmatter
- Daily Journal list refreshes after creation
- Admin Assistant UI is visually distinct from Anna
- duplicate admin controls are gone

## Logging

After meaningful Admin Assistant work:

1. Add a dated entry to this folder's `work-log.md`.
2. Add a short parent entry to `../work-log.md` when website behaviour, implementation, or agent structure changes.
