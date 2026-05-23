---
title: Anna chatbot — work instruction
type: work-instruction
status: active
published: false
project: personal-portfolio-chatbot
tags:
  - personal-chatbot
  - workflow
---

# Work instruction — Anna chatbot

Use this note when **developing**, **debugging**, **shipping**, or **updating embeddings**. Behaviour rules live in **`agent-instruction.md`**. Facts and paths live in **`memory.md`**. Website-wide coordination lives in **`../AGENTS.md`**.

## 1. Where to work

- **Application code:** clone / open **`MaxHoang_Notion`** (see `memory.md` for path).
- **Markdown content:** **`maxhoang-blog-content`** repo, under `content/`.
- **Anna markdown brain:** **`maxhoang-blog-content/markdown-brain`** for approved personality, relationship, and training memory.
- **Website agent docs:** `maxhoang-blog-content/content/obsidian/Maxhoang.com.au`
- **Chatbot agent docs (this folder):** `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/personal-chatbot-agent` — edit when chatbot behaviour or workflow changes.

## 2. Daily commands (from `MaxHoang_Notion`)

```bash
npm install          # if needed
npm run dev          # local site + chatbot
npm run lint
npm run build
npm run index-chatbot-content   # regenerate embeddings after content or indexer changes
```

After **content** or **indexing logic** changes, run **`npm run index-chatbot-content`** before trusting search results locally or in preview.

## 3. Git workflow (two repos)

| Change type | Repo to commit |
|-------------|----------------|
| Blog posts, obsidian notes, awards, events, **content** only | **maxhoang-blog-content** |
| Chatbot UI, API, `lib/chatbot/*`, scripts, **`data/chatbot-embeddings.json`** | **MaxHoang_Notion** |

Typical sequence:

1. Pull latest in **both** repos.
2. Edit Markdown in **maxhoang-blog-content** (respect `published` / site rules).
3. In **MaxHoang_Notion**: `npm run index-chatbot-content` → verify `data/chatbot-embeddings.json`.
4. `npm run lint` && `npm run build`.
5. Push **content** repo, then push **app** repo (or one PR each).

Do **not** commit `.env` files with real secrets.

## 4. Verification checklist (before merge / deploy)

- [ ] `OPENAI_API_KEY` set locally for full RAG test (optional for pure UI tweaks).
- [ ] `npm run index-chatbot-content` if content or indexer changed.
- [ ] `npm run index-chatbot-content` if approved `markdown-brain` files changed and should be embedded.
- [ ] `npm run lint` clean.
- [ ] `npm run build` succeeds.
- [ ] Spot-check prompts from **`agent-instruction.md`** (greeting, domain question, out-of-scope).

## 5. Work log

Whenever you (or an agent) **ship a meaningful change** to the chatbot or this docs set:

1. Open **`work-log.md`**.
2. Add a **dated** bullet (one line or short cluster).
3. Add a short parent entry to **`../work-log.md`** when the work changes website behaviour, app implementation, workflow, or agent structure.
4. Keep it factual: *what* changed, *where* (repo/path if useful).

Do not paste secrets or full API keys into the log.

## 6. Documentation sync

- **`agent-instruction.md`** — persona, rules, tests, safety. Update when product behaviour changes.
- **`chatbot-answer-rules.md`** — answer style, fallback wording, grounding details, proactive guidance, and system-prompt behaviour. Update when Anna's conversation style changes.
- **`memory.md`** — repos, paths, pipeline, file map, architecture. Update when implementation or locations change.
- **`work-instruction.md`** — commands, Git, checklists. Update when workflow or tooling changes.
- **`AGENTS.md`** — router, entry points, file maps, current product direction, and cross-file rules. Update when future agents need different starting context.
- **`work-log.md`** — dated one-liners. Update whenever chatbot code, content, docs, behaviour, UI, or workflow changes.

Before finishing a chatbot change, scan this folder and update every affected file. Do not leave agent docs stale after editing chatbot code.

## 7. Obsidian / publishing note

Files in this folder may use `published: false` so they are **internal planning** and not required on the public site. If you add a note that must appear on the web, follow your normal vault frontmatter rules.
