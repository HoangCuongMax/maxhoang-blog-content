---
title: Website Assistant Chatbot Build Plan
slug: website-assistant-chatbot-build-plan
publish: false
published: false
status: Draft
category: planning
tags:
  - chatbot
  - website
  - OpenRouter
  - Obsidian
  - Supabase
  - RAG
---

# Website Assistant Chatbot Build Plan

## Context

You are helping me build a website assistant chatbot for my existing personal portfolio website.

Important context:

- My website already exists.
- Do not rebuild the whole website.
- Do not change the global design system unless necessary.
- My website uses Next.js App Router, TypeScript, Tailwind CSS, and shadcn/ui.
- The chatbot should use OpenRouter API for chat responses.
- Later, the chatbot will read my Obsidian Markdown notes and answer based on them.
- Build this step by step.
- Before changing important structure, ask me first.
- If you need an API key, environment variable, model choice, Supabase setting, or design opinion, ask me.
- Do not guess private values.
- Do not expose API keys in frontend code.

## Main Goal

Create a floating website assistant chatbot that can eventually answer questions about me, my projects, services, study, achievements, portfolio, and website content.

The final architecture should be:

```text
Obsidian Markdown notes
-> Ingestion script
-> Embeddings
-> Supabase vector database
-> /api/chat retrieval
-> OpenRouter API
-> Chatbot UI on website
```

Build it in safe stages.

---

## Stage 0: Inspect Project First

Before writing code:

1. Inspect the current project structure.
2. Identify:
   - Next.js version and App Router structure
   - Existing `app/layout.tsx`
   - Existing `components` folder
   - Existing shadcn/ui components
   - Existing Tailwind config
   - Existing environment variable pattern
3. Do not rename or move existing files unless necessary.
4. Tell me what you found before making major changes.

---

## Stage 1: Build Chatbot UI Only

Build UI only first.

No OpenRouter API yet.  
No Supabase yet.  
No Obsidian ingestion yet.

Create these files:

```text
components/chatbot/ChatbotWidget.tsx
components/chatbot/ChatbotButton.tsx
components/chatbot/ChatbotWindow.tsx
components/chatbot/ChatMessage.tsx
components/chatbot/ChatInput.tsx
```

Use:

- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- lucide-react

Use shadcn components where suitable:

- Button
- Card
- CardHeader
- CardContent
- CardFooter
- Avatar
- AvatarFallback
- ScrollArea
- Textarea
- Badge
- Separator

If components are missing, ask me before installing them, or suggest this command:

```bash
npx shadcn@latest add button card avatar scroll-area textarea badge separator
```

### UI Behaviour

1. Show floating circular chatbot button at bottom-right.
2. Clicking the button opens chatbot window.
3. Chatbot window appears bottom-right on desktop.
4. On mobile, chatbot window should be almost full width.
5. User can type message.
6. Press Enter to send.
7. Shift + Enter creates new line.
8. Empty messages cannot be sent.
9. Show fake loading state.
10. Return fake response.
11. Show suggested question chips before first user message.
12. Clicking a suggested chip sends that question.
13. Auto-scroll to latest message.
14. Close button closes the window.

Assistant name:

```text
Max AI Assistant
```

Welcome message:

```text
Hi, I’m Max’s website assistant. You can ask me about Max’s projects, skills, services, study, and portfolio.
```

Suggested questions:

- Who is Max Hoang?
- What AI projects has Max built?
- What services does Max offer?
- What awards has Max won?
- How can I contact Max?

Fake response:

```text
Thanks for your question. This is a UI demo for now. In the next step, I will connect this chatbot to Max’s Obsidian notes and website content.
```

### Desktop Style

- Floating button: `fixed bottom-6 right-6 z-50`
- Button size: `h-14 w-14 rounded-full`
- Chat window: `fixed bottom-24 right-6 z-50`
- Width: `380px`
- Height: `560px`
- `rounded-2xl`
- `shadow-2xl`
- `border`

### Mobile Style

- Button: `bottom-4 right-4`
- Window: `bottom-20 left-3 right-3`
- Width: `calc(100vw - 24px)`
- Height: `75vh`

Use theme tokens:

- `bg-background`
- `bg-card`
- `text-card-foreground`
- `bg-muted`
- `text-muted-foreground`
- `bg-primary`
- `text-primary-foreground`
- `border-border`

Do not hard-code many colours.

Add `<ChatbotWidget />` to `app/layout.tsx` so it appears on every page.

Important:

- Do not break the existing layout.
- If `app/layout.tsx` has custom providers, keep them unchanged.

---

## Stage 2: Add OpenRouter Backend Route

After UI is working, add OpenRouter connection.

Create:

```text
app/api/chat/route.ts
```

This route should:

1. Accept POST request with:

```json
{
  "message": "user message"
}
```

2. Validate message is not empty.
3. Read environment variables:
   - `OPENROUTER_API_KEY`
   - `OPENROUTER_MODEL`
4. If missing API key, return a clear error:

```text
OpenRouter API key is not configured.
```

5. Call OpenRouter chat completions endpoint:

```text
https://openrouter.ai/api/v1/chat/completions
```

6. Use Authorization Bearer token.
7. Use a safe default model if `OPENROUTER_MODEL` is missing:

```text
openrouter/free
```

8. Return:

```json
{
  "answer": "...",
  "sources": []
}
```

Important:

- API key must only be used in server route.
- Never expose `OPENROUTER_API_KEY` to frontend.
- Do not use `NEXT_PUBLIC` for the API key.
- Add basic error handling.
- Add request timeout if reasonable.
- Keep code simple.

Environment variables:

```env
OPENROUTER_API_KEY=
OPENROUTER_MODEL=openrouter/free
```

Optional OpenRouter headers:

```text
HTTP-Referer: my website URL
X-Title: Max Hoang Website Assistant
```

If website URL is unknown, ask me.

System prompt for basic stage:

```text
You are Max Hoang’s website assistant. Answer in a clear, friendly, professional way. Keep answers short. If you do not know something, say you do not have enough information yet. This chatbot will later connect to Max’s website and Obsidian notes.
```

---

## Stage 3: Connect UI To /api/chat

Update the chatbot UI.

Replace fake response with real call to:

```text
POST /api/chat
```

Request:

```json
{
  "message": "userMessage"
}
```

Response:

```json
{
  "answer": "...",
  "sources": []
}
```

Keep loading state.  
Keep error state.

If API fails, show:

```text
Sorry, I could not answer right now. Please try again later.
```

Do not remove the demo UI features.  
Keep suggested question chips.

---

## Stage 4: Prepare Obsidian Content Structure

Create folder:

```text
content/obsidian/
```

Add example file only:

```text
content/obsidian/about-max.example.md
```

Example content:

```md
---
title: About Max Hoang
publish: true
category: about
tags:
  - portfolio
  - about
slug: about-max
---

# About Max Hoang

This is an example public note for the chatbot. Replace this with real Obsidian content later.
```

Important privacy rule:

```text
Only process notes with publish: true.
```

Ignore folders:

- private
- journal
- family
- finance
- visa
- passwords
- health
- archive
- templates

Do not import my whole Obsidian vault yet.  
Ask me before adding real notes.

---

## Stage 5: Add Supabase Schema For Future RAG

Only do this when I confirm Supabase is ready.

Create:

```text
supabase/schema.sql
```

Use pgvector.

Schema:

```sql
create extension if not exists vector;

create table if not exists documents (
  id uuid primary key default gen_random_uuid(),
  title text,
  source_path text not null,
  slug text,
  category text,
  tags text[],
  content text not null,
  chunk_index int not null,
  embedding vector(1536),
  publish boolean default true,
  updated_at timestamptz default now()
);

create index if not exists documents_embedding_idx
on documents
using ivfflat (embedding vector_cosine_ops)
with (lists = 100);

create index if not exists documents_source_path_idx
on documents(source_path);

create or replace function match_documents (
  query_embedding vector(1536),
  match_count int default 8,
  match_threshold float default 0.75
)
returns table (
  id uuid,
  title text,
  source_path text,
  slug text,
  category text,
  tags text[],
  content text,
  similarity float
)
language sql stable
as $$
  select
    documents.id,
    documents.title,
    documents.source_path,
    documents.slug,
    documents.category,
    documents.tags,
    documents.content,
    1 - (documents.embedding <=> query_embedding) as similarity
  from documents
  where 1 - (documents.embedding <=> query_embedding) > match_threshold
  order by documents.embedding <=> query_embedding
  limit match_count;
$$;
```

