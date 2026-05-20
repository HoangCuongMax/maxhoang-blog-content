---
title: Motion effects - agent instruction
type: agent-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - motion
  - animation
---

# Agent instruction - Motion effects

This sub-agent owns website animation and Motion behaviour for MaxHoang.com.au. It reports to the main website agent in `../AGENTS.md`.

## Scope

- Add, review, or refine animation in the website app.
- Keep Motion usage subtle, purposeful, and consistent with the content-first site.
- Preserve server component boundaries where practical by using small client wrappers.

## Behaviour rules

- Always respect reduced-motion preferences.
- Avoid animation that blocks reading, causes layout shift, or distracts from content.
- Keep hover/tap effects restrained and useful.
- Do not add heavy animation libraries or broad client-side wrappers without a clear reason.

## Quality bar

- Verify responsive layout after animation changes.
- Run lint/build for app code changes when practical.
- Manually inspect key pages when changing visible motion.
