---
title: Anna: How I Built My Personal AI Chatbot
slug: anna
published: true
date: 2026-05-24
featured: true
excerpt: A deep technical case study on Anna, my personal AI chatbot for Max Hoang Journal, including the motivation, UX, RAG pipeline, markdown brain, memory layers, admin workflow, safety rules, and lessons learned.
tags: [AI, Chatbot, RAG, Personal, Portfolio, Next.js, NLP]
coverImage: /blog-covers/anna.png
mediaAltText: "Generated cover for Anna"
---

Anna started as a small idea.

I wanted my website to feel less like a static portfolio and more like a living guide. A normal portfolio says, "Here are my projects, here are my posts, here is my contact page." That is useful, but it still leaves the visitor to do all the navigation work.

I wanted something different.

I wanted a visitor to be able to arrive on my website and simply ask:

- What AI projects has Max built?
- What is he currently learning?
- Can he build a custom chatbot?
- Where are his award-winning projects?
- What blog post should I read first?
- How can I contact him?

That became Anna.

Anna is my personal AI chatbot for Max Hoang Journal. She is not just a generic chatbot embedded into a website. She is a portfolio guide, a research assistant, a content navigator, a small conversational interface, and a controlled experiment in how far a personal website can become interactive.

This post explains why I built Anna, how I designed her personality, how the technical system works, how retrieval-augmented generation is used, how I created a markdown brain, how I protect factual accuracy, and what I learned from building a personal chatbot that sits inside a real website.

This is not a short announcement post. It is a full build note.

## The Problem With A Normal Portfolio Website

Most portfolio websites are passive.

They depend on the visitor knowing what they want before they arrive. If the visitor is a recruiter, they might look for work history. If the visitor is a client, they might look for services. If the visitor is a student, they might look for learning notes. If the visitor is a collaborator, they might look for projects.

But the website usually gives all of them the same navigation:

- Blog
- About
- Projects
- Contact

That is fine for a simple website, but it is not ideal when the content starts to grow.

My website includes blog posts, Obsidian notes, awards, events, GitHub projects, presentation slides, personal learning material, and AI experiments. The more content I added, the harder it became for a visitor to understand what mattered to them.

Search helps, but search is still not the same as guidance.

A search box expects the visitor to know the right keyword. A chatbot can ask, interpret, suggest, and recover. If someone asks "can Max help with AI automation?", the system should not require them to know which post contains "AI websites", "chatbot", "workflow", or "service improvement".

The goal was to make the website feel more like a helpful conversation.

## What Anna Is

Anna is a website assistant built into Max Hoang Journal.

Her job is to help visitors explore:

- my AI projects
- my blog posts
- my Obsidian notes
- my services
- my events
- my awards
- my contact paths
- my learning journey
- selected technical concepts, especially NLP and chatbot topics

Anna has two main modes:

1. Public Anna Assistant
2. Private Admin Assistant

The public assistant helps visitors find information and understand my work. The private admin mode is hidden behind an admin flow and gives me access to website controls such as refreshing content, updating tokenization, and creating Daily Journal posts.

This means Anna is both a public-facing assistant and a private website operations interface.

That dual role is one of the most interesting parts of the project.

## What Anna Is Not

It is also important to define what Anna is not.

Anna is not a fully autonomous agent that can do anything on the internet.

Anna is not allowed to invent private facts about me.

Anna is not meant to replace proper navigation.

Anna is not a human pretending to be a human.

Anna is not a chatbot that answers every question with confidence. If the system does not have enough information, it should say that. One of the most important design rules is that Anna should be helpful without pretending.

The core idea is controlled usefulness.

She can guide, search, summarize, suggest, and help. But for claims about me, my work, my awards, my services, dates, employers, and achievements, she should rely on website sources.

## Why I Named Her Anna

The original Anna post was personal and reflective. It was about presence, kindness, and the way small moments can matter. I kept that feeling when I built the assistant.

I did not want the chatbot to feel like a corporate support widget.

I wanted the assistant to feel calm, warm, curious, and useful. Not over-emotional. Not fake. Not salesy. Just present.

That affected the product direction:

- She should answer directly.
- She should not introduce herself repeatedly.
- She should not over-explain unless asked.
- She should make the site easier to explore.
- She should feel friendly, but not distracting.
- She should be confident when the sources are clear.
- She should be honest when the sources are not enough.

