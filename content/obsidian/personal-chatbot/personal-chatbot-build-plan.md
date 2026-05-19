---
title: Personal Portfolio Chatbot Build Plan
type: build-plan
status: active
project: personal-portfolio-chatbot
domain: personal portfolio website assistant
website: https://maxhoang.com.au
tags:
  - personal-chatbot
  - build-plan
  - rag
  - supabase-ready
  - maxhoang-website
---

# Personal Portfolio Chatbot Build Plan

## Navigation

- Project index: [[personal-chatbot-index]]
- Assignment requirements: [[expert-chatbot-assignment-requirements]]
- Project brief: [[personal-portfolio-chatbot-brief]]

## Relationship to Project

This note is the implementation roadmap for the chatbot described in [[personal-portfolio-chatbot-brief]]. It also maps the project back to the assignment requirements in [[expert-chatbot-assignment-requirements]].

## Goal

Build a small chatbot widget for `maxhoang.com.au` that reads Markdown/Obsidian website content and answers questions about Max Hoang, his projects, awards, blog posts, skills, and website content.

The chatbot should act as a personal portfolio website assistant and showcase chatbot development skills.

## Build Strategy

Use a step-by-step approach so the website structure is not broken. Start with the UI only, then add content loading, retrieval, AI response generation, testing, and deployment.

The system should be built in an upgradeable way. Version 1 can use a local JSON index, but the architecture must be ready to move to Supabase later without rewriting the whole chatbot.

Core design rule:

> The chatbot should not care whether the knowledge comes from JSON or Supabase. It should only call a retriever interface.

This means JSON storage is only the first storage option. Supabase can be added later by replacing the retriever layer.

---

# Upgradeable RAG Architecture

## Target Architecture

```txt
Markdown / Obsidian notes
        ↓
content loader
        ↓
chunking system
        ↓
embedding system
        ↓
retriever interface
        ↓
chat API
        ↓
chatbot UI
```

## Recommended Folder Structure

```txt
src/
  lib/
    chatbot/
      content-loader.ts
      chunker.ts
      embedder.ts
      retriever.ts
      prompts.ts
      types.ts
      retrievers/
        json-retriever.ts
        supabase-retriever.ts

scripts/
  index-chatbot-content.ts
  upload-chatbot-index-to-supabase.ts

data/
  chatbot-index.json
  chatbot-embeddings.json
```

## Shared Chunk Type

The project should use one shared chunk type from the beginning, even before Supabase is added.

```ts
export type ChatbotChunk = {
  id: string;
  title: string;
  path: string;
  slug?: string;
  tags?: string[];
  category?: string;
  content: string;
  sourceUrl?: string;
  embedding?: number[];
  createdAt?: string;
  updatedAt?: string;
};
```

## Retriever Interface

All retrieval systems should follow the same interface.

```ts
export interface Retriever {
  search(query: string, limit?: number): Promise<ChatbotChunk[]>;
}
```

Version 1 can use:

```ts
const retriever = new JsonRetriever();
```

Later, the production version can use:

```ts
const retriever = new SupabaseRetriever();
```

The chat API should not contain hard-coded JSON search logic. JSON logic should stay inside `json-retriever.ts` only.

## Storage Upgrade Path

```txt
Version 1:
Markdown → chunks → chatbot-index.json → keyword search

Version 2:
Markdown → chunks → embeddings → chatbot-embeddings.json → semantic search

Version 3:
Markdown → chunks → embeddings → Supabase pgvector → production RAG search
```

## Future Supabase Table Design

```sql
create table chatbot_documents (
  id text primary key,
  title text,
  path text,
  slug text,
  tags text[],
  category text,
  content text,
  source_url text,
  embedding vector(1536),
  created_at timestamp,
  updated_at timestamp
);
```

## RAG Update Rule

Markdown content is the source of truth. The RAG index is only a searchable copy of the Markdown content.

Whenever website content changes, the RAG index should be regenerated or updated.

Update flow:

```txt
Update Obsidian note
→ push to GitHub
→ website rebuilds or GitHub Action runs
→ indexing script reads Markdown
→ JSON index or Supabase vector table updates
→ chatbot answers from latest indexed content
```

---

# Phase 1: Confirm Project Scope

## Tasks

- [ ] Confirm the chatbot domain: personal portfolio website assistant.
- [ ] Confirm target users: visitors, students, employers, recruiters, and collaborators.
- [ ] Confirm main website: `maxhoang.com.au`.
- [ ] Confirm content source: Markdown/Obsidian files.
- [ ] Confirm the chatbot will only answer based on available website content.
- [ ] Confirm fallback behaviour for unsupported questions.
- [ ] Confirm JSON-first but Supabase-ready architecture.

