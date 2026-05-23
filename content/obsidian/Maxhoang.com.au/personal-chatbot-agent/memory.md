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
- **Anna brain architecture folder:** `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/personal-chatbot-agent/anna-brain-architecture`

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
  -> Anna UI (message stream + compact footer actions)
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
| Chat shell, messages, quick prompts, footer actions, desktop sidebar layout | `components/chatbot/ChatbotWindow.tsx` |
| Message bubbles and admin panel rendering | `components/chatbot/ChatMessage.tsx` |
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

## UI behaviour (current)

- The chat scroll area should stay focused on conversation messages only.
- First open uses a pre-chat welcome flow with optional name capture and optional newsletter signup before the normal chat input appears.
- Latest `Sources`, `Continue` suggestions, and contextual `Feedback` live in a compact footer action area above the input.
- Sources are collapsed behind a `Sources` button and expand in the footer action area.
- Feedback appears after roughly every third saved assistant answer, hides after a rating/correction, and also hides when the visitor continues without rating.
- On desktop, the open chatbot is a right-side overlay sidebar using full viewport height. On mobile, it remains compact/fullscreen as appropriate.
- Anna uses warmer identity copy, rotating status text, conversational suggested questions, and a stronger assistant/researcher/collaborator personality layer.
- General chat, greetings, identity questions, capability questions, and small talk such as "How are you?" are handled directly before retrieval so Anna does not search the site for basic conversation.
- Minimized widget reveals an inline quick-chat input when the visitor hovers or focuses the message bubble. It calls `/api/chat` with `mode: "mini"` and shows short 1-2 sentence answers without opening the full chatbot. The avatar stays large and fixed in place while the mini input opens.
- Desktop expand mode should become a true fullscreen overlay while the normal open state remains a full-height right-side sidebar.

## Environment (names only; values in `.env`)

- **Required for RAG + chat:** `OPENAI_API_KEY`
- **Common optional:** `OPENAI_EMBEDDING_MODEL`, `OPENAI_CHAT_MODEL`, `OPENAI_CHAT_MAX_OUTPUT_TOKENS`, `CHATBOT_CONTENT_ROOT`, `NEXT_PUBLIC_SITE_URL`

Never commit real keys. Site content pull from GitHub uses separate vault vars (see app `README.md` / `.env.example`).

## Future automation (not required for “memory” but known direction)

1. **Build-time:** run indexer before `next build` (simple; costs embeddings every build).
2. **Manual:** index before deploy (current practical default).
3. **GitHub Action:** on content repo changes, regenerate `chatbot-embeddings.json` and commit or artifact.
4. **Supabase:** move vectors to DB; same retriever pattern, different backend.

## Future Anna brain architecture

The `anna-brain-architecture/` folder captures the planned shift from chatbot UI to digital personality system.

The target design has three memory layers:

- **Knowledge memory:** factual website content such as posts, projects, notes, awards, services, events, and FAQs.
- **Personality memory:** Anna's identity, speech style, behaviour rules, emotional patterns, mood states, and dialogue examples.
- **Relationship memory:** session and future long-term context about visitor intent, interests, preferred depth, and visitor type.

Long term, personality docs and dialogue examples can be embedded alongside factual content with metadata such as `memory_layer: personality`, then retrieved before response generation. Keep this separate from factual claims about Max.

Recommended structure is documented in `anna-brain-architecture/markdown-brain-structure.md` and now exists at the content repo root: `maxhoang-blog-content/markdown-brain/`.

Current app support:

- `MaxHoang_Notion/lib/chatbot/personality-memory.ts` loads approved markdown-brain personality, relationship, and training notes at runtime when available.
- `MaxHoang_Notion/scripts/index-chatbot-content.mjs` indexes `markdown-brain` docs with `memoryLayer` metadata for future embedding retrieval.
- `MaxHoang_Notion/app/api/chat/route.ts` filters factual sources to `memoryLayer: knowledge` while passing personality/relationship/training context to the model separately.

The key learning rule remains: Anna can record conversations automatically, but only Max can approve changes to Anna's Markdown memory. Approved memory should then be embedded and used in future retrieval.

## Changelog (high level)

- **v2:** Semantic RAG with local `chatbot-embeddings.json`, `/api/chat`, grounded completions, source UI.
- **v2 UI refinement:** Clean message stream with footer-based Sources/Continue/Feedback controls and a desktop right overlay sidebar.
- **Product:** Anna reframed as **journal / audience** assistant; Motion + reduced-motion; direct answers for greeting/contact only.
- **Architecture planning:** Added Anna brain architecture docs for knowledge memory, personality memory, relationship memory, mood states, dialogue examples, and future personality retrieval.
- **Markdown brain v1:** Added root `markdown-brain/` approved memory files plus app support for runtime personality memory loading and memory-layer-aware indexing.

For **dated implementation steps**, see **`work-log.md`**.