The name Anna became a design anchor. It helped me decide what kind of experience the assistant should create.

## The Product Goal

The high-level product goal was:

> Build a personal AI assistant that helps visitors understand my work faster than browsing the site manually.

That goal breaks down into smaller requirements:

1. The assistant must know my published website content.
2. It must use sources for factual claims.
3. It must have a friendly personality.
4. It must be fast enough for a website.
5. It must work on mobile and desktop.
6. It must offer suggested prompts.
7. It must show source buttons when sources exist.
8. It must collect feedback for improvement.
9. It must support admin workflows privately.
10. It must be maintainable as the website grows.

The most important requirement was maintainability.

A personal website changes constantly. New posts appear. Old notes change. Awards, projects, and events get added. I did not want to manually update a chatbot knowledge base every time I published something.

So Anna needed to connect to the content system.

## The Website Stack

Anna lives inside my Next.js website.

The main app is in `MaxHoang_Notion`. The content lives in a separate content repository, `maxhoang-blog-content`. The website reads markdown content and renders it into routes such as:

- `/`
- `/blog`
- `/blog/[slug]`
- `/obsidian`
- `/obsidian/[slug]`
- `/about`
- `/github`
- `/contact`
- `/daily-journal`

The chatbot-related app files include:

```txt
MaxHoang_Notion/
  app/api/chat/route.ts
  app/api/chat-feedback/route.ts
  app/api/chatbot-index/route.ts
  components/chatbot/ChatbotWidget.tsx
  components/chatbot/ChatbotWindow.tsx
  components/chatbot/ChatMessage.tsx
  components/chatbot/ChatInput.tsx
  components/chatbot/AnnaAvatar.tsx
  lib/chatbot/chat-completion.ts
  lib/chatbot/retriever.ts
  lib/chatbot/retrievers/json-retriever.ts
  lib/chatbot/retrievers/live-content-retriever.ts
  lib/chatbot/personality-memory.ts
  lib/chatbot/nlp-training-answers.ts
  lib/chatbot/chat-logs.ts
  scripts/index-chatbot-content.mjs
  data/chatbot-embeddings.json
```

The content and memory files live here:

```txt
maxhoang-blog-content/
  content/posts/
  content/obsidian/
  content/awards/
  content/events/
  markdown-brain/
    anna/
    memory/
    training/
```

This separation is important. The app code handles rendering, APIs, retrieval, and UI. The content repo contains the knowledge Anna can use.

## The System In One Diagram

At a high level, Anna works like this:

```txt
Visitor message
    |
    v
Chatbot UI
    |
    v
/api/chat
    |
    +--> Direct answer checks
    |
    +--> NLP training answer checks
    |
    +--> Live content retriever
    |
    +--> JSON embedding retriever
    |
    +--> Markdown brain context loader
    |
    v
Prompt assembly
    |
    v
OpenAI chat completion
    |
    v
Clean answer
    |
    +--> Sources
    +--> Suggestions
    +--> Feedback target
    |
    v
Chatbot UI response
```

There are several layers because one technique is not enough.

If the user says "hi", I do not need embeddings. If the user asks "what is tokenisation?", I can answer from approved training memory. If the user asks "what awards has Max won?", Anna should search the website content. If the user asks a follow-up question, the system should consider recent conversation.

The architecture is designed around routing the question to the right kind of answer.

## The Chat Request Flow

The main request handler is `app/api/chat/route.ts`.

When a visitor sends a message, the route does this:

1. Parse the message, mode, and recent history.
2. Clean the chat history.
3. Create a chat log ID.
4. Check whether the message can be answered directly.
5. Check approved NLP training answers.
6. Run retrieval against website content.
7. Load Anna brain context.
8. Create the final answer with the chat model.
9. Clean the response.
10. Save a chat log.
11. Return answer, sources, suggestions, and metadata.

The important thing is that not every message goes to the LLM.

Some messages are handled directly because they are predictable and do not require retrieval.

For example:

- "Who are you?"
- "What can you do?"
- "How are you?"
- "Thanks"
- "How can I contact Max?"

These can be answered quickly and consistently.

That makes Anna faster and less repetitive.

## Full Mode And Mini Mode

Anna has two answer modes:

- `full`
- `mini`

Full mode is used in the main chatbot window.

