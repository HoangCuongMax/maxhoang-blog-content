---
title: Personal Portfolio Website Assistant Chatbot Brief
type: project-brief
status: active
published: true
project: personal-portfolio-chatbot
domain: personal portfolio website assistant
website: https://maxhoang.com.au
tags:
  - personal-chatbot
  - portfolio-assistant
  - rag
  - maxhoang-website
---

# Personal Portfolio Website Assistant Chatbot Brief

## Navigation

- Project index: [[personal-chatbot-index]]
- Assignment requirements: [[expert-chatbot-assignment-requirements]]
- Build plan: [[personal-chatbot-build-plan]]

## Relationship to Project

This note translates the assignment requirements from [[expert-chatbot-assignment-requirements]] into a specific chatbot idea for `maxhoang.com.au`. The implementation steps are planned in [[personal-chatbot-build-plan]].

## Project Title

Personal Portfolio Website Assistant Chatbot

## Website

https://maxhoang.com.au

## Domain

Personal portfolio website assistant

## Project Summary

This chatbot will be displayed on my personal website, `maxhoang.com.au`. It will act as an intelligent website assistant that reads all my blog post content written in Markdown/Obsidian format and answers questions based on that content.

The chatbot is designed to help visitors understand who I am, what I do, what projects I have built, what awards I have received, and what knowledge or experience I have shared through my website content.

It is also a practical showcase of my chatbot development skills. Instead of being only a general chatbot, it will demonstrate how a domain-specific chatbot can use website content as a knowledge base to support navigation, personal branding, and interactive information retrieval.

## Purpose

The main purposes of this chatbot are:

- To showcase my chatbot development work.
- To help website visitors navigate my personal website.
- To answer questions about me using my own blog and website content.
- To provide a more interactive experience for students, visitors, and employers.
- To demonstrate how Markdown/Obsidian content can become a chatbot knowledge base.

## Target Users

The chatbot is designed for:

- Website visitors
- Students
- Employers
- Recruiters
- Potential collaborators
- People interested in my AI, data, web development, and project work

## Knowledge Source

The chatbot will use my website content as its main knowledge source.

Main content source:

- Markdown files from my Obsidian-based blog content repository
- Blog posts
- Project notes
- Award notes
- Event notes
- Portfolio content
- Website-related Markdown content

The chatbot should answer only based on available website and Markdown content. If the information is not available, it should say that it does not have enough information instead of guessing.

This knowledge source connects directly to the RAG update workflow in [[personal-chatbot-build-plan]].

## Main Use Cases

The chatbot should be able to help users with questions such as:

- Who is Max Hoang?
- What projects has Max worked on?
- What awards has Max received?
- What is Max studying?
- What AI or data projects are shown on the website?
- Where can I find blog posts about AI, web development, or chatbot development?
- What is Max's experience in AI, data analytics, marketing, and web development?
- How can I contact Max?
- What content is available on the website?

## Functional Requirements

These functional requirements come from [[expert-chatbot-assignment-requirements]] and are implemented step by step in [[personal-chatbot-build-plan]].

- [ ] The chatbot answers questions related to the selected domain.
- [ ] The chatbot outputs clear sentence-level answers.
- [ ] The chatbot can handle simple greetings and casual conversation.
- [ ] The chatbot can recognise when a question is outside its domain.
- [ ] The chatbot can provide a fallback response when it does not know the answer.
- [ ] The chatbot avoids hallucinating unsupported answers.
- [ ] The chatbot provides useful and user-friendly responses.
- [ ] The chatbot helps users navigate the website.
- [ ] The chatbot can summarise relevant blog posts or website sections.
- [ ] The chatbot can guide users to related content when available.

## Expected Chatbot Behaviour

The chatbot should be friendly, clear, and professional. It should answer like a helpful website assistant, not like a random general chatbot.

The chatbot should:

- Give direct answers.
- Use simple and clear language.
- Keep answers short unless the user asks for detail.
- Refer to relevant website content when possible.
- Be honest when information is missing.
- Avoid making claims that are not supported by the content.
- Help the user find the right page, post, or project.

## Conversation Handling

The chatbot should be able to handle simple conversations, including:

- Greetings
- Thank you messages
- Simple follow-up questions
- Clarification questions
- Questions about the website
- Questions about Max's background, projects, skills, awards, and blog content

Example greeting response:

> Hi, I am Max's website assistant. I can help you learn about Max, his projects, awards, blog posts, and AI development journey.

## Out-of-Scope Handling

The chatbot should recognise when a question is outside the personal portfolio website domain.

Out-of-scope examples:

- Medical advice
- Legal advice
- Financial advice
- Questions unrelated to Max or the website content
- Unsupported personal information
- Information not available in the Markdown knowledge base

Example fallback response:

> I do not have enough information about that in Max's website content. I can help with questions about Max, his projects, blog posts, awards, skills, and portfolio instead.

## Development Approach

The preferred approach is a retrieval-based or RAG chatbot.

The technical implementation is planned in [[personal-chatbot-build-plan]]. The preferred architecture is JSON-first but Supabase-ready, so the first working version can stay simple while still allowing a future production upgrade.

Possible pipeline:

1. Read Markdown files from the Obsidian/blog content repository.
2. Extract title, headings, tags, metadata, and body content.
3. Split content into small searchable chunks.
4. Create embeddings for each chunk.
5. Store embeddings first in JSON, then later in Supabase if needed.
6. Retrieve relevant chunks when a user asks a question.
7. Generate an answer based only on retrieved content.
8. Return a clear and helpful response in the website chatbot UI.

## Possible Technology Stack

- Next.js website frontend
- Markdown/MDX content source
- Obsidian notes as content management system
- OpenRouter or OpenAI API for chatbot response generation
- JSON index for the first version
- Supabase with pgvector for future production RAG
- Embedding model for semantic search
- Small chatbot widget UI using shadcn components

## Success Criteria

The chatbot will be successful if it can:

- Answer common questions about Max and his website.
- Help users find relevant website content.
- Demonstrate chatbot development skills.
- Use Markdown content as a reliable knowledge base.
- Avoid unsupported or hallucinated answers.
- Provide a smooth and useful visitor experience.

## Presentation/Demo Focus

During the assignment presentation, this chatbot can be demonstrated as an expert chatbot for the domain of personal portfolio website assistance.

The demo can show:

- A visitor asking who Max is.
- A student asking about Max's AI projects.
- An employer asking about Max's skills and awards.
- A visitor asking where to find chatbot-related blog posts.
- An out-of-scope question to show fallback handling.

## Future Improvements

These improvements connect to the later phases in [[personal-chatbot-build-plan]].

- [ ] Add source links to the exact blog posts used in each answer.
- [ ] Add memory for follow-up questions.
- [ ] Add multilingual support, especially English and Vietnamese.
- [ ] Add analytics to see what visitors ask most often.
- [ ] Add better filtering by topic, tag, or project type.
- [ ] Add automatic content updates when new Obsidian notes are pushed to GitHub.
- [ ] Add Supabase vector storage for production.
- [ ] Add voice input or voice response in the future.

## Related Notes

- [[personal-chatbot-index]]
- [[expert-chatbot-assignment-requirements]]
- [[personal-chatbot-build-plan]]
