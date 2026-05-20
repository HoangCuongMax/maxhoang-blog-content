# AGENTS.md - Personal Chatbot Project Startup Guide

Use this file at the start of every session about the personal chatbot project.

## Project Identity

- Project: Personal Portfolio Website Assistant Chatbot
- Assistant persona: Anna Assistant
- Website: `https://maxhoang.com.au`
- Main app folder: `/Users/hoangcuong/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/MaxHoang_Notion`
- Content vault folder: `/Users/hoangcuong/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/maxhoang-blog-content`
- Planning folder: `/Users/hoangcuong/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/maxhoang-blog-content/content/obsidian/personal-chatbot`

Anna is no longer only a personal-profile bot. Current positioning is:

> Anna is a blog and audience assistant for Max Hoang Journal. She helps readers explore blog posts, AI and data notes, project write-ups, events, resources, and ways to contact or subscribe.

## Read First

Start each session by reading these notes in this order:

1. `personal-chatbot-index.md`
2. `codex-work-log.md`
3. `version-2-chatbot-implementation-plan.md`
4. `Personal Portfolio Website Assistant Chatbot Brief.md`
5. `Expert Chatbot Assignment Requirements.md`

Use the build plan and presentation notes when the task involves architecture, assignment explanation, or slides:

- `personal-chatbot-build-plan.md`
- `expert-chatbot-5-minute-slide-content.md`
- `expert-chatbot-presentation-task-division.md`

## Current Implementation State

The chatbot is implemented in the `MaxHoang_Notion` Next.js app.

Important files:

- UI shell: `components/chatbot/ChatbotWidget.tsx`
- Open button and intro bubble: `components/chatbot/ChatbotButton.tsx`
- Chat window: `components/chatbot/ChatbotWindow.tsx`
- Message rendering and source buttons: `components/chatbot/ChatMessage.tsx`
- Input: `components/chatbot/ChatInput.tsx`
- API route: `app/api/chat/route.ts`
- Chat completion helper: `lib/chatbot/chat-completion.ts`
- Embedding helper: `lib/chatbot/embedder.ts`
- Retriever interface: `lib/chatbot/retriever.ts`
- JSON semantic retriever: `lib/chatbot/retrievers/json-retriever.ts`
- Shared types: `lib/chatbot/types.ts`
- Embedding index script: `scripts/index-chatbot-content.mjs`
- Local embedding index: `data/chatbot-embeddings.json`

Current pipeline:

```txt
Published Markdown content
-> scripts/index-chatbot-content.mjs
-> OpenAI embeddings
-> data/chatbot-embeddings.json
-> JsonRetriever semantic search
-> /api/chat
-> OpenAI chat completion
-> Anna chatbot UI with source buttons
```

## Commands

Run commands from the `MaxHoang_Notion` folder.

```bash
npm run dev
npm run index-chatbot-content
npm run lint
npm run build
```

Use `npm run index-chatbot-content` after content changes. It regenerates `data/chatbot-embeddings.json`.

## Environment Variables

Required for indexing and runtime semantic search:

```env
OPENAI_API_KEY=
```

Optional:

```env
OPENAI_EMBEDDING_MODEL=text-embedding-3-small
OPENAI_CHAT_MODEL=gpt-4.1-nano
OPENAI_CHAT_MAX_OUTPUT_TOKENS=180
CHATBOT_CONTENT_ROOT=
NEXT_PUBLIC_SITE_URL=https://maxhoang.com.au
```

Rules:

- Never commit real API keys.
- Keep API usage server-side only.
- If `OPENAI_API_KEY` is missing, UI work can continue but live retrieval/answer generation will fail.

## Content Rules

Markdown in `maxhoang-blog-content/content` is the source of truth.

The indexer currently includes:

- `posts` as `blog`
- `awards` as `award`
- `events` as `event`
- `obsidian` as `obsidian`

Only published/public/visible notes should be indexed. Draft, hidden, private, archived, and unpublished notes must stay out of the chatbot index.

When changing indexing behavior, keep it aligned with the website publishing rules.

## Chatbot Behavior Rules

Anna should:

- Answer only from retrieved Max Hoang Journal / website content.
- Keep responses concise, friendly, and useful.
- Help users find blog posts, AI/data notes, project write-ups, events, and resources.
- Show source buttons through the UI instead of putting raw URLs in answer text.
- Give a clear fallback when the content does not support an answer.
- Avoid unsupported claims about Max, private personal details, or facts not in the content.
- Avoid medical, legal, financial, or unrelated advice.

Fallback style:

> I do not have enough information about that in Max's website content. I can help with questions about Max, his projects, awards, blog posts, skills, and portfolio instead.

## Current Direct Answers

`app/api/chat/route.ts` handles some questions without calling the model:

- Greetings introduce Anna as the guide to Max Hoang Journal.
- Contact questions point users to the website contact page.

Keep direct answers cheap and narrow. Do not add broad rule-based answers that bypass retrieval unless the answer is stable and obvious.

## Implementation Guidelines

- Keep the chat API storage-independent. It should call the retriever interface, not embed JSON-specific logic.
- Keep JSON retrieval isolated in `json-retriever.ts`.
- Keep OpenAI embedding calls in `embedder.ts` or the indexing script.
- Keep answer-generation rules in `chat-completion.ts`.
- Preserve the source-button UI pattern in `ChatMessage.tsx`.
- Maintain reduced-motion support when editing Motion animations.
- Do not expose API keys to client components.
- After changing chatbot code, run `npm run lint` and `npm run build`.
- After changing indexed content or indexing logic, run `npm run index-chatbot-content` before testing.

## Test Prompts

Use these prompts for manual checks:

- `Hello, who are you?`
- `Show me AI blog posts`
- `Find data analytics notes`
- `What projects are featured?`
- `What awards has Max won?`
- `How can I contact Max?`
- `Can you give me medical advice?`
- `What is Max's favourite movie?`

Expected behavior:

- Greetings and contact questions should work directly.
- Domain questions should return grounded answers and source buttons.
- Out-of-scope or unsupported questions should use fallback behavior.

## Work Log Rule

When Codex creates, edits, fixes, or reorganizes files for this project, update:

```txt
codex-work-log.md
```

Keep the log short and dated.
