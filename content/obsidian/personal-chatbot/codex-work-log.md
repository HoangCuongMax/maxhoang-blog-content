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