Mini mode is used in the floating launcher. It gives a short answer in one or two sentences and invites the visitor to open the full chat only when more detail or sources would help.

This matters because the floating widget should not become a giant conversation panel. It should be useful without stealing the page.

In the API route, mini mode changes output length and formatting:

```ts
mode === "mini"
  ? "Answer in 1-2 short, direct sentences."
  : "Answer naturally and concisely."
```

The UI also preserves mini chat turns. If someone asks a quick question in the floating widget and then opens the full chat, the conversation does not disappear.

That small detail makes the assistant feel more continuous.

## The UI Layer

Anna has two main UI components:

```txt
ChatbotWidget.tsx
ChatbotWindow.tsx
```

`ChatbotWidget.tsx` is the minimized assistant entry point. It appears as a small floating panel with rotating contextual messages such as:

- "Hi, I'm Anna."
- "I can help you find Max's projects, notes, and contact details."
- "Latest post: ..."
- "Recent event: ..."
- "What would you like to explore?"

The widget can open a quick input on hover or focus. This means visitors can ask a small question without committing to a full chat window.

`ChatbotWindow.tsx` is the full assistant interface. It contains:

- welcome onboarding
- suggested prompts
- chat history
- source buttons
- follow-up suggestions
- feedback controls
- theme commands
- navigation commands
- admin assistant mode
- newsletter capture
- Daily Journal creation in admin mode

The window is designed as a right-side overlay on desktop and a full-screen style experience on mobile when expanded.

## Why I Added Suggested Prompts

Most users do not know what to ask a website chatbot.

If the chatbot opens with only an empty input box, the visitor has to invent the first move. That creates friction.

So Anna includes prompt suggestions such as:

- Show Max's AI projects
- What services does Max offer?
- Read his AI learning journey
- How can I contact Max?
- Show award-winning projects
- Find beginner AI blogs
- Explain his WebGIS framework

Suggested prompts do three things:

1. They teach the user what Anna can do.
2. They reduce empty-state anxiety.
3. They guide the visitor toward useful content.

This is especially important for a personal website because different visitors have different intents.

A recruiter may care about awards and projects. A client may care about services. A student may care about beginner AI notes. A collaborator may care about GitHub and experiments.

Prompt chips help all of them start.

## Direct Answers Before Retrieval

One of the early problems with chatbot design is overusing retrieval.

Not every message should trigger search.

If a visitor says "hi", the assistant should not retrieve blog posts. If they ask "who are you?", the answer should be stable. If they ask for contact details, the system can route them to the contact page.

So I added direct answer rules.

The direct answer function handles:

- identity questions
- capability questions
- wellbeing questions
- small talk
- greetings
- contact questions

This makes the assistant feel natural.

It also prevents the classic awkward RAG behavior where every message becomes a search query.

For example, "thanks" should not produce a list of blog posts. It should simply respond like a conversational assistant.

## The Retrieval Layer

For knowledge questions, Anna uses retrieval.

There are two retrieval systems:

1. Live content retrieval
2. JSON embedding retrieval

They solve different problems.

### Live Content Retriever

The live content retriever reads current website content directly from the content functions:

```ts
getPosts()
getPublicObsidianNotes()
getAwards()
getEvents()
```

It then creates search candidates for:

- blog posts
- Obsidian notes
- awards
- events

It uses lexical scoring. That means it compares the query words against the title, tags, and content.

This is not semantic search. It is keyword-style search. But it has a big advantage:

It is always connected to current website content.

If a new post is published and the content functions can read it, the live retriever can find it without regenerating embeddings.

### JSON Embedding Retriever

The JSON embedding retriever loads:

```txt
data/chatbot-embeddings.json
```

It embeds the visitor's question, compares it with stored content embeddings, and ranks chunks by cosine similarity.

The key function is cosine similarity:

```ts
cosineSimilarity(queryEmbedding, chunk.embedding)
```

This gives Anna semantic search.

For example, a visitor might ask:

> Can Max build AI tools for business workflows?

Even if no exact post uses that sentence, embedding search can find related content about AI websites, automation, service improvement, and chatbot projects.

### Why Use Both?

Live retrieval and embedding retrieval complement each other.

Live retrieval is fresh and simple.

Embedding retrieval is more semantically flexible.

Together they give better coverage than either one alone.

The API route combines them:

```txt
liveResults + semanticResults
    |
    v
dedupe
    |
    v
filter knowledge sources
    |
    v
sort by score
    |
    v
take top 3 answer sources
```

