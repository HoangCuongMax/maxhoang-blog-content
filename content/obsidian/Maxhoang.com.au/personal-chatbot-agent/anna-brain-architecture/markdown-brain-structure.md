---
title: Anna markdown brain structure
type: architecture-plan
status: active
published: false
project: personal-portfolio-chatbot
tags:
  - personal-chatbot
  - anna-assistant
  - markdown-brain
  - memory-architecture
---

# Markdown Brain Structure

The content repo should become Anna's brain.

Start with a human-reviewed Markdown memory system, not fully automatic learning. Anna can record conversations automatically, but only Max should approve changes to Anna's memory.

## Current implementation

The first working version now lives at the content repo root:

```txt
maxhoang-blog-content/markdown-brain/
```

The app supports this in two ways:

- `MaxHoang_Notion/lib/chatbot/personality-memory.ts` loads approved Anna personality, relationship, and training notes at runtime when the folder is available.
- `MaxHoang_Notion/scripts/index-chatbot-content.mjs` can include `markdown-brain` files in `data/chatbot-embeddings.json` with `memoryLayer` metadata.

The chat API keeps personality memory separate from factual website sources, so Anna can use the brain for style and behaviour without showing personality docs as public source buttons.

## Recommended Structure

```txt
markdown-brain/
  content/
    projects/
    blog-posts/
    services/
    awards/

  anna/
    identity.md
    personality.md
    speaking-style.md
    behaviour-rules.md
    boundaries.md
    conversation-examples.md
    human-dictionary.md

  memory/
    visitor-types.md
    common-questions.md
    good-responses.md
    bad-responses.md
    improvement-log.md

  training/
    reviewed-conversations/
    approved-patterns.md
    rewrite-rules.md
```

This structure has been created with starter approved memory files.

## How The Chatbot Works

```txt
Visitor question
  -> Next.js API route
  -> search markdown-brain content
  -> retrieve relevant knowledge chunks
  -> retrieve Anna personality rules
  -> retrieve session conversation memory
  -> send all context to OpenRouter / OpenAI model
  -> Anna answers in her personality
  -> save conversation log
```

The response should be built from three ingredients:

```txt
Answer = website knowledge + Anna personality + conversation memory
```

## How Anna Learns Over Time

Anna should not automatically rewrite her own approved memory at first. That can become messy and unsafe.

Use this safer workflow:

1. Visitor chats with Anna.
2. Save question, answer, sources, session context, and feedback.
3. Max reviews the logs weekly.
4. Mark each useful pattern:
   - good answer
   - bad answer
   - needs warmer tone
   - missing project link
   - too robotic
   - unsupported claim
5. Update the relevant `markdown-brain` files.
6. Re-run the embedding script.
7. Anna improves next time.

Current logging already saves chat and feedback records. The next improvement is a review helper that turns selected log patterns into files under `markdown-brain/memory/` or `markdown-brain/training/reviewed-conversations/`.

## Approval Rule

Anna can record conversations automatically, but only Max can approve changes to Anna's memory.

This gives:

- better quality
- safer answers
- less hallucination
- stronger personality over time
- cleaner long-term memory

## Example Improvement Log

```md
# Improvement Log

## 2026-05-23

Visitor asked:
"Can Max build an AI chatbot for my business?"

Anna answered too generally.

Better rule:
When visitors ask about services, Anna should:
1. confirm the need warmly
2. explain Max can help with AI chatbot UI, RAG, OpenRouter, Supabase, and website integration
3. show one related project
4. suggest contacting Max

Approved response:
"Yes - that's exactly the kind of system Max is building..."
```

## Human Dictionary Example

```md
# Anna Human Dictionary

Instead of:
"How may I assist you?"

Say:
"What are you trying to explore today?"

Instead of:
"No results found."

Say:
"I couldn't find an exact match, but I found something close."

Instead of:
"Please clarify."

Say:
"Can you tell me a little more so I can guide you properly?"
```
