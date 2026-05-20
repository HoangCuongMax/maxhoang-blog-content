---
title: Motion effects - work instruction
type: work-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - motion
  - workflow
---

# Work instruction - Motion effects

## Workflow

1. Read `../AGENTS.md`.
2. Read this folder's `AGENTS.md`, `agent-instruction.md`, and `memory.md`.
3. Make app changes in `MaxHoang_Notion`.
4. Verify animation behaviour, layout, and reduced-motion handling.
5. Log detailed work in this folder's `work-log.md`.
6. Add a short website-level entry to `../work-log.md` for meaningful changes.

## Commands

From `MaxHoang_Notion`:

```bash
npm run lint
npm run build
```

Use the dev server and browser checks when visual behaviour changes.

## Verification

- Confirm no major layout shift is introduced.
- Confirm reduced-motion users avoid movement-heavy transitions.
- Confirm desktop and mobile layouts remain readable.
- Confirm build output is acceptable.