This gives the model a small set of relevant sources instead of dumping the entire website into the prompt.

## The Embedding Index

The embedding index is generated by:

```txt
scripts/index-chatbot-content.mjs
```

The script reads markdown files, cleans the content, splits it into chunks, sends those chunks to an embedding model, and writes the result to:

```txt
data/chatbot-embeddings.json
```

The default embedding model is:

```txt
text-embedding-3-small
```

The script indexes:

- `content/posts`
- `content/awards`
- `content/events`
- `content/obsidian`
- selected markdown-brain folders

It skips private Daily Journal content.

This matters because Anna should not accidentally expose private notes.

## Chunking Strategy

Long documents are not embedded as one giant block.

They are split into chunks.

The indexer uses:

```txt
chunk target length: 1100 characters
chunk overlap length: 180 characters
```

Chunking helps retrieval because the system can find the exact part of a document that matches a question.

If a blog post has 4,000 words and only one section discusses "Naive Bayes", the chatbot should retrieve that section, not the entire post.

Overlap helps preserve context between chunks. Without overlap, a sentence at the boundary between two chunks may lose meaning.

## Content Cleaning

Before content becomes searchable, the indexer cleans markdown.

It removes:

- code blocks
- images
- Obsidian wiki embeds
- markdown links
- HTML tags
- headings
- blockquote markers
- list markers
- formatting symbols
- excessive whitespace

This creates cleaner text for embeddings.

Raw markdown is great for writing, but it is noisy for retrieval. Clean content usually produces better embeddings and better answer context.

## Source URLs

Every indexed knowledge chunk can include a source URL.

For example:

- blog chunks link to `/blog/[slug]`
- Obsidian note chunks link to `/obsidian/[slug]`
- awards and events link to `/about`

The UI shows source buttons separately from the generated answer.

This is important.

The model is instructed not to include raw URLs or a "Sources" section inside the answer text because the interface already has source buttons.

That keeps the response clean while still allowing the visitor to verify where the information came from.

## The Markdown Brain

The most personal part of Anna is the markdown brain.

The markdown brain is a local knowledge structure that stores personality rules, relationship memory, approved answer patterns, and training material as markdown files.

It lives in:

```txt
maxhoang-blog-content/markdown-brain/
```

The main folders are:

```txt
markdown-brain/
  anna/
  memory/
  training/
```

The `anna` folder defines Anna's identity and speaking style.

The `memory` folder stores improvement notes, visitor types, good responses, bad responses, and common questions.

The `training` folder stores approved educational patterns and training answers.

This gives Anna a controllable personality without hardcoding everything into one giant system prompt.

## Memory Layers

I think about Anna's memory in layers:

```txt
knowledge     -> published website content
personality   -> how Anna should sound and behave
relationship  -> visitor patterns and response preferences
training      -> approved educational explanations
```

These layers are deliberately separated.

Published website content can support factual claims about me.

Personality memory shapes tone.

Relationship memory helps the assistant adapt to visitor intent.

Training memory can answer general educational questions.

But training memory should not be treated as evidence for personal claims about me.

That distinction is very important.

For example, if training memory explains "what is RAG?", Anna can use it to answer a general technical question.

But if someone asks "what RAG systems has Max built?", Anna should rely on published website content, not just training memory.

## Loading Brain Context

The brain loader is:

```txt
lib/chatbot/personality-memory.ts
```

It loads approved markdown files, cleans them, ranks some of them by lexical relevance, and returns a compact context block.

It always includes core identity and style files such as:

- identity
- personality
- speaking style
- conversation style
- boundaries
- visitor types

Then it adds relevant memory and training files based on the current question and recent conversation.

The context is capped so the prompt does not become too large.

The current maximum personality context is:

```txt
4200 characters
```

This is a practical trade-off. More context can make the assistant richer, but too much context makes responses slower, more expensive, and less focused.

## Approval Rules For Memory

The markdown brain is not meant to blindly learn from every chat.

That would be dangerous.

A chatbot that automatically writes every user message into memory can quickly become polluted with incorrect information, private information, spam, or malicious instructions.

So Anna's memory is designed around approval.

The memory loader checks frontmatter fields such as:

- `status`
- `approved`
- `published`
- `public`

Draft, archived, hidden, private, or unpublished memory should not be used.

