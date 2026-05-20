---
title: Code cleanup refactor - work instruction
type: work-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - refactor
  - workflow
---

# Work instruction - Code cleanup and refactor

From `MaxHoang_Notion`, run:

```bash
npm run lint
npm run typecheck
npm run build
```

Before removing files, search for references with `rg`. Log meaningful cleanup in this folder and the parent log.
