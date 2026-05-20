---
title: MaxHoang.com.au website - work log
type: work-log
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - work-log
---

# Work log

Short dated entries. **Newest first.**

## 2026-05-20

- Website fixes: redesigned event cards so text no longer overlays photos, filtered GitHub repositories containing `maxhoang`, and made the sidebar push-content action verify refreshed database counts.
- Website theme upgrade: added warm light/dark colour tokens, Geist typography, a sidebar theme toggle, and Anna chatbot styling tied to semantic tokens.
- App cleanup: added shared metadata helper, typecheck script, artifact ignore rules, removed two unused legacy components, and removed tracked `.DS_Store` files.
- Added UI/UX, code cleanup/refactor, blog/content management, SEO/metadata, performance, and accessibility sub-agents for broader website ownership.
- Added `side-bar-navigation-agent` for website sidebar/navigation ownership and reporting.
- Set every Markdown note under `Maxhoang.com.au` and its sub-agent folders to `published: false`.
- Created the website-level `Maxhoang.com.au` agent with root instruction, memory, workflow, and reporting log.
- Formalized `personal-chatbot-agent`, `cover-photo-generate-agent`, and `motion-effect-agent` as sub-agents that report to the website agent.