## Output

- Clear project scope.
- Confirmed chatbot role and limitations.
- Confirmed upgrade path from JSON to Supabase.

---

# Phase 2: Create Chatbot UI Only

## Goal

Create a small chatbot widget on the website without connecting it to AI yet.

## Tasks

- [ ] Add a chatbot floating button to the website.
- [ ] Place the button at the bottom-right corner.
- [ ] Use a clean icon for the chatbot.
- [ ] Open a small chat window when the user clicks the button.
- [ ] Add a header with chatbot name.
- [ ] Add a welcome message.
- [ ] Add message bubbles for user and assistant.
- [ ] Add a text input box.
- [ ] Add a send button.
- [ ] Make the UI responsive for desktop and mobile.
- [ ] Match the website design style.
- [ ] Use shadcn/ui components where suitable.

## Output

- Chatbot UI is visible and working.
- User can type messages.
- Chat window can open and close.
- No AI connection yet.

---

# Phase 3: Prepare Markdown Content Source

## Goal

Prepare the website Markdown/Obsidian content so the chatbot can use it later.

## Tasks

- [ ] Identify all Markdown folders used by the website.
- [ ] Confirm which content folders should be included.
- [ ] Exclude private or unfinished notes if needed.
- [ ] Read frontmatter fields such as title, description, date, tags, slug, and category.
- [ ] Extract body content from Markdown files.
- [ ] Remove unnecessary Markdown syntax where needed.
- [ ] Keep useful headings and metadata.
- [ ] Create a clean content format for indexing.
- [ ] Map content fields to the shared `ChatbotChunk` type.

## Suggested Included Content

- [ ] Blog posts
- [ ] Project notes
- [ ] Award notes
- [ ] Event notes
- [ ] Portfolio notes
- [ ] Website assistant notes

## Output

- Markdown content can be loaded and prepared for search.
- Content format is ready for both JSON and Supabase storage.

---

# Phase 4: Build Content Indexing Script

## Goal

Create a script that reads all Markdown files and converts them into searchable chunks.

## Tasks

- [ ] Create `scripts/index-chatbot-content.ts`.
- [ ] Load Markdown files from the selected content folders.
- [ ] Parse frontmatter.
- [ ] Split long content into smaller chunks.
- [ ] Keep metadata for each chunk.
- [ ] Include title, slug, path, tags, category, source URL, created date, and updated date where possible.
- [ ] Generate stable chunk IDs so updates can replace old content later.
- [ ] Save indexed content to `data/chatbot-index.json` for the first version.
- [ ] Keep the structure close to the future Supabase table design.

## Example Chunk Fields

- `id`
- `title`
- `slug`
- `path`
- `tags`
- `category`
- `content`
- `sourceUrl`
- `createdAt`
- `updatedAt`

## Output

- A searchable JSON content index exists.
- The chatbot has a structured knowledge source.
- The index can later be uploaded to Supabase with minimal changes.

---

# Phase 5: Add Retriever Interface and JSON Retriever

## Goal

Build retrieval in a modular way so JSON can be replaced by Supabase later.

## Tasks

- [ ] Create `src/lib/chatbot/types.ts`.
- [ ] Add the shared `ChatbotChunk` type.
- [ ] Create `src/lib/chatbot/retriever.ts`.
- [ ] Add the shared `Retriever` interface.
- [ ] Create `src/lib/chatbot/retrievers/json-retriever.ts`.
- [ ] Load `data/chatbot-index.json`.
- [ ] Implement simple keyword search.
- [ ] Return results using the shared `ChatbotChunk` type.
- [ ] Keep the chat API independent from JSON details.

## Output

- JSON retrieval works.
- The chatbot can later use Supabase by changing the retriever only.

---

# Phase 6: Add Simple Search First

## Goal

Before using AI, test whether the chatbot can find relevant website content using simple search.

## Tasks

- [ ] Add keyword search over indexed Markdown chunks.
- [ ] Match questions with titles, tags, headings, and body content.
- [ ] Return the most relevant chunks.
- [ ] Show a simple answer using matched content.
- [ ] Test with common questions about Max, awards, projects, and blog posts.

## Example Test Questions

- [ ] Who is Max Hoang?
- [ ] What projects has Max worked on?
- [ ] What awards has Max received?
- [ ] What AI projects are on this website?
- [ ] Where can I read about chatbot development?

## Output

- Basic non-AI retrieval works.
- The system can find relevant content.

---

# Phase 7: Add AI API Connection

## Goal

Connect the chatbot to an AI model so it can generate natural answers from retrieved Markdown content.

## Possible Providers

