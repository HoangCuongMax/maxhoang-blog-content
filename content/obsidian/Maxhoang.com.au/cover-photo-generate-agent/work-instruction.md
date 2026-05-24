---
title: Blog cover generator - work instruction
type: work-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - cover-generator
  - workflow
---

# Work instruction - Blog cover generator

## Workflow

1. Read `../AGENTS.md`.
2. Read this folder's `AGENTS.md`, `agent-instruction.md`, and `memory.md`.
3. Make content changes in `maxhoang-blog-content` and script/app changes in `MaxHoang_Notion`.
4. Verify generated covers and frontmatter before committing.
5. Log detailed work in this folder's `work-log.md`.
6. Add a short website-level entry to `../work-log.md` for meaningful changes.

## Commands

From `MaxHoang_Notion`, use the standard website checks:

```bash
npm run lint
npm run build
```

When the generator exists, use the project script documented in `blog-cover-generator-implementation-plan.md`.

```bash
npm run generate:covers
npm run generate:covers -- --force
```

Use `--force` when refreshing existing generated `/blog-covers/` assets into the current visual system.

## Verification

- Confirm posts with manual covers are unchanged.
- Confirm generated images are readable at 1200x630 and thumbnail sizes.
- Confirm updated Markdown frontmatter parses.
- Confirm website pages use the generated cover path.
