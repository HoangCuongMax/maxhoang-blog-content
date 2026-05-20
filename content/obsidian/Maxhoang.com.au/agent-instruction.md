---
title: MaxHoang.com.au website - agent instruction
type: agent-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - website-agent
---

# Agent instruction - MaxHoang.com.au

Use this note when shaping website-wide product behaviour, content architecture, UI direction, technical implementation, or sub-agent coordination. For repos, paths, and file names, use **`memory.md`**. For commands and reporting, use **`work-instruction.md`**.

## Role and positioning

- **Website:** Max Hoang Journal / `https://maxhoang.com.au`
- **Role:** A public portfolio, blog, and learning archive for Max Hoang.
- **Audience:** visitors, students, employers, recruiters, collaborators, and readers exploring Max's work.

One-line positioning:

> MaxHoang.com.au presents Max's public writing, projects, events, awards, and learning notes through a fast, polished, content-first website.

## Website-wide principles

- Keep public content grounded in the Markdown content vault and the live website publishing rules.
- Prefer clear, useful pages over decorative or marketing-heavy layouts.
- Keep the website fast, accessible, and readable on mobile and desktop.
- Preserve existing design language unless a task explicitly changes it.
- Keep implementation changes close to the relevant feature area.
- Do not expose private notes, drafts, secrets, API keys, or unpublished content.

## Sub-agent coordination

- The root website agent is the main coordinator.
- Sub-agents own focused areas but must align with the website-wide rules in this note.
- A sub-agent should not silently change another sub-agent's scope. If work crosses areas, update both relevant local logs and the website-level `work-log.md`.
- Chatbot work reports through `personal-chatbot-agent/`.
- Code cleanup and maintainability work reports through `code-cleanup-refactor-agent/`.
- Blog/content workflow work reports through `blog-content-management-agent/`.
- Cover-generation work reports through `cover-photo-generate-agent/`.
- Motion and animation work reports through `motion-effect-agent/`.
- SEO and metadata work reports through `seo-metadata-agent/`.
- Performance work reports through `performance-optimisation-agent/`.
- Accessibility work reports through `accessibility-review-agent/`.
- Sidebar and navigation work reports through `side-bar-navigation-agent/`.
- UI/UX improvement work reports through `ui-ux-improvement-agent/`.

## Quality bar

- Verify code changes with the app's normal checks where practical: lint, build, and focused manual checks.
- For content-only changes, check Markdown paths, frontmatter, links, and publishing status.
- For UI changes, respect responsive layout, contrast, keyboard accessibility, and reduced-motion preferences.
- For automation scripts, keep outputs deterministic where practical and avoid overwriting human-authored content unless explicitly requested.

## Safety and publishing scope

- Website-facing features must not publish private content or local-only planning material.
- Internal agent notes should usually use `published: false`.
- Never commit real secrets.
- Avoid broad rewrites unless the task explicitly requires a website-wide reorganization.
