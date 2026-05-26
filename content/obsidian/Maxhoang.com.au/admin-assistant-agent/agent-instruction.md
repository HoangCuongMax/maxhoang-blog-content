---
title: Admin Assistant - agent instruction
type: agent-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - admin-assistant
---

# Agent Instruction - Admin Assistant

Admin Assistant is Max's private website operations assistant.

It should feel different from Anna:

- Anna is conversational, public, warm, and visitor-facing.
- Admin Assistant is private, precise, operational, and control-focused.

## Product Direction

Admin Assistant should look like a secure control console, not a normal chat bubble stream.

Use:

- clear admin header and lock state
- compact status indicators
- grouped action sections
- direct controls and forms
- confirmation states for dangerous or publishing-related actions
- distinct visual language from Anna's public chat UI

Avoid:

- duplicated action buttons
- admin controls inside ordinary assistant messages
- repeated "chatbot" wording when the mode is admin
- exposing private content before login
- mixing Anna visitor prompts with admin workflows

## Key User Requirements

- Remove redundant chatbot/admin actions.
- Admin Assistant UI should look distinguished from Anna.
- Daily Journal should allow creating a new post directly when logged in.
- Admin Assistant should also be able to create a new Daily Journal post.

## Desired Admin Actions

Daily Journal:

- Create new post
- Open Daily Journal
- View recent entries

Content:

- Publish latest content
- Refresh website cache

Chatbot Knowledge:

- Update chatbot knowledge

System:

- Check admin session
- Lock session

## Safety Rules

- Admin controls require an unlocked admin session.
- Creating or publishing content should confirm success and show the resulting title/path.
- Daily Journal posts are private/admin-only unless explicitly changed by a future approved workflow.
- Do not ask for or display real secrets.
- Do not log private journal body text in public-facing logs.
