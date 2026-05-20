---
title: MaxHoang.com.au website - work instruction
type: work-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - workflow
---

# Work instruction - MaxHoang.com.au

Use this note when developing, debugging, shipping, reorganizing website notes, or coordinating sub-agents.

## 1. Where to work

- **Website code:** `MaxHoang_Notion`
- **Website content:** `maxhoang-blog-content/content`
- **Website agent docs:** `maxhoang-blog-content/content/obsidian/Maxhoang.com.au`
- **Focused sub-agent docs:** the relevant subfolder under `Maxhoang.com.au`

## 2. Normal commands

Run app commands from `MaxHoang_Notion`:

```bash
npm install
npm run dev
npm run lint
npm run build
```

Use feature-specific commands from sub-agent notes when relevant, such as chatbot indexing or cover generation.

## 3. Git workflow

| Change type | Repo to commit |
|---|---|
| Website app code, generated app assets, scripts | `MaxHoang_Notion` |
| Markdown content, planning notes, agent docs | `maxhoang-blog-content` |

If a task changes both repos, commit and push each repo separately with focused commit messages.

## 4. Sub-agent reporting

When work belongs to a sub-agent:

1. Read this root `AGENTS.md`.
2. Read the sub-agent's local `AGENTS.md`.
3. Do the work in the correct repo.
4. Update the sub-agent's `work-log.md` if one exists.
5. Add a short website-level entry to this folder's `work-log.md` if the work affects website behaviour, implementation, workflow, or agent structure.

## 5. Verification checklist

- [ ] Content links and frontmatter checked for content-only changes.
- [ ] `npm run lint` for app code changes when practical.
- [ ] `npm run build` for app behaviour, routing, or component changes when practical.
- [ ] Feature-specific checks from the relevant sub-agent completed.
- [ ] Work logs updated where needed.

## 6. Guardrails

- Do not commit `.env` files with real secrets.
- Avoid committing local editor state such as `.obsidian/workspace.json` unless explicitly requested.
- Do not overwrite generated or user-authored content unless the task calls for it.
- Keep root agent docs high-level; detailed feature rules belong in sub-agent folders.