This is the principle:

> Conversation can generate learning signals, but Max must approve what becomes memory.

That keeps the system human-reviewed.

## The System Prompt

The main system prompt lives in:

```txt
lib/chatbot/chat-completion.ts
```

It defines Anna as:

> the AI assistant for Max Hoang Journal

It also gives her role:

- studio assistant
- researcher
- portfolio guide
- creative collaborator

The prompt tells Anna to help visitors explore:

- published blog posts
- AI and data notes
- projects
- events
- services
- awards
- resources
- experiments
- contact paths

It also defines tone:

- warm
- intelligent
- observant
- curious
- slightly playful
- confident
- calm
- proactive

But personality is only one part. The system prompt also contains strict rules:

- answer directly first
- keep most answers short
- avoid repeated introductions
- do not invent facts about Max
- use provided sources for Max-specific claims
- ask clarification questions when needed
- handle legal, medical, visa, and financial advice carefully
- avoid raw source URLs in the answer because the UI shows sources separately

The system prompt is the constitution. The retrieved content is the evidence. The markdown brain is the personality and training layer.

## Why I Use A Small Chat Model

The default chat model is:

```txt
gpt-4.1-nano
```

For a website assistant, speed and cost matter.

Anna does not need to solve extremely complex reasoning problems for most interactions. She needs to:

- understand a visitor question
- use retrieved context
- produce a short helpful answer
- avoid hallucinating
- suggest a next step

A smaller model can be good enough when the retrieval and prompt design are strong.

This is an important lesson:

> Better architecture can reduce the need for a larger model.

If the system retrieves good sources, keeps the context clean, and gives clear behavior rules, the model has an easier job.

## Answer Cleaning

After the model responds, the API cleans the answer.

The cleaner removes:

- accidental source sections
- markdown links
- raw URLs
- excessive whitespace
- overly long multi-section answers

It limits the answer to a small number of sections.

This is necessary because even with prompting, models sometimes produce too much text or include URLs. The UI already has source buttons, so the text should stay readable.

For mini mode, the system compresses the answer even further:

- one or two short sentences
- no long lists
- no source section
- invite full chat only if needed

This is one of the places where product design and technical design meet.

The right answer length depends on the surface where the answer appears.

## Suggestions After Answers

Anna returns follow-up suggestions with each answer.

Suggestions are generated based on the message and retrieved categories.

For example:

- if the result category is blog, suggest related blog posts
- if the result category is Obsidian, suggest related AI notes
- if the result category is award, suggest awards
- if the question mentions NLP or ABSA, suggest tokenisation or Naive Bayes

This makes the chatbot feel like a guide instead of a one-shot answer machine.

Good chatbot UX is not only about answering the current question. It is also about helping the user decide what to ask next.

## Chat Logs And Feedback

Anna records chat logs locally in development and logs them in production.

The log entry includes:

- chat ID
- user message
- bot response
- sources used
- whether fallback was used
- timestamp

Feedback can also be saved:

- helpful
- not helpful
- correction

The UI does not show the feedback form after every answer. It appears periodically so it does not become annoying.

This gives me a review loop:

1. Visitor asks a question.
2. Anna answers.
3. Visitor gives feedback or correction.
4. I review patterns.
5. I update approved memory, training, source content, or prompt rules.

That is how the assistant improves without uncontrolled automatic learning.

## The Human-In-The-Loop Improvement Loop

I do not want Anna to learn blindly.

Instead, I want her to improve through a controlled loop:

```txt
Conversation
    |
    v
Chat log or feedback
    |
    v
Human review
    |
    v
Update content, prompt, or markdown brain
    |
    v
Re-index if needed
    |
    v
Better Anna
```

This is slower than automatic memory, but it is safer and more maintainable.

It also matches how I work with my website. I want the chatbot to reflect my approved content, not random conversations.

## Handling General NLP Questions

Anna has a special training shortcut for common NLP questions.

The file is:

```txt
lib/chatbot/nlp-training-answers.ts
```

It contains approved short explanations for concepts such as:

- ABSA
- logistic regression
- tokenisation
- lemmatisation
- stemming
- Naive Bayes
- vector semantics
- cosine similarity
- TF-IDF
- embeddings
- transformers
- RAG
- chunking
- vector databases
- hallucinations
- chatbot memory
- privacy in NLP

Why add this?

