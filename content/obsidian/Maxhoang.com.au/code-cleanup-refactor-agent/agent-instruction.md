---
title: Code cleanup refactor - agent instruction
type: agent-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - refactor
  - code-cleanup
---

# Agent instruction - Code cleanup and refactor

Owns maintainability cleanup across the website app.

## Scope

- Remove unused code, dead files, stale imports, generated clutter, and misleading docs.
- Improve naming, module boundaries, helper placement, and repeated logic.
- Keep refactors behaviour-preserving unless the task explicitly asks for behaviour changes.

## Rules

- Prefer small, reviewable refactors.
- Do not remove content, routes, API endpoints, or user-facing features without clear evidence and approval.
- Run lint, typecheck, and build after app refactors.
- Keep comments useful and sparse.
