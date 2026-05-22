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

## 2026-05-23

- Chatbot UI/personality: moved Sources/Continue/Feedback into Anna's footer action area, switched desktop open chat to a full-height left overlay sidebar, refreshed conversational copy and suggestions, and updated chatbot agent docs.

## 2026-05-22

- Chatbot agent docs: added Anna's next UI/personality improvement plan and strengthened the rule that future chatbot changes must update affected agent docs in the same work session.
- Chatbot conversation UX: changed Anna's answer display into staged conversational turns, moved feedback to a compact bottom panel after multiple answers, added recent session history for follow-up context, and added chat commands for theme switching and website page navigation.
- Chatbot admin: moved Push content, Update tokenization, and System theme controls into Anna behind an `I am Max` password-gated Admin Assistant flow.
- Chatbot UI: compacted answer cards with collapsible long answers, clearer Sources/Continue/Feedback sections, and fixed mobile fullscreen keyboard/zoom overflow behaviour.
- Chatbot UI: added an expand/collapse control for fullscreen mobile chat and a large desktop chat panel.
- Chatbot retrieval: added live published-content fallback search, deduped repeated source buttons, added answer follow-up suggestions, and exposed a manual `Update tokenization` sidebar action.
- Chatbot UI/indexing: added Anna's full ImageKit image to the chat background and made the chatbot indexer report tokenized published document counts, including Obsidian notes.
- Main agent docs: expanded root `AGENTS.md` with the website app code structure, content structure, and routing guidance for sub-agent work.
- Chatbot agent docs: expanded Anna's `AGENTS.md` with the website app code structure, content structure, and chatbot change checklist.
- Chatbot behaviour: updated Anna's live system prompt and small UI/API copy so the website reflects the new `chatbot-answer-rules.md` guidance.
- Published the Common NLP Questions and Answers note as a blog post and prepared it for chatbot content indexing through the website tokenization/indexing script.

## 2026-05-20

- Website fixes: redesigned event cards so text no longer overlays photos, filtered GitHub repositories containing `maxhoang`, and made the sidebar push-content action verify refreshed database counts.
- Website theme upgrade: added warm light/dark colour tokens, Geist typography, a sidebar theme toggle, and Anna chatbot styling tied to semantic tokens.
- App cleanup: added shared metadata helper, typecheck script, artifact ignore rules, removed two unused legacy components, and removed tracked `.DS_Store` files.
- Added UI/UX, code cleanup/refactor, blog/content management, SEO/metadata, performance, and accessibility sub-agents for broader website ownership.
- Added `side-bar-navigation-agent` for website sidebar/navigation ownership and reporting.
- Set every Markdown note under `Maxhoang.com.au` and its sub-agent folders to `published: false`.
- Created the website-level `Maxhoang.com.au` agent with root instruction, memory, workflow, and reporting log.
- Formalized `personal-chatbot-agent`, `cover-photo-generate-agent`, and `motion-effect-agent` as sub-agents that report to the website agent.