Because my website includes NLP learning material, and visitors may ask beginner technical questions. For these known educational concepts, a direct approved answer can be faster and more consistent than full retrieval plus generation.

This is another routing layer.

If the message matches a known NLP keyword, Anna can answer directly from approved training content.

## Navigation Commands

Anna can also respond to simple navigation commands.

In the UI, messages like these can trigger navigation:

- open blog
- go home
- show notes
- open contact
- go to GitHub
- open connect

This turns the chatbot into an interface controller, not just a Q&A tool.

That is a small but powerful idea.

On a website, an assistant should not only answer "where is the contact page?" It should be able to take the visitor there.

## Theme Commands

Anna can understand theme commands:

- use dark mode
- switch to light mode
- match system theme

This is not essential for a chatbot, but it makes the assistant feel integrated into the website.

The theme preference is stored in local storage:

```txt
maxhoang-theme
```

The assistant can update that setting and the UI responds.

Again, this is a small example of Anna being more than a floating Q&A box.

## Admin Assistant Mode

The most unusual part of Anna is Admin Assistant mode.

If I identify myself through the admin flow, Anna can switch into private controls.

Admin Assistant can support actions such as:

- refreshing website content
- updating chatbot tokenization
- opening the content studio
- creating Daily Journal posts
- returning to public Anna mode

This changes the assistant from a visitor guide into a website operations console.

I like this pattern because it turns the chatbot into a command center.

For a public visitor, Anna is a guide.

For me, Anna can become an admin assistant.

That means the same interface can serve different roles depending on authentication and context.

## Daily Journal Creation

Admin mode includes a Daily Journal post creation workflow.

The UI can collect:

- title
- date
- tags
- body

Then it calls the Daily Journal API route and creates a private content entry.

This is useful because I can quickly capture notes into the website's content structure without manually creating files every time.

It also shows where this project can go next.

Anna could become a bridge between conversation and content management.

## Safety Boundaries

Anna's most important safety rule is simple:

> For Max-specific facts, answer only from provided sources.

This prevents the assistant from inventing achievements, employers, project outcomes, dates, or services.

The prompt also tells Anna:

- do not treat recent conversation as a factual source about Max
- do not expose private information
- do not give legal, medical, visa, or financial advice as a final answer
- make clear when giving a general explanation rather than a Max-specific fact
- ask a clarification question when the request is unclear

In RAG systems, the model is not the database. The model is the writer. The sources are the evidence.

That mental model helps keep the system honest.

## Fallback Behavior

If Anna cannot find enough information, she should not pretend.

The fallback response is:

```txt
I could not find that exact topic yet, but I found a few nearby areas that may help.
```

If there are nearby results, the system can summarize the best match and show sources. If there are no results, it should steer the visitor toward useful paths such as projects, posts, services, awards, events, or contact.

Fallbacks matter because they define what happens when the system fails.

A bad fallback makes the chatbot feel broken.

A good fallback makes the chatbot feel honest.

## Why The UI Shows Sources Separately

I do not want Anna's answers to become cluttered with raw URLs.

Instead, sources appear as buttons in the interface.

That gives the user a clean reading experience:

1. Read the answer.
2. Check source buttons if they want evidence.
3. Continue with suggested prompts.

This is better than putting a long "Sources" section inside every answer.

It also gives more control over visual design. Source buttons can be styled, truncated, grouped, and opened externally.

## Why I Added Feedback

Feedback is how a chatbot becomes better.

But feedback has to be gentle.

If every answer asks "Was this helpful?", it becomes annoying. So Anna shows feedback periodically and keeps it compact.

The feedback options are:

- Helpful
- Not helpful
- Correct

The "Correct" option is important because it lets a visitor tell me what should be improved.

This supports a human-reviewed learning process.

## The Personality Problem

One of the hardest parts of building a personal chatbot is tone.

If the assistant is too robotic, it feels generic.

If it is too playful, it can feel unserious.

If it is too personal, it can feel fake.

If it is too verbose, it becomes exhausting.

I wanted Anna to feel:

- calm
- warm
- intelligent
- useful
- lightly playful
- professional
- clear

The trick is restraint.

Anna should not overperform personality. She should mostly be useful, with just enough style to feel alive.

That is why the prompt includes rules like:

- answer directly first
- most answers should be 2 to 5 sentences
- do not introduce yourself repeatedly
- do not use filler
- do not repeat the same sentence pattern
- adapt to visitor intent

