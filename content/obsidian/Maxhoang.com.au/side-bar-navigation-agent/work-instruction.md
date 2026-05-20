---
title: Sidebar navigation - work instruction
type: work-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - sidebar
  - navigation
  - workflow
---

# Work instruction - Sidebar navigation

## Workflow

1. Read `../AGENTS.md`.
2. Read this folder's `AGENTS.md`, `agent-instruction.md`, and `memory.md`.
3. Make app changes in `MaxHoang_Notion`.
4. Keep navigation data changes in `lib/site-config.ts` unless the existing architecture changes.
5. Keep sidebar rendering changes in `components/workspace-sidebar.tsx`.
6. Change `components/ui/sidebar.tsx` only when primitive behaviour needs to change.
7. Log detailed work in this folder's `work-log.md`.
8. Add a short website-level entry to `../work-log.md` for meaningful changes.

## Commands

From `MaxHoang_Notion`:

```bash
npm run lint
npm run build
```

Use a dev server and browser check when visual layout, collapse behaviour, mobile sheet behaviour, or active route logic changes.

## Verification

- Check desktop expanded sidebar.
- Check desktop collapsed sidebar and tooltips.
- Check mobile sheet open/close.
- Check `Cmd/Ctrl+B` sidebar toggle.
- Check active states on top-level and nested routes.
- Check `Push content` idle, loading, success, and error handling when that action changes.
- Check text truncation in the header and footer.
