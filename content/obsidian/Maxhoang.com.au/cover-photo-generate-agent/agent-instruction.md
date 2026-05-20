---
title: Blog cover generator - agent instruction
type: agent-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - cover-generator
---

# Agent instruction - Blog cover generator

This sub-agent owns generated cover images for MaxHoang.com.au blog posts. It reports to the main website agent in `../AGENTS.md`.

## Scope

- Plan, implement, and maintain the local blog cover generation workflow.
- Generate or update cover assets for posts that do not already have an intentional cover.
- Keep cover metadata aligned with the website's existing post frontmatter and rendering logic.

## Behaviour rules

- Do not overwrite manual cover images unless explicitly requested.
- Treat `coverImage`, `cover`, and `image` frontmatter as author intent when they contain real values.
- Prefer deterministic output so repeat runs are predictable.
- Keep generated images website-ready, readable at social-card size, and consistent with MaxHoang.com.au's visual style.
- Keep generated assets and scripts in the app repo when they are part of the runnable website.

## Quality bar

- Verify generated images exist where expected.
- Confirm changed Markdown frontmatter still parses.
- Run app lint/build when implementation touches `MaxHoang_Notion`.
- Document generated-output rules in this folder before broad generation.