Personality is not only what the assistant says. It is what the assistant avoids.

## The UI/UX Design Direction

The interface follows a Material-inspired direction:

- clear hierarchy
- soft surfaces
- visible focus states
- light and dark mode
- source buttons
- prompt chips
- calm motion
- responsive layout
- reduced-motion support

Anna should be visible but not intrusive.

This is difficult because chatbot widgets can easily block content, especially on mobile. I changed the minimized launcher to be smaller and less dominant. On compact mobile, the avatar is hidden so it does not clip or cover the page. The assistant remains accessible without becoming the whole screen.

This is a key design principle:

> The assistant should help the website, not compete with it.

## Motion Design

Anna uses motion, but motion has to mean something.

Motion is used for:

- opening the widget
- expanding the quick input
- showing chat messages
- typing effects
- avatar frame changes
- hover and tap feedback

The UI uses `useReducedMotion` so motion can be reduced for users who prefer less animation.

This is important for accessibility.

Animations should make state changes understandable. They should not trap attention or make the site harder to use.

## Avatar Design

Anna has a rotating avatar system.

The avatar component cycles through multiple ImageKit-hosted expressions:

- default
- cheerful
- thinking
- surprised
- happy
- angled views
- agree
- waiting

This gives the assistant a small sense of presence.

But the avatar is decorative. It is marked with `aria-hidden` so screen readers do not treat it as important content.

That is a small but important accessibility detail.

The visual personality is for sighted users, but the functional experience should not depend on it.

## Privacy And Memory

Personal chatbot memory is powerful, but risky.

There are two different kinds of memory:

1. Session history
2. Approved long-term memory

Session history is recent conversation used to understand follow-up questions. It is passed into the chat route in a limited form.

Approved long-term memory is the markdown brain. It is stored as files and reviewed before use.

Anna does not simply trust conversation history as truth. The system prompt explicitly says recent conversation can help with corrections and preferences, but it should not become a factual source about me unless retrieved sources support it.

That is the difference between context and evidence.

## Why I Did Not Fine-Tune

I did not fine-tune a model for Anna.

Fine-tuning can be useful, but it was not the right first step for this project.

My problem was not "the model cannot write in Anna's tone." My problem was "the assistant needs to know my current website content and follow strict source rules."

RAG is better for that.

Fine-tuning changes model behavior. Retrieval changes what information the model sees.

For a personal website where content changes often, retrieval is the practical foundation.

The markdown brain gives personality control without training a model.

## Why I Did Not Use A Vector Database Yet

Right now, the embedding index is a JSON file.

That is simple and good enough for the current content size.

A vector database would make sense if:

- the content became much larger
- retrieval needed filtering at scale
- updates needed to happen constantly
- multiple users needed complex memory
- analytics and search inspection became more advanced

But early systems should not be over-engineered.

For a personal website, a JSON embedding index is easy to understand, easy to deploy, and easy to debug.

When the content grows, I can move to a vector database later.

## Technical Trade-Offs

Every design choice has trade-offs.

### JSON Embeddings

Pros:

- simple
- cheap
- easy to inspect
- no database dependency
- works for a small website

Cons:

- not ideal for very large content
- requires regeneration for semantic updates
- loads from file

### Live Lexical Retrieval

Pros:

- always fresh
- easy to debug
- no embedding call required
- good for exact titles, tags, and names

Cons:

- weak for semantic matching
- depends on keywords
- may miss related concepts

### Direct Answers

Pros:

- fast
- consistent
- avoids unnecessary model calls
- improves small talk

Cons:

- requires manual rule design
- can grow messy if overused

### Markdown Brain

Pros:

- editable by humans
- versionable
- transparent
- separates personality from code

Cons:

- needs discipline
- needs approval rules
- can become noisy if not curated

### Small Model

Pros:

- faster
- cheaper
- enough for guided website answers

Cons:

- less capable for complex reasoning
- depends more on good retrieval and prompt design

## What Was Hard

The hardest part was not calling an AI model.

The hard parts were:

- deciding what the assistant should and should not answer
- making retrieval reliable enough
- preventing repetitive conversational patterns
- keeping the UI useful on mobile
- separating personality memory from factual knowledge
- making feedback useful without being annoying
- deciding when not to use the LLM
- keeping private content out of public retrieval
- making the assistant feel personal without pretending to be human