Ask me before applying this to Supabase.

---

## Stage 6: Add Ingestion Script

Only do this after I confirm Supabase keys and embedding provider.

Create:

```text
scripts/ingest-notes.ts
```

The script should:

1. Read Markdown files from `content/obsidian`.
2. Ignore private folders.
3. Parse frontmatter.
4. Only process `publish: true`.
5. Remove frontmatter.
6. Convert Obsidian links:
   - `[[Note Name]]` -> `Note Name`
   - `![[image.png]]` -> remove for now
7. Split content into chunks.
8. Create embeddings.
9. Delete old chunks for same `source_path`.
10. Insert new chunks into Supabase `documents` table.
11. Log indexed files and chunks.

Use package:

```text
gray-matter
```

Use package:

```text
@supabase/supabase-js
```

Use embedding provider:

```text
OpenAI text-embedding-3-small
```

Environment variables:

```env
NEXT_PUBLIC_SUPABASE_URL=
SUPABASE_SERVICE_ROLE_KEY=
OPENAI_API_KEY=
EMBEDDING_MODEL=text-embedding-3-small
```

Add script to `package.json`:

```json
{
  "ingest": "tsx scripts/ingest-notes.ts"
}
```

Ask me before installing dependencies.

---

## Stage 7: Add RAG Retrieval

Only do this after ingestion works.

Create:

```text
lib/retrieval.ts
lib/prompt.ts
lib/embeddings.ts
```

Retrieval flow:

1. Take user message.
2. Create embedding for query.
3. Call Supabase RPC `match_documents`.
4. Get top relevant chunks.
5. If no chunks are found, return no-context response.
6. Build context.
7. Send context + question to OpenRouter.
8. Return answer + source list.

RAG system prompt:

```text
You are Max Hoang’s website assistant.

You answer questions about Max, his projects, skills, study, work, services, blog content, and public portfolio information.

You must answer only using the provided context from Max's website and Obsidian notes.

Rules:
- Do not invent facts.
- If the answer is not in the context, say you do not have enough information in Max’s public notes.
- Keep answers clear, friendly, and professional.
- Use simple language.
- Do not reveal private or hidden information.
- Do not answer as if you are Max unless specifically asked to draft text for him.
- If a visitor asks about hiring Max, explain his relevant services and suggest contacting him through the website.
```

Update `app/api/chat/route.ts`:

- First retrieve relevant context.
- If context exists, call OpenRouter with context.
- If no context exists, return:

```text
I do not have enough information in Max’s public notes to answer that yet.
```

- Return sources.

---

## Stage 8: Add GitHub Actions Auto-Ingest

Only do this after manual ingestion works.

Create:

```text
.github/workflows/ingest.yml
```

Workflow:

- Trigger on push to `content/obsidian/**/*.md`
- Install dependencies
- Run `npm run ingest`
- Use GitHub secrets for API keys

Ask me before creating workflow if deployment structure is unclear.

---

## Safety Rules For Codex

1. Work in small steps.
2. Do not refactor unrelated files.
3. Do not delete existing components.
4. Do not rename existing routes.
5. Do not change global CSS unless necessary.
6. Do not overwrite `app/layout.tsx`. Only add `ChatbotWidget` carefully.
7. Do not expose API keys in frontend.
8. Do not commit `.env.local`.
9. Update `.env.example` only.
10. Ask me before installing packages.
11. Ask me before adding Supabase.
12. Ask me before changing database schema.
13. Ask me before importing real Obsidian notes.
14. After each stage, run:
    - `npm run lint`
    - `npm run build`
15. If build fails, fix only related errors.
16. Explain what changed after each stage.

---

## First Task For Codex

Start with Stage 0 and Stage 1 only.

Do not connect OpenRouter yet.

Inspect the project, then create the shadcn chatbot UI.

After Stage 1 is working, stop and ask me before moving to Stage 2.
