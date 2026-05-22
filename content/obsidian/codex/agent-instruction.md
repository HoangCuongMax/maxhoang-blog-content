---
title: Codex operating folder - agent instruction
type: agent-instruction
status: active
published: false
project: codex-operating-system
tags:
  - codex
  - agents
  - skills
---

# Agent instruction - Codex Operating Folder

Use this folder to make Codex more effective over time for Max Hoang's website, content vault, skills, and automation workflows.

## Role

This is not public website content. It is a private working system for:

- Designing reusable Codex skills.
- Recording durable decisions and workflows.
- Improving agent instructions.
- Tracking recurring mistakes, fixes, and validation checks.
- Coordinating with the `agentmemory` plugin when explicit memory should be saved.

## Operating Rules

- Keep notes concise and actionable.
- Use `published: false` for operating notes in this folder.
- Keep copied skill bundles valid as skills; do not add Obsidian-only frontmatter to `skills/**/SKILL.md` unless deliberately promoting a different format.
- Do not store secrets, API keys, credentials, private tokens, or raw `.env` values.
- Prefer updating existing rules over creating duplicate documents.
- When creating an actual Codex skill, follow the system `skill-creator` guidance.
- Draft skills here first; install or copy them into `$CODEX_HOME/skills` only when the user asks.
- Do not claim automatic background learning. Codex can update this folder and agentmemory when it is active in a conversation.

## Memory Rules

- Use human-readable Markdown in `memory/` for project-level decisions that should be inspectable in Obsidian.
- Use the `agentmemory` plugin only for concise, useful long-term facts, preferences, workflows, or decisions.
- Save memory only when it is stable and likely to help future sessions.
- Never save private secrets or sensitive personal data.

## Skill Rules

- Each draft skill should live in `skills/<skill-name>/`.
- Each real skill must have a concise `SKILL.md` with YAML frontmatter containing `name` and `description`.
- Keep `SKILL.md` focused on core workflow. Put optional details in `references/`.
- Add scripts only when deterministic execution is better than rewriting the same code repeatedly.
- Add evaluations in `evaluations/` when a skill needs regression prompts or validation examples.
