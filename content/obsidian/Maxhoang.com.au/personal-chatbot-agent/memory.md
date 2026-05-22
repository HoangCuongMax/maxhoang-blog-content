---
title: Anna chatbot — memory
type: project-memory
status: active
published: false
project: personal-portfolio-chatbot
tags:
  - personal-chatbot
  - memory
---

# Memory — Anna chatbot (stable facts)

Use this note for **repos**, **paths**, **pipeline**, **file map**, and **architecture decisions**. It should change only when the system or locations actually change.

## Repositories (canonical)

| Role | Repository |
|------|-------------|
| **Website / Next.js app** (UI, `/api/chat`, indexer script, `data/chatbot-embeddings.json`) | `https://github.com/HoangCuongMax/MaxHoang_Notion` |
| **Content database** (Markdown under `content/`) | `https://github.com/HoangCuongMax/maxhoang-blog-content` |

GitHub web: [MaxHoang_Notion](https://github.com/HoangCuongMax/MaxHoang_Notion) · [maxhoang-blog-content](https://github.com/HoangCuongMax/maxhoang-blog-content)

## Local paths (this machine)

Adjust if your clone location differs.

- **App:** `/Users/maxhoang/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/MaxHoang_Notion`
- **Content vault:** `/Users/maxhoang/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/maxhoang-blog-content`
- **Website agent folder:** `maxhoang-blog-content/content/obsidian/Maxhoang.com.au`
- **This sub-agent folder:** `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/personal-chatbot-agent`

## Parent agent

- Main website agent: `../AGENTS.md`

## Runtime pipeline (current)

```txt
Published Markdown (maxhoang-blog-content/content)
  -> MaxHoang_Notion: scripts/index-chatbot-content.mjs
  -> OpenAI embeddings
  -> data/chatbot-embeddings.json
  -> JsonRetriever (cosine semantic search)
  -> POST /api/chat
  -> OpenAI chat completion (grounded)
  -> Anna UI (messages + source controls)
```

## Indexer content categories (high level)

Under `content/`, published material is chunked and typed roughly as:

- `posts` → `blog`
- `awards` → `award`
- `events` → `event`
- `obsidian` → `obsidian`

Exclusions follow **site publishing rules** (draft / private / unpublished must not appear in the index).

## Key files (MaxHoang_Notion)

| Area | Path |
|------|------|
| Launcher + intro bubble + window switch | `components/chatbot/ChatbotWidget.tsx` |
| Floating open control (if used) | `components/chatbot/ChatbotButton.tsx` |
| Chat shell, messages, quick prompts | `components/chatbot/ChatbotWindow.tsx` |
| Message bubbles + sources | `components/chatbot/ChatMessage.tsx` |
| Input | `components/chatbot/ChatInput.tsx` |
| Avatar | `components/chatbot/AnnaAvatar.tsx` |
| API | `app/api/chat/route.ts` |
| Completion / system rules | `lib/chatbot/chat-completion.ts` |
| Embeddings (runtime) | `lib/chatbot/embedder.ts` |
| Retriever contract | `lib/chatbot/retriever.ts` |
| JSON semantic retriever | `lib/chatbot/retrievers/json-retriever.ts` |
| Shared types | `lib/chatbot/types.ts` |
| Indexing script | `scripts/index-chatbot-content.mjs` |
| Generated index (committed or generated per workflow) | `data/chatbot-embeddings.json` |

## Architecture decision (long-lived)

> The chat layer must **not** care whether chunks live in **JSON**, **Supabase**, or another store. It only talks to a **Retriever** implementation.

Today: **local JSON embeddings file** + `JsonRetriever`. Later: optional **Supabase / pgvector** or **CI indexing** without rewriting the whole UI or route contract.

## Environment (names only; values in `.env`)

- **Required for RAG + chat:** `OPENAI_API_KEY`
- **Common optional:** `OPENAI_EMBEDDING_MODEL`, `OPENAI_CHAT_MODEL`, `OPENAI_CHAT_MAX_OUTPUT_TOKENS`, `CHATBOT_CONTENT_ROOT`, `NEXT_PUBLIC_SITE_URL`

Never commit real keys. Site content pull from GitHub uses separate vault vars (see app `README.md` / `.env.example`).

## Future automation (not required for “memory” but known direction)

1. **Build-time:** run indexer before `next build` (simple; costs embeddings every build).
2. **Manual:** index before deploy (current practical default).
3. **GitHub Action:** on content repo changes, regenerate `chatbot-embeddings.json` and commit or artifact.
4. **Supabase:** move vectors to DB; same retriever pattern, different backend.

## Changelog (high level)

- **v2:** Semantic RAG with local `chatbot-embeddings.json`, `/api/chat`, grounded completions, source UI.
- **Product:** Anna reframed as **journal / audience** assistant; Motion + reduced-motion; direct answers for greeting/contact only.

For **dated implementation steps**, see **`work-log.md`**.
