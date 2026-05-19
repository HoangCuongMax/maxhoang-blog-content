# Personal Portfolio Chatbot Build Plan

## Goal

Build a small chatbot widget for `maxhoang.com.au` that reads Markdown/Obsidian website content and answers questions about Max Hoang, his projects, awards, blog posts, skills, and website content.

The chatbot should act as a personal portfolio website assistant and showcase chatbot development skills.

## Build Strategy

Use a step-by-step approach so the website structure is not broken. Start with the UI only, then add content loading, retrieval, AI response generation, testing, and deployment.

---

# Phase 1: Confirm Project Scope

## Tasks

- [ ] Confirm the chatbot domain: personal portfolio website assistant.
- [ ] Confirm target users: visitors, students, employers, recruiters, and collaborators.
- [ ] Confirm main website: `maxhoang.com.au`.
- [ ] Confirm content source: Markdown/Obsidian files.
- [ ] Confirm the chatbot will only answer based on available website content.
- [ ] Confirm fallback behaviour for unsupported questions.

## Output

- Clear project scope.
- Confirmed chatbot role and limitations.

---

# Phase 2: Create Chatbot UI Only

## Goal

Create a small chatbot widget on the website without connecting it to AI yet.

## Tasks

- [ ] Add a chatbot floating button to the website.
- [ ] Place the button at the bottom-right corner.
- [ ] Use a clean icon for the chatbot.
- [ ] Open a small chat window when the user clicks the button.
- [ ] Add a header with chatbot name.
- [ ] Add a welcome message.
- [ ] Add message bubbles for user and assistant.
- [ ] Add a text input box.
- [ ] Add a send button.
- [ ] Make the UI responsive for desktop and mobile.
- [ ] Match the website design style.
- [ ] Use shadcn/ui components where suitable.

## Output

- Chatbot UI is visible and working.
- User can type messages.
- Chat window can open and close.
- No AI connection yet.

---

# Phase 3: Prepare Markdown Content Source

## Goal

Prepare the website Markdown/Obsidian content so the chatbot can use it later.

## Tasks

- [ ] Identify all Markdown folders used by the website.
- [ ] Confirm which content folders should be included.
- [ ] Exclude private or unfinished notes if needed.
- [ ] Read frontmatter fields such as title, description, date, tags, slug, and category.
- [ ] Extract body content from Markdown files.
- [ ] Remove unnecessary Markdown syntax where needed.
- [ ] Keep useful headings and metadata.
- [ ] Create a clean content format for indexing.

## Suggested Included Content

- [ ] Blog posts
- [ ] Project notes
- [ ] Award notes
- [ ] Event notes
- [ ] Portfolio notes
- [ ] Website assistant notes

## Output

- Markdown content can be loaded and prepared for search.

---

# Phase 4: Build Content Indexing Script

## Goal

Create a script that reads all Markdown files and converts them into searchable chunks.

## Tasks

- [ ] Create a script such as `scripts/index-chatbot-content.ts`.
- [ ] Load Markdown files from the selected content folders.
- [ ] Parse frontmatter.
- [ ] Split long content into smaller chunks.
- [ ] Keep metadata for each chunk.
- [ ] Include title, slug, path, tags, and source URL where possible.
- [ ] Save indexed content to a local JSON file for the first version.

## Example Chunk Fields

- `id`
- `title`
- `slug`
- `path`
- `tags`
- `content`
- `sourceUrl`

## Output

- A searchable content index exists.
- The chatbot has a structured knowledge source.

---

# Phase 5: Add Simple Search First

## Goal

Before using AI, test whether the chatbot can find relevant website content using simple search.

## Tasks

- [ ] Add keyword search over indexed Markdown chunks.
- [ ] Match questions with titles, tags, headings, and body content.
- [ ] Return the most relevant chunks.
- [ ] Show a simple answer using matched content.
- [ ] Test with common questions about Max, awards, projects, and blog posts.

## Example Test Questions

- [ ] Who is Max Hoang?
- [ ] What projects has Max worked on?
- [ ] What awards has Max received?
- [ ] What AI projects are on this website?
- [ ] Where can I read about chatbot development?

## Output

- Basic non-AI retrieval works.
- The system can find relevant content.

---

# Phase 6: Add AI API Connection

## Goal

Connect the chatbot to an AI model so it can generate natural answers from retrieved Markdown content.

## Possible Providers

- [ ] OpenRouter
- [ ] OpenAI API
- [ ] DeepSeek API through OpenRouter
- [ ] Other low-cost LLM provider

## Tasks

- [ ] Create a secure server-side API route for chat.
- [ ] Store API key in environment variables.
- [ ] Never expose the API key to the browser.
- [ ] Send the user question to the backend.
- [ ] Retrieve relevant Markdown chunks.
- [ ] Send only relevant chunks to the AI model.
- [ ] Ask the model to answer only based on the provided context.
- [ ] Return the answer to the chatbot UI.

## Output

- The chatbot can generate natural answers.
- The answer is based on website content.

