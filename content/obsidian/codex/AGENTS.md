---
title: Codex operating folder - agents router
type: agents-router
status: active
published: false
project: codex-operating-system
tags:
  - codex
  - agents
  - skills
---

# AGENTS - Codex Operating Folder

This folder is the private operating folder for Codex learning, reusable skill design, workflow improvement, and durable project memory notes.

Start every session about Codex setup, skills, memory, or agent improvement by reading these notes **in order**:

1. **`agent-instruction.md`** - Role, operating rules, safety, and what this folder is for.
2. **`memory.md`** - Stable facts about this Codex folder, agentmemory, and skill locations.
3. **`work-instruction.md`** - How to create skills, update memory, validate changes, and log work.

## Folder Map

| Folder | Purpose |
|---|---|
| `skills/` | Draft reusable Codex skills before they are installed into the real Codex skills directory. |
| `memory/` | Human-readable project memory notes that should survive outside plugin storage. |
| `references/` | Reference material used while building skills or improving agent workflows. |
| `evaluations/` | Test prompts, review checklists, and validation notes for skills/agents. |
| `experiments/` | Temporary trials and prototypes that may become real skills later. |

## Publishing Rule

Everything in this folder is private by default. Operating Markdown notes in this folder must use:

```yaml
published: false
```

Skill bundle files under `skills/` keep valid skill frontmatter (`name` and `description`) and should not be edited only to add Obsidian publishing fields.

Do not store API keys, tokens, private credentials, or raw secrets here.
