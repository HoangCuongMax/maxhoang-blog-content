---
title: Anna chatbot - agents router
type: agents-router
status: active
published: false
project: personal-portfolio-chatbot
tags:
  - personal-chatbot
  - anna-assistant
---

# AGENTS - Personal chatbot (Anna)

**Parent agent:** `../AGENTS.md` (MaxHoang.com.au website agent)

**Start every session** about the Max Hoang Journal website chatbot by reading these notes **in order**:

1. **`../AGENTS.md`** - Website-wide rules and parent reporting.
2. **`agent-instruction.md`** - Persona, behaviour, safety, and what "good" looks like for Anna.
3. **`memory.md`** - Repos, paths, architecture, pipeline, and stable facts about the implementation.
4. **`work-instruction.md`** - Commands, env, Git workflow, indexing, verification, and how to log work.

## Website code structure to know

The runnable website app is the **MaxHoang_Notion** Next.js repo, not this Obsidian folder. For chatbot work, assume this app structure:

| Area | Path | What to check |
|---|---|---|
| App routes | `MaxHoang_Notion/app/` | Next.js App Router pages, layouts, API routes, and route metadata. |
| Chat API | `MaxHoang_Notion/app/api/chat/route.ts` | Request handling, direct greeting/contact answers, fallback responses, source payloads, and retriever wiring. |
| Chat completion | `MaxHoang_Notion/lib/chatbot/chat-completion.ts` | Anna system prompt, answer rules, OpenAI chat request, context formatting, and output limits. |
| Retriever contract | `MaxHoang_Notion/lib/chatbot/retriever.ts` | Storage-agnostic search interface used by the API route. |
| JSON retriever | `MaxHoang_Notion/lib/chatbot/retrievers/json-retriever.ts` | Local embedding index loading, query embeddings, cosine search, result scoring, and minimum score threshold. |
| Embeddings | `MaxHoang_Notion/lib/chatbot/embedder.ts` | OpenAI embedding calls and embedding model configuration. |
| Chatbot types | `MaxHoang_Notion/lib/chatbot/types.ts` | Shared chunk, index, and search result shapes. |
| Chat UI shell | `MaxHoang_Notion/components/chatbot/ChatbotWindow.tsx` | Conversation flow, welcome/name steps, quick prompts, message submission, loading/error states, and window layout. |
| Messages and sources | `MaxHoang_Notion/components/chatbot/ChatMessage.tsx` | Assistant/user bubble rendering and source button display. |
| Input | `MaxHoang_Notion/components/chatbot/ChatInput.tsx` | User text entry, submit controls, and input accessibility. |
| Launcher/widget | `MaxHoang_Notion/components/chatbot/ChatbotWidget.tsx` | Floating launcher, intro bubble, open/close behaviour, and reduced-motion handling. |
| Avatar | `MaxHoang_Notion/components/chatbot/AnnaAvatar.tsx` | Anna avatar image variants and rendering. |
| Indexer script | `MaxHoang_Notion/scripts/index-chatbot-content.mjs` | Published content discovery, exclusions, chunking, source URLs, metadata, and embedding generation. |
| Generated index | `MaxHoang_Notion/data/chatbot-embeddings.json` | Generated RAG chunks and embeddings used by the local JSON retriever. |
| Global styling | `MaxHoang_Notion/app/globals.css` | Theme tokens and chatbot surface/message styling. |
| Package commands | `MaxHoang_Notion/package.json` | `dev`, `lint`, `build`, `typecheck`, and `index-chatbot-content` scripts. |

## Content structure to know

The content source is the **maxhoang-blog-content** repo:

| Area | Path | What to check |
|---|---|---|
| Blog posts | `maxhoang-blog-content/content/posts/` | Published post Markdown used by the site and chatbot index. |
| Awards | `maxhoang-blog-content/content/awards/` | Public awards and recognition content. |
| Events | `maxhoang-blog-content/content/events/` | Public event entries. |
| Obsidian notes | `maxhoang-blog-content/content/obsidian/` | Notes and internal docs; only published/public material should be indexed. |
| Website agent docs | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/` | Website-wide agent instructions, memory, workflow, and work log. |
| Chatbot agent docs | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/personal-chatbot-agent/` | Anna-specific instructions, answer rules, workflow, memory, and work log. |

## Chatbot change checklist

- For answer behaviour, check `chatbot-answer-rules.md`, then update `MaxHoang_Notion/lib/chatbot/chat-completion.ts` or `MaxHoang_Notion/app/api/chat/route.ts`.
- For retrieval or content coverage, check `scripts/index-chatbot-content.mjs`, `lib/chatbot/retrievers/json-retriever.ts`, and `data/chatbot-embeddings.json`.
- For visible chatbot experience, check `components/chatbot/*` and `app/globals.css`.
- For content-only changes, check frontmatter and publishing rules before regenerating embeddings.
- After content or indexing changes, run `npm run index-chatbot-content` from `MaxHoang_Notion` when Node tooling is available.

**Reporting rule:** append dated one-liners to **`work-log.md`** when you change chatbot code, content, or this folder. Add a short parent entry to `../work-log.md` when chatbot work changes website behaviour, app implementation, workflow, or agent structure.

This folder lives under the content vault: `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/personal-chatbot-agent`. The runnable app is **not** here; it is in the **MaxHoang_Notion** Next.js repo (see `memory.md`).
