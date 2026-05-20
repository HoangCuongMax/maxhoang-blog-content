---
title: AIHero.dev notes - agents router
type: agents-router
status: active
published: true
project: aihero-dev-reference
tags:
  - aihero
  - course
  - publishing-rule
---

# AGENTS - aihero.dev

Use this folder for AIHero course references and course-related learning notes.

## Publishing Rule

All Markdown documents under `content/obsidian/aihero.dev` should be publishable by default:

- Set `published: true` in frontmatter for every course note.
- New course folders should include a `course.md` file with `published: true`.
- Do not add private planning, credentials, or internal-only notes here unless they are clearly marked `published: false` and intentionally excluded.

## Course Folder Pattern

Each course should live in its own slug folder:

```txt
course-slug/
  course.md
```

The `course.md` file should include at minimum:

- `title`
- `type: course-reference`
- `status`
- `published: true`
- `source: aihero.dev`
- useful tags
