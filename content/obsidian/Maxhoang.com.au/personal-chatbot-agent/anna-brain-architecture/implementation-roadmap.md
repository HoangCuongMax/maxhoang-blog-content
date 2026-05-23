---
title: Anna brain implementation roadmap
type: implementation-roadmap
status: active
published: false
project: personal-portfolio-chatbot
tags:
  - personal-chatbot
  - anna-assistant
  - roadmap
---

# Implementation Roadmap

## Phase 1 - Personality bible

- Create and maintain Anna's core personality Markdown files.
- Keep `anna-core-personality.md` as the source of truth.
- Add dialogue examples whenever Anna's behaviour is refined.
- Update `chatbot-answer-rules.md` when these rules become live system behaviour.
- Define the future `markdown-brain/` folder structure for content, Anna personality, approved memory, and reviewed training examples.

Status: first version created in `maxhoang-blog-content/markdown-brain/`.

## Phase 2 - Prompt integration

- Load selected personality rules into the system prompt.
- Keep the prompt compact.
- Use only stable identity and behaviour rules in the always-on prompt.
- Keep detailed examples retrievable instead of stuffing everything into one prompt.

Status: first version implemented through `lib/chatbot/personality-memory.ts` and `lib/chatbot/chat-completion.ts`.

## Phase 3 - Personality retrieval

- Chunk and embed personality files separately from factual website content.
- Add metadata such as:
  - `memory_layer: personality`
  - `type: speech-style | behaviour | dialogue-example | emotional-reaction`
  - `mood: warm | focused | technical | playful | calm | excited`
- Retrieve relevant personality chunks before generating a response.

Status: indexer support added. Regenerate embeddings with `npm run index-chatbot-content` when Node and `OPENAI_API_KEY` are available.

## Phase 4 - Relationship memory

- Track session-level visitor context:
  - likely visitor type
  - interests
  - current goal
  - preferred depth
  - last useful source category
- Keep this transparent and lightweight.
- Do not store sensitive data.
- Do not let Anna automatically rewrite approved memory. Save logs and feedback, then let Max approve memory updates.

Status: chat logs and feedback logs are saved with review metadata; approved memory updates remain manual.

## Phase 4.5 - Human-reviewed learning loop

Use a weekly review workflow:

1. Save visitor question, Anna answer, sources, session context, and feedback.
2. Review the logs.
3. Mark answers as good, bad, too robotic, missing source, unsupported, or worth turning into a rule.
4. Update `markdown-brain/memory/`, `markdown-brain/anna/`, or `markdown-brain/training/`.
5. Re-run the embedding script.
6. Anna improves on the next deployment or index refresh.

## Phase 5 - Hidden interaction analysis

Before generation, compute an internal interaction state:

```json
{
  "user_type": "potential client",
  "tone": "curious",
  "goal": "exploring AI services",
  "best_behaviour": "warm + confident",
  "next_action": "guide toward projects"
}
```

Use this to choose personality context, not to make unsupported claims.

## Phase 6 - Humanizer pass

Add an optional final style pass that:

- removes robotic phrasing
- shortens long answers
- improves transitions
- adds one useful follow-up
- keeps facts grounded

The humanizer must not add new factual claims.

## Phase 7 - Vector store upgrade

Move from local JSON embeddings to a vector database when useful.

Candidates:

- Supabase pgvector
- ChromaDB
- Pinecone
- Weaviate

Keep the existing retriever interface so storage can change without rewriting the chat route or UI.
