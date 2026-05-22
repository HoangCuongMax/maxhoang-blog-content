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
