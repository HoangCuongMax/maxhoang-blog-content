---
title: Version 2 Chatbot Implementation Plan
type: implementation-plan
status: active
published: true
project: personal-portfolio-chatbot
domain: personal portfolio website assistant
tags:
  - personal-chatbot
  - rag
  - embeddings
  - vercel
  - implementation-plan
---

# Version 2 Chatbot Implementation Plan

## Summary

Version 2 adds semantic search to the personal portfolio chatbot.

The pipeline is:

```txt
Markdown files
-> chunks
-> OpenAI embeddings
-> data/chatbot-embeddings.json
-> semantic search
-> chatbot response
```

The implementation is in the `MaxHoang_Notion` Next.js app, while the source content comes from the sibling `maxhoang-blog-content` Markdown vault.

API keys must stay in environment variables only. They should be configured locally in `.env.local` and later in Vercel Project Settings.

## Implemented Files

In `MaxHoang_Notion`:

- `scripts/index-chatbot-content.mjs`
- `data/chatbot-embeddings.json`
- `lib/chatbot/types.ts`
- `lib/chatbot/retriever.ts`
- `lib/chatbot/embedder.ts`
- `lib/chatbot/retrievers/json-retriever.ts`
- `app/api/chat/route.ts`
- `components/chatbot/ChatbotWindow.tsx`
- `.env.example`
- `package.json`

In `maxhoang-blog-content`:

- `content/obsidian/personal-chatbot/codex-work-log.md`

## How The System Works

1. The indexing script reads published Markdown files from `maxhoang-blog-content/content`.
2. The script parses frontmatter and Markdown body content.
3. Draft, private, hidden, and unpublished notes are excluded.
4. Published content is cleaned and split into chunks.
5. Each chunk is sent to OpenAI to generate an embedding.
6. The generated chunks are saved to `MaxHoang_Notion/data/chatbot-embeddings.json`.
7. When a user asks the chatbot a question, `/api/chat` embeds the question.
8. The JSON retriever compares the question embedding against stored chunk embeddings.
9. The chatbot returns a grounded answer from the most relevant chunks.
10. If no relevant content is found, the chatbot returns a fallback response.

## Environment Variables

Required:

```env
OPENAI_API_KEY=
```

Optional:

```env
OPENAI_EMBEDDING_MODEL=text-embedding-3-small
```

For Vercel, add these in:

```txt
Vercel Dashboard
-> Project
-> Settings
-> Environment Variables
```

Do not commit real API keys to the repository.

## Current Update Workflow

At the moment, embeddings are not fully automatic.

When new Markdown content is added or existing content changes, run this manually from the `MaxHoang_Notion` folder:

```bash
npm run index-chatbot-content
```

This regenerates:

```txt
data/chatbot-embeddings.json
```

Then the chatbot can search the updated content.

## Future Automatic Options

### Option 1: Build-Time Update

Run the indexing script before every production build.

Example future package script:

```json
{
  "scripts": {
    "build": "npm run index-chatbot-content && next build"
  }
}
```

This is simple, but every Vercel build would call the OpenAI embeddings API.

### Option 2: Manual Update Before Deployment

Keep the current workflow:

```bash
npm run index-chatbot-content
npm run build
```

This gives more control and avoids unexpected embedding API usage.

### Option 3: GitHub Action

Create a GitHub Action that runs when Markdown content changes.

The action can:

- Check out the website repo and content repo.
- Run `npm install`.
- Run `npm run index-chatbot-content`.
- Commit the updated `data/chatbot-embeddings.json`.
- Trigger or support deployment.

This is the best long-term option if the content changes often.

### Option 4: Supabase Version 3

Later, move embeddings from local JSON to Supabase `pgvector`.

Then the update flow becomes:

```txt
Markdown change
-> indexing script
-> embeddings generated
-> Supabase vector table updated
-> chatbot searches Supabase
```

## Recommended Workflow For Now

For the assignment and demo, use manual regeneration.

Recommended steps:

```bash
cd MaxHoang_Notion
npm run index-chatbot-content
npm run build
```

Use Vercel environment variables for API keys later.

This keeps the project simple, avoids surprise API cost, and is easier to explain in the presentation.

## Testing Checklist

- [ ] Add `OPENAI_API_KEY` locally.
- [ ] Run `npm run index-chatbot-content`.
- [ ] Confirm `data/chatbot-embeddings.json` contains chunks and embedding arrays.
- [ ] Run `npm run lint`.
- [ ] Run `npm run build`.
- [ ] Test the chatbot with: `Who is Max Hoang?`
- [ ] Test the chatbot with: `What AI projects has Max built?`
- [ ] Test the chatbot with: `What awards has Max won?`
- [ ] Test the chatbot with an out-of-scope question.

## Presentation Explanation

The current system uses a manual update workflow:

> When the website content changes, the indexing script is run again. It reads the Markdown content, creates new chunks, generates embeddings, and updates the chatbot's local semantic search file.

Future improvement:

> This can be automated later using a build-time script, GitHub Action, or Supabase vector database.
