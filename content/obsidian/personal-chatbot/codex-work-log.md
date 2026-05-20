---
title: Codex Work Log
type: work-log
status: active
project: personal-portfolio-chatbot
tags:
  - codex
  - work-log
  - personal-chatbot
---

# Codex Work Log

This note records changes made by Codex in the personal chatbot project folder.

Whenever Codex creates, edits, fixes, or reorganises files for this project, the update should be recorded here.

## Log

### 2026-05-20

- Created this work log file so future Codex changes can be tracked in one place.
- Previous files created in this folder during this session:
  - [[expert-chatbot-presentation-task-division]]
  - [[expert-chatbot-5-minute-slide-content]]
- Implemented the planned Version 2 chatbot foundation in the `MaxHoang_Notion` Next.js app:
  - Added a Markdown-to-OpenAI-embeddings indexing script.
  - Added `data/chatbot-embeddings.json` as the local semantic search index target.
  - Added server-side chatbot types, embedder, JSON semantic retriever, and `/api/chat` route.
  - Connected the existing chatbot UI to `/api/chat` instead of the previous fake demo response.
  - Added Vercel/local environment variable notes for `OPENAI_API_KEY` and `OPENAI_EMBEDDING_MODEL`.
  - Kept the indexer aligned with website publishing rules so draft/private Markdown notes are not embedded.
- Created [[version-2-chatbot-implementation-plan]] to document the Version 2 implementation, current manual embedding workflow, and future automation options.
- Generated the local chatbot embedding index with the temporary OpenAI key provided in chat:
  - `MaxHoang_Notion/data/chatbot-embeddings.json`
  - 18 chunks embedded.
  - The key was not written into project files.
- Resolved merge conflict markers in:
  - [[Expert Chatbot Assignment Requirements]]
  - [[Personal Portfolio Website Assistant Chatbot Brief]]
- Planned and implemented a low-cost answer-generation improvement for the chatbot:
  - Added direct no-model answers for greetings and contact questions.
  - Added a small OpenAI chat completion layer after semantic retrieval.
  - Limited context to 3 retrieved chunks and capped output tokens.
  - Added `OPENAI_CHAT_MODEL` and `OPENAI_CHAT_MAX_OUTPUT_TOKENS` environment variable examples.
- Improved chatbot answer presentation:
  - Assistant messages now render paragraphs instead of one raw text block.
  - Markdown/plain URLs are converted into clickable links.
  - Retrieved sources are shown as compact source buttons under the answer.
  - The chat prompt now avoids raw URLs and separate source text because the UI handles links.
- Added an animated pre-open introduction bubble for the chatbot:
  - Introduces the assistant as Ana before the chat window opens.
  - Uses a lightweight typewriter animation.
  - Keeps the opened chatbot welcome/header consistent with the Ana assistant persona.
- Fixed chatbot message/input overlap:
  - Changed the chat window to a proper flex layout with fixed header/footer and a scrollable message area.
  - Removed fragile fixed scroll-height calculations.
  - Added bottom padding inside the message list so long answers do not hide behind the input box.
