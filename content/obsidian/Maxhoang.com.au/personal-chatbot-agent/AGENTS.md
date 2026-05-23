---
title: Anna chatbot - agents router
type: agents-router
status: active
published: false
project: personal-portfolio-chatbot
tags:
  - personal-chatbot
  - anna-assistant
---

# AGENTS - Personal chatbot (Anna)

**Parent agent:** `../AGENTS.md` (MaxHoang.com.au website agent)

**Start every session** about the Max Hoang Journal website chatbot by reading these notes **in order**:

1. **`../AGENTS.md`** - Website-wide rules and parent reporting.
2. **`agent-instruction.md`** - Persona, behaviour, safety, and what "good" looks like for Anna.
3. **`memory.md`** - Repos, paths, architecture, pipeline, and stable facts about the implementation.
4. **`work-instruction.md`** - Commands, env, Git workflow, indexing, verification, and how to log work.

For Anna's long-term personality system and memory architecture, also read:

5. **`anna-brain-architecture/README.md`** - Digital personality system plan, memory layers, and implementation roadmap entry points.

## Website code structure to know

The runnable website app is the **MaxHoang_Notion** Next.js repo, not this Obsidian folder. For chatbot work, assume this app structure:

| Area | Path | What to check |
|---|---|---|
| App routes | `MaxHoang_Notion/app/` | Next.js App Router pages, layouts, API routes, and route metadata. |
| Chat API | `MaxHoang_Notion/app/api/chat/route.ts` | Request handling, direct greeting/contact answers, fallback responses, source payloads, and retriever wiring. |
| Chat completion | `MaxHoang_Notion/lib/chatbot/chat-completion.ts` | Anna system prompt, answer rules, OpenAI chat request, context formatting, and output limits. |
| Retriever contract | `MaxHoang_Notion/lib/chatbot/retriever.ts` | Storage-agnostic search interface used by the API route. |
| JSON retriever | `MaxHoang_Notion/lib/chatbot/retrievers/json-retriever.ts` | Local embedding index loading, query embeddings, cosine search, result scoring, and minimum score threshold. |
| Embeddings | `MaxHoang_Notion/lib/chatbot/embedder.ts` | OpenAI embedding calls and embedding model configuration. |
| Chatbot types | `MaxHoang_Notion/lib/chatbot/types.ts` | Shared chunk, index, and search result shapes. |
| Chat UI shell | `MaxHoang_Notion/components/chatbot/ChatbotWindow.tsx` | Conversation flow, welcome/name steps, quick prompts, message submission, loading/error states, and window layout. |
| Messages and sources | `MaxHoang_Notion/components/chatbot/ChatMessage.tsx` | Assistant/user bubble rendering and source button display. |
| Input | `MaxHoang_Notion/components/chatbot/ChatInput.tsx` | User text entry, submit controls, and input accessibility. |
| Launcher/widget | `MaxHoang_Notion/components/chatbot/ChatbotWidget.tsx` | Floating launcher, intro bubble, open/close behaviour, and reduced-motion handling. |
| Avatar | `MaxHoang_Notion/components/chatbot/AnnaAvatar.tsx` | Anna avatar image variants and rendering. |
| Indexer script | `MaxHoang_Notion/scripts/index-chatbot-content.mjs` | Published content discovery, exclusions, chunking, source URLs, metadata, and embedding generation. |
| Generated index | `MaxHoang_Notion/data/chatbot-embeddings.json` | Generated RAG chunks and embeddings used by the local JSON retriever. |
| Global styling | `MaxHoang_Notion/app/globals.css` | Theme tokens and chatbot surface/message styling. |
| Package commands | `MaxHoang_Notion/package.json` | `dev`, `lint`, `build`, `typecheck`, and `index-chatbot-content` scripts. |

## Content structure to know

The content source is the **maxhoang-blog-content** repo:

| Area | Path | What to check |
|---|---|---|
| Blog posts | `maxhoang-blog-content/content/posts/` | Published post Markdown used by the site and chatbot index. |
| Awards | `maxhoang-blog-content/content/awards/` | Public awards and recognition content. |
| Events | `maxhoang-blog-content/content/events/` | Public event entries. |
| Obsidian notes | `maxhoang-blog-content/content/obsidian/` | Notes and internal docs; only published/public material should be indexed. |
| Website agent docs | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/` | Website-wide agent instructions, memory, workflow, and work log. |
| Chatbot agent docs | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/personal-chatbot-agent/` | Anna-specific instructions, answer rules, workflow, memory, and work log. |
| Anna brain architecture | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/personal-chatbot-agent/anna-brain-architecture/` | Personality bible, conversation dictionary, dialogue examples, mood states, and future memory architecture plan. |
| Markdown brain plan | `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/personal-chatbot-agent/anna-brain-architecture/markdown-brain-structure.md` | Proposed content/personality/memory/training folder structure and human-reviewed learning loop. |
| Active markdown brain | `maxhoang-blog-content/markdown-brain/` | Approved Anna brain files used by runtime personality loading and future embedding retrieval. |

## Chatbot change checklist

- For answer behaviour, check `chatbot-answer-rules.md`, then update `MaxHoang_Notion/lib/chatbot/chat-completion.ts` or `MaxHoang_Notion/app/api/chat/route.ts`.
- For retrieval or content coverage, check `scripts/index-chatbot-content.mjs`, `lib/chatbot/retrievers/json-retriever.ts`, and `data/chatbot-embeddings.json`.
- For visible chatbot experience, check `components/chatbot/*` and `app/globals.css`.
- For personality memory, relationship memory, mood states, or future Anna brain architecture, check `anna-brain-architecture/*` as well as `agent-instruction.md` and `chatbot-answer-rules.md`.
- For active Anna brain content, edit `maxhoang-blog-content/markdown-brain/*`, then update docs/logs and regenerate embeddings when Node/OpenAI tooling is available.
- For learning or memory updates, preserve the rule: Anna can record conversation logs automatically, but only Max can approve changes to Anna's Markdown memory.
- For content-only changes, check frontmatter and publishing rules before regenerating embeddings.
- After content or indexing changes, run `npm run index-chatbot-content` from `MaxHoang_Notion` when Node tooling is available.

## Current UI and personality improvement plan

Anna's current implementation should preserve this product direction:

- Keep the chat stream clean: the scroll area should show only user and assistant messages.
- Move `Sources`, `Continue`, and `Feedback` into one compact footer action area above the input.
- Collapse `Sources` behind a button in the footer action area, with an option to expand and show source links.
- Move `Continue` suggestions into the same footer action area so suggested next steps do not consume message space.
- Keep the current feedback visual style, but show it contextually instead of all the time. Show it after roughly 3 to 5 assistant answers, hide it after a rating/correction, and hide it when the user continues without rating.
- On desktop, make the open chatbot a right-side overlay sidebar that sticks to the right edge and uses the full viewport height. Keep mobile behaviour compact/fullscreen as appropriate.
- Make Anna feel like a real digital assistant, not a website search widget. She should be warm, observant, curious, slightly playful, confident, proactive, and calm.
- Position Anna as a smart studio assistant, portfolio guide, research assistant, and creative AI collaborator.
- Replace software-like identity copy such as "Professional guide to posts, notes..." with warmer positioning such as "Your guide through Max's AI lab, projects, notes, and experiments" or "Part assistant, part researcher, part creative collaborator."
- Rotate natural welcome messages instead of repeating one robotic greeting. Examples: "Hey, I'm Anna. I can help you explore Max's AI projects, experiments, blog posts, and ideas. What are you curious about?" and "Looking for a project, blog post, or AI experiment? I probably know where it is."
- Add human behaviours: acknowledge, react, guide, suggest, remember session context, and continue conversations naturally.
- Make Anna proactive. If a visitor asks for a website, service, project, or career context, Anna should ask a useful follow-up and offer relevant paths through Max's work.
- Use small emotional cues where appropriate: "I found something useful", "This one might interest you", "That project is actually pretty interesting", "Max is actively improving this one."
- Use session memory to adapt to visitor type when possible: recruiter, client, student, developer, collaborator, or general visitor.
- Improve suggested questions so they feel conversational: "Show me AI projects", "What services does Max offer?", "Can Max build custom AI chatbots?", "What is he currently studying?", "Show award-winning projects", "Find beginner AI blogs", "Explain his WebGIS framework."
- Add tasteful thinking/status behaviour: "Let me think...", "Searching Max's notes...", "I found a few relevant things", "Comparing projects..." and rotating status labels like "online", "reading notes", "thinking", "exploring projects", "building ideas", "available now."
- Consider conversation modes for visitor intent: recruiter mode, client mode, student mode, and developer mode.
- Avoid search-like wording. Prefer "I found a few things that match what you're looking for" over "Here are 3 blog posts"; prefer "I couldn't find an exact match, but these might help" over "No results found"; prefer "Could you tell me a little more about what you mean?" over "Please clarify."
- Do not let Anna introduce herself repeatedly after the first welcome unless the visitor asks who she is.
- Answer greetings, identity questions, and basic help questions directly before retrieval.
- Only show search/thinking prefaces when Anna is actually searching Max's content.
- In minimized mode, hovering or focusing the message bubble reveals an inline quick-chat input instead of opening the full chatbot. The input auto-hides when the visitor stops hovering/focusing the minimized widget. There is no pencil button. Anna's avatar should stay large and stable while chatting. Mini answers should be short, direct, and opening full chat after mini chat should preserve the mini conversation.

Implementation priority:

1. Move `Sources`, `Continue`, and `Feedback` into the bottom action area.
2. Update visible copy, welcome messages, status text, and suggested questions.
3. Strengthen the system prompt and answer rules for personality, proactive guidance, and non-search wording.
4. Add session visitor-mode detection and adaptive follow-up behaviour.
5. Add subtle liveliness polish such as typing animation, blinking cursor, live status changes, avatar movement, hover reactions, and dynamic background glow while respecting reduced motion.

## Documentation sync rule

Any meaningful chatbot change must update the relevant files in this `personal-chatbot-agent` folder during the same work session:

- Update **`AGENTS.md`** when routing, entry points, file maps, current product direction, or cross-file rules change.
- Update **`agent-instruction.md`** when Anna's persona, tone, behaviour, safety rules, conversation modes, or quality bar changes.
- Update **`chatbot-answer-rules.md`** when answer style, fallback wording, grounding rules, proactive guidance, or system-prompt behaviour changes.
- Update **`memory.md`** when app paths, architecture, data flow, implementation details, environment assumptions, or stable facts change.
- Update **`work-instruction.md`** when commands, verification steps, workflow, indexing, deployment, or logging rules change.
- Update **`work-log.md`** with a dated one-liner whenever chatbot code, content, docs, behaviour, UI, or workflow changes.
- Add a short parent entry to **`../work-log.md`** when chatbot work changes website behaviour, app implementation, workflow, or agent structure.

Do not leave the agent docs stale after editing chatbot code. Before finishing, scan this folder and update every file whose instructions, memory, or workflow are affected by the change.

This folder lives under the content vault: `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/personal-chatbot-agent`. The runnable app is **not** here; it is in the **MaxHoang_Notion** Next.js repo (see `memory.md`).
