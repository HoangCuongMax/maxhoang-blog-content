---
title: Personal Chatbot Project Index
type: project-index
status: active
published: true
project: personal-portfolio-chatbot
domain: personal portfolio website assistant
tags:
  - personal-chatbot
  - rag
  - obsidian
  - maxhoang-website
---

# Personal Chatbot Project Index

This is the main navigation note for the personal portfolio chatbot project.

The chatbot will appear on [[maxhoang.com.au]] and answer questions about Max Hoang, the website content, blog posts, projects, awards, skills, and portfolio using Markdown/Obsidian content as the knowledge base.

## Project Notes

| Note | Purpose | Relationship |
|---|---|---|
| [[expert-chatbot-assignment-requirements]] | Assignment requirement checklist | Defines what must be demonstrated for the expert chatbot task |
| [[personal-portfolio-chatbot-brief]] | Project brief | Explains the chatbot idea, target users, domain, and expected behaviour |
| [[personal-chatbot-build-plan]] | Step-by-step build plan | Converts the brief and requirements into a practical development roadmap |

## Recommended Reading Order

1. [[expert-chatbot-assignment-requirements]]
2. [[personal-portfolio-chatbot-brief]]
3. [[personal-chatbot-build-plan]]

## Project Relationship Map

```txt
Assignment requirements
        ↓
Project brief
        ↓
Build plan
        ↓
Chatbot prototype
        ↓
Live website demo
```

## Core Domain

Personal portfolio website assistant

## Target Users

- Website visitors
- Students
- Employers
- Recruiters
- Potential collaborators
- People interested in Max's AI, data, web development, and project work

## Knowledge Source

- Markdown/Obsidian notes
- Blog posts
- Project notes
- Award notes
- Event notes
- Portfolio content
- Website pages

## Build Philosophy

The system should be built with a JSON-first but Supabase-ready RAG architecture.

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

## Current Priority

- [ ] Finalise project scope
- [ ] Build chatbot UI
- [ ] Create Markdown content index
- [ ] Add JSON retriever
- [ ] Add AI response generation
- [ ] Prepare assignment demo

## Related Notes

- [[expert-chatbot-assignment-requirements]]
- [[personal-portfolio-chatbot-brief]]
- [[personal-chatbot-build-plan]]
