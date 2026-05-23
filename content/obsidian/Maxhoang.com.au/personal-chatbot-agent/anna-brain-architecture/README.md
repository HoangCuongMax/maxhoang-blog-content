---
title: Anna brain architecture
type: architecture-plan
status: active
published: false
project: personal-portfolio-chatbot
tags:
  - personal-chatbot
  - anna-assistant
  - personality-system
---

# Anna Brain Architecture

This folder captures the plan for moving Anna from a chatbot UI into a digital personality system.

The goal is not only to make Anna answer questions. The goal is to make Anna feel like someone visitors can talk to: warm, observant, consistent, proactive, and aware of the conversation.

## Core idea

Anna should have three memory layers:

1. **Knowledge memory**
   - Facts from Max's public website content.
   - Blog posts, projects, notes, portfolio pages, services, awards, events, and FAQs.
   - Stored in embeddings / vector search.
   - Answers questions like: "What projects has Max built?"

2. **Personality memory**
   - Anna's identity, speaking style, emotional patterns, behaviour rules, vocabulary, humour level, pacing, and boundaries.
   - Stored as Markdown personality documents and later embedded for retrieval.
   - Keeps Anna from sounding like a search result.

3. **Relationship memory**
   - Session and future long-term memory about the visitor's current intent.
   - Visitor type, interests, favourite topics, ongoing discussion, and whether they seem like a recruiter, client, student, developer, collaborator, or casual visitor.
   - Makes Anna feel aware of the person she is helping.

## Best architecture

Use a hybrid system instead of one giant prompt:

```txt
Core system prompt
  + personality retrieval
  + relationship/session memory
  + knowledge retrieval
  + hidden interaction analysis
  + LLM generation
  + optional humanizer/style pass
  -> Anna response
```

This lets Anna stay grounded in facts while also keeping a consistent personality.

## Recommended stack direction

```txt
Obsidian notes
  -> chunking pipeline
  -> embedding pipeline
  -> Supabase pgvector or another vector store
  -> retrieval layer
  -> personality engine
  -> conversation engine
  -> OpenRouter / OpenAI LLM
  -> humanizer or style post-processor
  -> frontend UI
```

The existing JSON embedding system can stay while this is designed. The long-term architecture should keep the retriever interface storage-agnostic so personality memory can move to Supabase, pgvector, ChromaDB, Pinecone, Weaviate, or another vector store later.

## What makes Anna feel human

The human feeling should come mostly from:

- memory
- emotional consistency
- proactive guidance
- conversational rhythm
- personality persistence
- session awareness
- small imperfections and softer transitions

It should not depend only on avatar realism, animation, or visual effects.

## Folder map

- `anna-core-personality.md` - Anna's main identity, emotional framework, and relationship rules.
- `personality/identity.md` - who Anna is and is not.
- `personality/speech-style.md` - how Anna speaks.
- `personality/behaviour-rules.md` - how Anna reacts and guides.
- `personality/emotional-reactions.md` - tone shifts for user emotion and intent.
- `personality/relationship-style.md` - session memory and visitor relationship rules.
- `conversation-dictionary.md` - robotic-to-human phrasing replacements.
- `dialogue-examples.md` - example conversations that teach the personality by demonstration.
- `mood-states.md` - warm, focused, technical, playful, calm, and excited response modes.
- `markdown-brain-structure.md` - proposed repo folder structure and human-reviewed learning workflow.
- `implementation-roadmap.md` - phased build plan.

## Learning rule

Start with human-reviewed learning, not fully automatic memory rewriting.

Anna can record conversations automatically, but only Max can approve changes to Anna's memory. Approved changes should be written into Markdown files, embedded, and used in future retrieval.