---

# Phase 7: Add RAG Behaviour

## Goal

Improve the chatbot by using Retrieval-Augmented Generation.

## Tasks

- [ ] Convert Markdown chunks into embeddings.
- [ ] Store embeddings in a vector database.
- [ ] Use semantic search to find relevant content.
- [ ] Retrieve the top matching chunks for each question.
- [ ] Generate answers using only retrieved context.
- [ ] Include source titles or links when possible.

## Possible Vector Storage Options

- [ ] Supabase with pgvector
- [ ] Local JSON for demo version
- [ ] Upstash Vector
- [ ] Pinecone
- [ ] Chroma for local testing

## Output

- The chatbot can answer more accurately using semantic search.

---

# Phase 8: Add Safety and Fallback Rules

## Goal

Make the chatbot reliable and avoid unsupported answers.

## Tasks

- [ ] Add a system prompt with strict website-assistant behaviour.
- [ ] Tell the chatbot not to hallucinate.
- [ ] Tell the chatbot to answer only from provided content.
- [ ] Add fallback response for missing information.
- [ ] Add out-of-scope detection.
- [ ] Avoid giving medical, legal, or financial advice.
- [ ] Keep responses clear and professional.

## Example Fallback

I do not have enough information about that in Max's website content. I can help with questions about Max, his projects, awards, blog posts, skills, and portfolio instead.

## Output

- The chatbot gives safer and more honest answers.

---

# Phase 9: Add Website Navigation Support

## Goal

Help users move around the website.

## Tasks

- [ ] Add source links to answers.
- [ ] Suggest relevant blog posts or project pages.
- [ ] Guide users to awards, events, projects, or contact pages.
- [ ] Add quick suggestion buttons.
- [ ] Add common prompts such as:
  - Who is Max?
  - Show me Max's AI projects.
  - What awards has Max won?
  - How can I contact Max?

## Output

- The chatbot works as a website navigation assistant.

---

# Phase 10: Test the Chatbot

## Goal

Evaluate whether the chatbot meets the assignment and website goals.

## Test Categories

- [ ] Greeting test
- [ ] Personal profile question
- [ ] Project question
- [ ] Award question
- [ ] Blog content question
- [ ] Website navigation question
- [ ] Out-of-scope question
- [ ] Unknown information question

## Example Test Set

- [ ] Hello, who are you?
- [ ] Who is Max Hoang?
- [ ] What AI projects has Max built?
- [ ] What awards has Max received?
- [ ] What blog posts are about chatbot development?
- [ ] How can I contact Max?
- [ ] Can you give me medical advice?
- [ ] What is Max's favourite movie?

## Output

- Test results recorded.
- Strengths and weaknesses identified.

---

# Phase 11: Prepare Assignment Demonstration

## Goal

Prepare the chatbot for live presentation.

## Tasks

- [ ] Prepare a short intro about the chatbot domain.
- [ ] Explain the challenge: helping users explore personal website content.
- [ ] Explain the approach: Markdown content plus retrieval plus AI response.
- [ ] Show live chatbot testing.
- [ ] Show fallback behaviour.
- [ ] Explain limitations.
- [ ] Explain future improvements.

## Demo Questions

- [ ] Who is Max Hoang?
- [ ] What AI projects are shown on this website?
- [ ] What awards has Max won?
- [ ] Where can I find blog posts about chatbot development?
- [ ] Can you answer questions outside Max's website?

## Output

- Presentation demo is ready.

---

# Phase 12: Deploy and Monitor

## Goal

Deploy the chatbot safely on the live website.

## Tasks

- [ ] Test locally.
- [ ] Test on preview deployment.
- [ ] Check mobile responsiveness.
- [ ] Check API key security.
- [ ] Check response speed.
- [ ] Check usage cost.
- [ ] Deploy to production.
- [ ] Monitor errors and user questions.

## Output

- Chatbot is live on `maxhoang.com.au`.

---

# Minimum Viable Product Checklist

The MVP should include:

- [ ] Floating chatbot button.
- [ ] Chat window UI.
- [ ] User input and assistant response display.
- [ ] Markdown content loading.
- [ ] Basic retrieval from website content.
- [ ] AI-generated answer based on retrieved content.
- [ ] Fallback response.
- [ ] Simple testing evidence.

---

# Recommended First Build Order

1. Build the chatbot UI only.
2. Create a local content index from Markdown files.
3. Add simple keyword search.
4. Add API route for chatbot response.
5. Connect OpenRouter or OpenAI.
6. Add RAG/embedding later.
7. Add source links and website navigation support.
8. Test and prepare the assignment demo.

---

# Notes for Codex

- Do not break the existing website structure.
- Ask before changing shared layout files.
- Keep chatbot code modular.
- Start with UI only if API keys are not available.
- Use environment variables for API keys.
- Do not expose API keys in frontend code.
- Keep the chatbot small and simple for the first version.
- Prefer readable code over complex architecture.
- Add comments where helpful for a beginner developer.