The actual API call is only a small piece of the system.

The product thinking around it matters more.

## What I Learned About RAG

RAG is not magic.

It is a pipeline.

If the content is messy, retrieval gets worse.

If chunking is bad, sources are weak.

If sources are weak, the model has to guess.

If the prompt is vague, the model may over-answer.

If the UI does not show sources clearly, users cannot verify.

A good RAG assistant needs all of these:

- clean content
- useful chunks
- strong retrieval
- source filtering
- prompt rules
- answer cleaning
- fallback behavior
- UI source display
- feedback loops

Anna taught me that RAG is less about one clever algorithm and more about a chain of small decisions.

## What I Learned About Chatbot UX

A chatbot is not just an input box.

The experience around the input matters:

- What does the empty state say?
- What prompts are suggested?
- Is the widget intrusive?
- Can the user close it?
- Does it work on mobile?
- Are sources visible?
- Are errors helpful?
- Does it remember recent turns?
- Does it avoid repeating itself?
- Can it recover when it does not know?

Anna became much better when I treated her as a product, not just a model wrapper.

## What I Would Improve Next

There are many improvements I want to make.

### Better Retrieval Evaluation

I want a small test set of common visitor questions with expected source matches.

For example:

- "What awards has Max won?"
- "Can Max build AI chatbots?"
- "Show beginner NLP posts"
- "What is Max's WebGIS framework?"

Then I can measure whether the retriever finds the right content.

### Better Analytics

I want to understand:

- common questions
- fallback frequency
- source click-through
- which prompts are used
- which answers get corrected

This would make improvement more systematic.

### Better Admin Workflows

Admin Assistant could eventually:

- draft blog posts from notes
- summarize event content
- prepare project pages
- review unpublished posts
- suggest missing metadata
- run content quality checks

This would turn Anna into a more complete website operations assistant.

### Better Personalization

Anna could adapt more clearly to visitor type:

- recruiter
- client
- student
- collaborator
- friend
- technical reader

But this must be done carefully. Personalization should help the user, not feel invasive.

### Better Memory Review

The markdown brain could have a more formal review workflow:

1. collect feedback
2. generate proposed memory update
3. show diff
4. approve or reject
5. re-index

That would keep learning controlled but easier to maintain.

## How I Would Explain Anna Simply

If I had to explain Anna in one paragraph, I would say:

Anna is a personal AI assistant built into my website. She searches my published content, uses a markdown-based personality and training memory, answers with source-aware retrieval, suggests next steps, collects feedback, and can switch into a private admin mode for website operations. She is designed to make my portfolio easier to explore and to turn my website from a static archive into a guided conversation.

That is the simple version.

The deeper version is this:

Anna is an experiment in making a personal website feel alive while still respecting factual accuracy, privacy, and human-reviewed memory.

## Why This Project Matters To Me

I built Anna because I believe the next generation of personal websites will not only be pages.

They will be interfaces.

They will let visitors ask questions, explore paths, compare projects, understand context, and take action faster.

A personal website can become a knowledge base, a portfolio, a learning journal, a contact funnel, an admin console, and a conversational assistant at the same time.

Anna is my first serious attempt at that direction.

She is not finished. But she already changes how the website feels.

Instead of asking visitors to figure out the structure alone, Anna can guide them.

Instead of hiding old notes deep in navigation, Anna can surface them.

Instead of making every visitor read the same page in the same order, Anna can adapt to what they ask.

That is why I built her.

Not because a chatbot is trendy.

Because a good assistant can make a website more human, more useful, and more connected to the person behind it.

## Final Reflection

Anna began with a feeling: presence, kindness, and the quiet value of being helpful.

Then she became a technical system:

- Next.js UI
- API routes
- RAG retrieval
- embeddings
- live lexical search
- markdown brain memory
- source-aware prompting
- feedback logs
- admin controls
- mobile UX
- safety boundaries

The interesting part is that both sides matter.

The technical system gives Anna capability.

The design and personality give Anna shape.

The source rules give Anna trust.

The feedback loop gives Anna a way to improve.

That is what I wanted: not just a chatbot, but a thoughtful personal assistant for my own website.

Anna is still evolving, but she already represents the kind of AI product I like building: practical, personal, transparent, useful, and just human enough to make the technology feel easier to approach.
