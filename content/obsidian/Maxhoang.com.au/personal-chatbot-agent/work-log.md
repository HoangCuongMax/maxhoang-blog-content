---
title: Anna chatbot — work log
type: work-log
status: active
published: false
project: personal-portfolio-chatbot
tags:
  - personal-chatbot
  - work-log
---

# Work log

Short dated entries. **Newest first.**

## 2026-05-22

- Added a chatbot expand/collapse control so Anna can open as a fullscreen chat app on mobile and a large near-fullscreen panel on desktop.
- Fixed chatbot retrieval UX by deduplicating repeated source buttons, adding follow-up suggestion chips under answers, adding a live published-content retriever for stale embedding coverage, and adding a sidebar `Update tokenization` action backed by `/api/chatbot-index`.
- Added Anna's full ImageKit image as the chatbot surface background and updated the chatbot indexer to report tokenized published document counts per content folder; embedding regeneration was blocked locally because `npm`/Node is unavailable in this shell.
- Expanded `AGENTS.md` with a website code structure map, content structure map, and chatbot change checklist so future Anna sessions know where to inspect app code.
- Wired `chatbot-answer-rules.md` into the live chatbot system prompt in `MaxHoang_Notion/lib/chatbot/chat-completion.ts`, refreshed fallback/greeting copy in `/api/chat`, and softened the UI intent acknowledgement.
- Added human conversation rules to `chatbot-answer-rules.md`, including acknowledgement, mixed initiative, clarification questions, side-question handling, and careful same-session memory.
- Refined `chatbot-answer-rules.md` with natural simple-English response style, example good/bad answer patterns, and safer general-topic fallback rules.
- Added `chatbot-answer-rules.md` with practical grounding, style, fallback, and QA rules for better Anna chatbot answers.

## 2026-05-20

- Updated Anna chatbot presentation to use the website theme tokens, including Anna purple accents, themed message bubbles, input controls, avatar frame, and light/dark readable surfaces without changing chatbot behavior.
- Moved Anna chatbot docs under `Maxhoang.com.au/personal-chatbot-agent` and updated the router to report to the website-level agent.
- Replaced loose planning set with **`agent-instruction.md`**, **`memory.md`**, **`work-instruction.md`**; slim **`AGENTS.md`** router; renamed log to **`work-log.md`**. Removed assignment-only and duplicate planning files from this folder.
- Prior session (Codex / app): RAG pipeline, `/api/chat`, JSON retriever, indexing script, Anna UI, direct greeting/contact answers, source buttons, Motion + reduced motion, `AGENTS.md` first version.
