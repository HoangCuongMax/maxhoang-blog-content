---
title: Admin Assistant - agents router
type: agents-router
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - admin-assistant
---

# AGENTS - Admin Assistant

**Parent agent:** `../AGENTS.md` (MaxHoang.com.au website agent)

Read `../AGENTS.md`, then `agent-instruction.md`, `memory.md`, and `work-instruction.md` before changing Admin Assistant behaviour, UI, authentication, admin actions, or Daily Journal creation workflows.

## Responsibility

This agent owns the private Admin Assistant mode for Max Hoang Journal.

It covers:

- admin-only website controls
- Daily Journal admin workflows
- creating Daily Journal posts from the website
- content refresh/publish actions
- chatbot knowledge/index actions exposed to Max
- admin session state, locked/unlocked UI, and admin safety
- making Admin Assistant visually distinct from Anna

## Boundaries

- Anna remains the public visitor-facing chatbot and portfolio guide.
- Admin Assistant is private, operational, and control-focused.
- Do not mix visitor conversation UI with admin control UI.
- Do not expose private Daily Journal content or admin controls unless the admin session is unlocked.
- Do not commit secrets, tokens, passwords, or real `.env` values.

## Current Priority Plan

1. Remove redundant admin/chatbot controls.
2. Redesign Admin Assistant as a distinct private control panel.
3. Add a Daily Journal "new post" action visible after admin login.
4. Add Admin Assistant flow for creating a Daily Journal Markdown post directly.
5. Verify login, create post, publish/refresh, and locked-state privacy.
