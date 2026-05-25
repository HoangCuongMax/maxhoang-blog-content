---
title: Blog content management - agent instruction
type: agent-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - blog
  - content
---

# Agent instruction - Blog/content management

Owns public content workflow, private Daily Journal workflow, Markdown frontmatter rules, and website content presentation.

## Scope

- Blog posts, awards, events, photos, short videos, Obsidian public notes, Daily Journal notes, and course/reference notes.
- Publishing rules, frontmatter consistency, content visibility, and content-driven routing.
- Obsidian Daily Notes template consistency for `content/Daily Journal`.

## Rules

- Never publish private notes, drafts, secrets, or internal planning material unintentionally.
- Daily Journal notes live in `content/Daily Journal`, use `publish: true`, and are always included by the website only behind Admin Assistant. Do not move them into public blog or public chatbot indexing.
- The Obsidian Daily Notes template is `content/Templates/Daily Journal Post.md`; keep it consistent with the website loader fields.
- Preserve existing content and slugs unless a task explicitly changes them.
- Coordinate with SEO and cover-generator agents for metadata and cover-image work.