- [ ] OpenRouter
- [ ] OpenAI API
- [ ] DeepSeek API through OpenRouter
- [ ] Other low-cost LLM provider

## Tasks

- [ ] Create a secure server-side API route for chat.
- [ ] Store API key in environment variables.
- [ ] Never expose the API key to the browser.
- [ ] Send the user question to the backend.
- [ ] Use the retriever interface to retrieve relevant Markdown chunks.
- [ ] Send only relevant chunks to the AI model.
- [ ] Ask the model to answer only based on the provided context.
- [ ] Return the answer to the chatbot UI.

## Output

- The chatbot can generate natural answers.
- The answer is based on website content.
- The chat API remains storage-independent.

---

# Phase 8: Add Embeddings in JSON First

## Goal

Improve retrieval quality using embeddings while still avoiding database complexity at the beginning.

## Tasks

- [ ] Create `src/lib/chatbot/embedder.ts`.
- [ ] Choose an embedding provider.
- [ ] Generate embeddings for each Markdown chunk.
- [ ] Save embeddings to `data/chatbot-embeddings.json`.
- [ ] Update `json-retriever.ts` to support semantic search.
- [ ] Compare user question embedding against stored chunk embeddings.
- [ ] Return the top matching chunks.
- [ ] Keep the embedding data structure compatible with Supabase `pgvector`.

## Output

- The chatbot can search semantically using local JSON embeddings.
- The system is closer to production RAG without needing Supabase yet.

---

# Phase 9: Prepare Supabase Upgrade Layer

## Goal

Prepare the codebase so Supabase can be added later without rewriting the chatbot.

## Tasks

- [ ] Create `src/lib/chatbot/retrievers/supabase-retriever.ts` as a placeholder.
- [ ] Create `scripts/upload-chatbot-index-to-supabase.ts` as a placeholder.
- [ ] Document the Supabase table schema.
- [ ] Keep chunk IDs stable so rows can be inserted or updated.
- [ ] Use environment variables for future Supabase URL and service key.
- [ ] Do not connect Supabase until the JSON version works.

## Future Supabase Environment Variables

```env
NEXT_PUBLIC_SUPABASE_URL=
SUPABASE_SERVICE_ROLE_KEY=
OPENAI_API_KEY=
OPENROUTER_API_KEY=
```

## Output

- Supabase migration path is ready.
- Version 1 can stay simple while Version 3 is planned properly.

---

# Phase 10: Add RAG Behaviour

## Goal

Use Retrieval-Augmented Generation properly.

## Tasks

- [ ] Retrieve relevant chunks before answering.
- [ ] Limit the number of chunks sent to the model.
- [ ] Include source title and source URL in the context.
- [ ] Generate answers using only retrieved context.
- [ ] Include source titles or links when possible.
- [ ] Use fallback response if retrieval confidence is low.

## Storage Options

- [ ] Local JSON for MVP.
- [ ] Local embeddings JSON for improved demo.
- [ ] Supabase with pgvector for production.
- [ ] Upstash Vector, Pinecone, or Chroma if needed later.

## Output

- The chatbot can answer accurately using website content.
- The RAG system is storage-agnostic.

---

# Phase 11: Add Safety and Fallback Rules

## Goal

Make the chatbot reliable and avoid unsupported answers.

## Tasks

- [ ] Add a system prompt with strict website-assistant behaviour.
- [ ] Tell the chatbot not to hallucinate.
- [ ] Tell the chatbot to answer only from provided content.
- [ ] Add fallback response for missing information.
- [ ] Add out-of-scope detection.
- [ ] Avoid giving medical, legal, or financial advice.
- [ ] Keep responses clear and professional.

## Example Fallback

I do not have enough information about that in Max's website content. I can help with questions about Max, his projects, awards, blog posts, skills, and portfolio instead.

## Output

- The chatbot gives safer and more honest answers.

---

# Phase 12: Add Website Navigation Support

## Goal

Help users move around the website.

## Tasks

- [ ] Add source links to answers.
- [ ] Suggest relevant blog posts or project pages.
- [ ] Guide users to awards, events, projects, or contact pages.
- [ ] Add quick suggestion buttons.
- [ ] Add common prompts such as:
  - Who is Max?
  - Show me Max's AI projects.
  - What awards has Max won?
  - How can I contact Max?

## Output

- The chatbot works as a website navigation assistant.

---

# Phase 13: Add Automatic Index Update Workflow

## Goal

Make sure the RAG system updates when website Markdown content changes.

## Option A: Build-Time Update

- [ ] Run the indexing script during website build.
- [ ] Regenerate `chatbot-index.json` or embeddings before deployment.
- [ ] Use this for the simplest automated workflow.

