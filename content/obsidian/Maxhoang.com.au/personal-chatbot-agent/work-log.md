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

## 2026-05-23

- Added minimized quick-chat UX: pencil toggles an inline input under the intro bubble, mini answers stay short/direct through `/api/chat` `mode: "mini"`, and full chat remains available for sources/details.
- Added Anna's first-open welcome flow plan to implementation: optional visitor name, optional newsletter signup, hidden input until start/skip, and anti-repetition/direct-answer conversation rules for greetings, identity, and help questions.
- Moved Anna's desktop overlay placement to the right edge while keeping the full-height sidebar behaviour, and updated the agent docs to match.
- Implemented markdown-brain v1: created approved root `markdown-brain/` memory files, added runtime personality-memory loading, updated the indexer for `memoryLayer` chunks, filtered factual sources away from personality memory, and kept learning human-approved.
- Added `markdown-brain-structure.md` to the Anna brain architecture plan with the proposed content/personality/memory/training folder structure, chatbot retrieval flow, and human-reviewed learning loop where only Max approves memory updates.
- Created `anna-brain-architecture/` with Anna's digital personality system plan, core personality bible, personality notes, conversation dictionary, dialogue examples, mood states, and implementation roadmap; linked it from `AGENTS.md` and `memory.md`.
- Implemented the Anna UI/personality plan: moved Sources/Continue/Feedback into a compact footer action area, made desktop chat open as a full-height right overlay sidebar, refreshed welcome/status/suggestion copy, strengthened the system prompt, and synced affected chatbot agent docs.

## 2026-05-22

- Updated Anna's `AGENTS.md` with the next UI/personality improvement plan and a stronger documentation sync rule requiring affected chatbot agent files to be updated whenever chatbot behaviour, UI, workflow, or implementation changes.
- Made Anna's answer flow more conversational by splitting API responses into staged chat turns: acknowledgement, answer, source summary, and follow-up suggestions; moved answer feedback to a compact bottom panel that appears after multiple saved answers; added chat commands for theme switching/page navigation and passed recent session history into answer generation for follow-up context.
- Moved admin actions from the public sidebar into Anna's chat behind an `I am Max` admin flow with password prompt, masked password transcript, in-chat Admin Assistant panel, and password-protected admin action endpoints.
- Improved Anna answer display and mobile fullscreen input behaviour: long answers collapse behind `Show more`, answer sections are labelled, source/suggestion buttons are visually distinct, and the expanded mobile chat locks horizontal overflow and avoids iOS input zoom.
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
