---
title: Codex operating folder - work instruction
type: work-instruction
status: active
published: false
project: codex-operating-system
tags:
  - codex
  - workflow
  - skills
---

# Work instruction - Codex Operating Folder

## 1. Starting Rule

Before working on Codex skills, memory, or agent improvement, read:

1. `AGENTS.md`
2. `agent-instruction.md`
3. `memory.md`
4. `work-instruction.md`

## 2. Folder Rules

- Keep operating Markdown notes here `published: false`.
- Exclude copied skill bundle files under `skills/` from the `published: false` rule; they need skill frontmatter such as `name` and `description`.
- Keep private/internal notes in this `codex` folder, not in public course or website folders.
- Put real draft skills in `skills/<skill-name>/SKILL.md`.
- Put durable workflow memories in `memory/`.
- Put skill validation prompts and expected outcomes in `evaluations/`.
- Put large supporting docs in `references/`.
- Use `experiments/` for prototypes that are not yet stable skills.

## 3. Creating A Draft Skill

Use the system `skill-creator` guidance. Minimum structure:

```txt
skills/<skill-name>/
  SKILL.md
```

`SKILL.md` must include:

```yaml
---
name: skill-name
description: Clear trigger description for when Codex should use this skill.
---
```

Keep the body short. Add `references/`, `scripts/`, or `assets/` inside the skill only when they directly support the skill.

## 4. Updating Memory

Use both layers intentionally:

- Markdown memory in `memory/` for inspectable project knowledge.
- `agentmemory` save for concise stable facts that future Codex sessions should recall.

Good memory candidates:

- User preferences.
- Stable repo paths.
- Repeated workflows.
- Important architecture decisions.
- Known gotchas and validation checks.

Bad memory candidates:

- Secrets or credentials.
- One-off temporary status.
- Large logs.
- Speculation.

## 5. Validation

For skill or agent changes:

- Check frontmatter.
- Check `published: false` for operating notes outside `skills/`.
- Run `git diff --check`.
- Add a dated entry to `work-log.md`.

For installed skills, validate with realistic prompts before considering them stable.