## Option B: Manual Update Script

- [ ] Run `npm run index-chatbot-content` manually after content changes.
- [ ] Use this for early development and assignment demo.

## Option C: GitHub Action Update

- [ ] Trigger a GitHub Action when Markdown files change.
- [ ] Run the indexing script automatically.
- [ ] Later, upload the updated index to Supabase.

## Output

- The chatbot knowledge base can stay updated as the website content changes.

---

# Phase 14: Test the Chatbot

## Goal

Evaluate whether the chatbot meets the assignment and website goals.

## Test Categories

- [ ] Greeting test
- [ ] Personal profile question
- [ ] Project question
- [ ] Award question
- [ ] Blog content question
- [ ] Website navigation question
- [ ] Out-of-scope question
- [ ] Unknown information question

## Example Test Set

- [ ] Hello, who are you?
- [ ] Who is Max Hoang?
- [ ] What AI projects has Max built?
- [ ] What awards has Max received?
- [ ] What blog posts are about chatbot development?
- [ ] How can I contact Max?
- [ ] Can you give me medical advice?
- [ ] What is Max's favourite movie?

## Output

- Test results recorded.
- Strengths and weaknesses identified.

---

# Phase 15: Prepare Assignment Demonstration

## Goal

Prepare the chatbot for live presentation.

## Tasks

- [ ] Prepare a short intro about the chatbot domain.
- [ ] Explain the challenge: helping users explore personal website content.
- [ ] Explain the approach: Markdown content plus retrieval plus AI response.
- [ ] Explain the upgradeable architecture: JSON first, Supabase later.
- [ ] Show live chatbot testing.
- [ ] Show fallback behaviour.
- [ ] Explain limitations.
- [ ] Explain future improvements.

## Demo Questions

- [ ] Who is Max Hoang?
- [ ] What AI projects are shown on this website?
- [ ] What awards has Max won?
- [ ] Where can I find blog posts about chatbot development?
- [ ] Can you answer questions outside Max's website?

## Output

- Presentation demo is ready.

---

# Phase 16: Deploy and Monitor

## Goal

Deploy the chatbot safely on the live website.

## Tasks

- [ ] Test locally.
- [ ] Test on preview deployment.
- [ ] Check mobile responsiveness.
- [ ] Check API key security.
- [ ] Check response speed.
- [ ] Check usage cost.
- [ ] Deploy to production.
- [ ] Monitor errors and user questions.

## Output

- Chatbot is live on `maxhoang.com.au`.

---

# Minimum Viable Product Checklist

The MVP should include:

- [ ] Floating chatbot button.
- [ ] Chat window UI.
- [ ] User input and assistant response display.
- [ ] Markdown content loading.
- [ ] `ChatbotChunk` shared type.
- [ ] `Retriever` interface.
- [ ] JSON retriever.
- [ ] Basic retrieval from website content.
- [ ] AI-generated answer based on retrieved content.
- [ ] Fallback response.
- [ ] Simple testing evidence.

---

# Supabase-Ready Checklist

Even before using Supabase, the project should include:

- [ ] Stable chunk IDs.
- [ ] Supabase-style metadata fields.
- [ ] Storage-independent retriever interface.
- [ ] JSON retriever separated from chat API.
- [ ] Placeholder Supabase retriever file.
- [ ] Placeholder Supabase upload script.
- [ ] Documented Supabase table schema.
- [ ] Environment variable plan.
- [ ] Clear update workflow for regenerated RAG indexes.

---

# Recommended First Build Order

1. Build the chatbot UI only.
2. Create a local content index from Markdown files.
3. Add shared types and retriever interface.
4. Add JSON retriever.
5. Add simple keyword search.
6. Add API route for chatbot response.
7. Connect OpenRouter or OpenAI.
8. Add local embeddings JSON.
9. Add placeholder Supabase retriever and upload script.
10. Add source links and website navigation support.
11. Test and prepare the assignment demo.
12. Move to Supabase after the JSON version works.

---

# Notes for Codex

- Do not break the existing website structure.
- Ask before changing shared layout files.
- Keep chatbot code modular.
- Start with UI only if API keys are not available.
- Use environment variables for API keys.
- Do not expose API keys in frontend code.
- Keep the chatbot small and simple for the first version.
- Prefer readable code over complex architecture.
- Add comments where helpful for a beginner developer.
- Keep JSON storage isolated inside `json-retriever.ts`.
- Keep Supabase logic isolated inside `supabase-retriever.ts`.
- The chat API should only call the retriever interface.

## Related Notes

- [[personal-chatbot-index]]
- [[expert-chatbot-assignment-requirements]]
- [[personal-portfolio-chatbot-brief]]
