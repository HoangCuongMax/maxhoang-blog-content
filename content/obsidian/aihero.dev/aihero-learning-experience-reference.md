---
title: AIHero.dev Learning Experience Reference
type: product-reference
status: draft
project: aihero-learning-platform
reference_site: https://aihero.dev
tags:
  - aihero-dev
  - learning-platform
  - ai-education
  - product-reference
  - ux-reference
---

# AIHero.dev Learning Experience Reference

## Purpose of This Note

This note describes the learning experience I want to study and use as inspiration from `aihero.dev`.

The goal is not to copy the website exactly, but to understand the kind of learning journey, structure, and user experience I want to build for my own AI learning platform or educational content system.

## Reference Website

- Website: https://aihero.dev
- Reference type: AI learning / developer education experience
- My goal: Build a similar learning experience with my own content, style, and learning pathway

## Screenshot-Based Observations

These observations are based on the screenshots provided from the AIHero LLM Fundamentals course and lesson pages.

### Course Landing Page Pattern

The course landing page uses a clear learning-product structure:

- Top navigation with logo, Learn, Live, Browse all, and Login.
- Strong course title: `LLM Fundamentals`.
- Short course description under the title.
- Instructor profile with photo/name.
- Hero course thumbnail/video preview on the right.
- Clear orange `Start Learning` button.
- Share action next to the main call-to-action.
- Main content area with an introduction and learning outcomes.
- Right-side course content panel listing lessons in sequence.
- Repeated `Start Learning` call-to-action near the bottom.
- Footer with grouped navigation links.

### Course Content Panel Pattern

The right-side content panel is important because it makes the learning path visible before the user starts.

Example lesson list shown in the screenshot:

1. Messages, System Prompts and Reasoning Tokens
2. What Are Tokens?
3. What Is The Context Window?
4. What Are Tools?
5. What Is An Agent?

This creates a simple but strong course structure:

```txt
Course page
→ visible lesson list
→ start learning button
→ individual lesson pages
→ next lesson navigation
```

### Lesson Page Pattern

The lesson page is focused and linear.

Observed structure:

- Left sidebar showing course title and lesson list.
- Current lesson is highlighted.
- Main video at the top.
- Lesson title below the video.
- Instructor name/avatar.
- Small actions such as close, share, and next lesson.
- Written explanation below the video.
- Visual diagrams inside the lesson content.
- Clear headings for each concept.
- Share/copy actions near the end.
- `Up Next` section for the next lesson.
- Footer with learning and account links.

### Content Style Pattern

The lesson content uses a strong teaching style:

- Start with a simple definition.
- Explain the idea in plain language.
- Use visual diagrams to make abstract AI concepts concrete.
- Break the lesson into short sections.
- Use headings for each concept.
- Explain why the concept matters.
- End with next-step navigation.

### Visual Learning Pattern

The screenshots show that the learning experience is not just text. It combines:

- Video teaching
- Written explanation
- Concept diagrams
- Lesson sequencing
- Progress/navigation cues
- Next lesson flow

This is the main experience I want to adapt for my own learning platform.

---

# Learning Experience I Want to Build

## Core Idea

I want to build a learning experience that helps people learn AI, coding, and practical AI product development in a clear, structured, and motivating way.

The experience should feel like a guided journey, not just a collection of blog posts.

Users should be able to:

- Start from beginner-friendly lessons.
- Follow a clear learning path.
- Learn by watching, reading, and doing.
- Build confidence step by step.
- Track what they have completed.
- Understand how each topic connects to real projects.
- Move from theory to hands-on implementation.

## Target Users

The target users may include:

- Beginners learning AI and coding
- Students studying IT or AI
- Career changers moving into technology
- Website visitors interested in my learning journey
- People who want to build practical AI projects
- Employers or collaborators who want to see how I teach and explain AI concepts

## Learning Philosophy

The learning platform should follow this philosophy:

> Learn by watching, reading, building, and connecting each concept to a real project.

The content should avoid being too theoretical. Each lesson should have a practical outcome or a clear concept that helps the learner build something later.

## Desired User Experience

The user experience should be:

- Simple
- Guided
- Visual
- Beginner-friendly
- Practical
- Progress-based
- Project-focused
- Easy to navigate

Users should always know:

- Where they are
- What they are learning
- Why it matters
- What they should do next
- How the lesson connects to a bigger project

---

# AIHero-Inspired Page Structure

## 1. Course Landing Page Template

Each course or learning path should have a landing page.

Recommended structure:

```txt
Header navigation
Course title
Short course description
Instructor/author profile
Course video or visual thumbnail
Start Learning button
Share button
Course introduction
What you will learn
Course content list
Bottom Start Learning button
Footer navigation
```

Checklist:

- [ ] Add course title.
- [ ] Add short description.
- [ ] Add instructor/author information.
- [ ] Add course thumbnail or intro video.
- [ ] Add strong `Start Learning` button.
- [ ] Add lesson list/sidebar.
- [ ] Add `You will learn` section.
- [ ] Add bottom call-to-action.

## 2. Lesson Page Template

Each lesson should have a focused page.

Recommended structure:

```txt
Course sidebar / lesson list
Video or hero visual
Lesson title
Instructor/author information
Lesson actions: share, next lesson, copy link
Short explanation
Concept sections
Visual diagrams
Practical task or reflection
Summary
Up Next section
Footer navigation
```

Checklist:

- [ ] Show course sidebar.
- [ ] Highlight current lesson.
- [ ] Add video or visual at the top.
- [ ] Add lesson title.
- [ ] Add short explanation.
- [ ] Add diagrams or screenshots.
- [ ] Add practical task.
- [ ] Add `Up Next` section.
- [ ] Add previous/next navigation.

## 3. Course Content Sidebar

The sidebar should show the learner where they are in the course.

It should include:

- Course title
- Lesson numbers
- Lesson titles
- Active lesson highlight
- Completed lesson state later

Example:

```txt
LLM Fundamentals
1. Messages, System Prompts and Reasoning Tokens
2. What Are Tokens?
3. What Is The Context Window?
4. What Are Tools?
5. What Is An Agent?
```

For my website, this could become:

```txt
Build a Personal Website Chatbot
1. What Is a Website Assistant?
2. Preparing Markdown Content
3. Building a Chatbot UI
4. Creating a RAG Index
5. Adding AI Responses
6. Adding Fallback Rules
7. Deploying the Chatbot
```

---

# Key Experience Features

## 1. Clear Learning Path

The platform should organise lessons into a clear path.

Example structure:

```txt
Start here
→ AI basics
→ Prompt engineering
→ Python for AI
→ APIs and LLMs
→ RAG chatbot
→ AI website assistant
→ Full AI project portfolio
```

Checklist:

- [ ] Create beginner learning path.
- [ ] Create project-based learning path.
- [ ] Create AI chatbot learning path.
- [ ] Create AI portfolio learning path.
- [ ] Show progress through the path.

## 2. Modular Lessons

Each lesson should be small and focused.

A good lesson should include:

- Topic title
- Short explanation
- Why it matters
- Video or visual explanation
- Step-by-step guide
- Example code or demo
- Small task for the learner
- Expected result
- Next lesson link

Checklist:

- [ ] Each lesson has one main goal.
- [ ] Each lesson has a practical task.
- [ ] Each lesson links to the next lesson.
- [ ] Each lesson connects to a project.

## 3. Project-Based Learning

The learning experience should be connected to real projects.

Possible project paths:

- Build a personal AI chatbot
- Build a website assistant
- Build a RAG system with Markdown notes
- Build a portfolio website
- Build an AI content generator
- Build an AI study assistant

Checklist:

- [ ] Each project has a project brief.
- [ ] Each project has a build plan.
- [ ] Each project has lessons attached to it.
- [ ] Each project has a final demo.
- [ ] Each project can be shown in a portfolio.

## 4. Interactive Learning

The platform should feel interactive where possible.

Possible interaction ideas:

- Checklists
- Quizzes
- Code snippets
- Mini tasks
- Prompt exercises
- Chatbot assistant
- Progress markers
- Reflection questions
- Copy code buttons
- Share lesson buttons

Checklist:

- [ ] Add lesson checklists.
- [ ] Add simple quiz questions.
- [ ] Add practical exercises.
- [ ] Add reflection prompts.
- [ ] Add AI assistant support for learning.

## 5. AI Learning Assistant

The platform should include a chatbot or AI assistant that helps users learn the content.

The assistant could:

- Explain lesson content.
- Answer questions about the learning path.
- Recommend the next lesson.
- Help debug beginner mistakes.
- Summarise project requirements.
- Guide users through exercises.

Checklist:

- [ ] Connect learning content to a RAG chatbot.
- [ ] Let users ask questions about lessons.
- [ ] Let users ask what to learn next.
- [ ] Add fallback when content is not available.
- [ ] Avoid unsupported or hallucinated answers.

---

# Content Structure I Want

## Main Sections

Possible website sections:

```txt
Home
Learn
Learning Paths
Projects
Lessons
AI Tools
Blog
Portfolio
About
```

## Learning Path Page

A learning path page should include:

- Path title
- Who it is for
- What users will build
- Required knowledge
- Estimated time
- Lesson list
- Project outcome
- Progress checklist

## Lesson Page

A lesson page should include:

- Lesson title
- Learning objective
- Simple explanation
- Practical example
- Video or diagram
- Step-by-step task
- Common mistakes
- Summary
- Up Next / Next lesson

## Project Page

A project page should include:

- Project title
- Problem
- Solution
- Tech stack
- Build steps
- Demo
- GitHub link
- What the learner will understand after completing it

---

# Design and UX Direction

## Visual Style

The design should feel:

- Modern
- Clean
- Developer-focused
- Friendly
- Motivating
- Easy to read
- Minimal but not empty

Possible design elements:

- Course hero section
- Video thumbnail card
- Orange or strong accent button
- Cards for lessons
- Progress bars
- Step numbers
- Badges or labels
- Code blocks
- Visual diagrams
- Simple icons
- Dark/light mode support

## Navigation Style

Navigation should be simple and learning-focused.

Possible navigation elements:

- Top navigation: Learn, Live, Browse all, Login
- Sidebar lesson menu
- Breadcrumbs
- Previous/next lesson buttons
- `Up Next` section
- Learning path progress
- Related lessons
- Related projects

---

# First Course Idea for My Website

## Course Name

Build a Personal Website Chatbot

## Course Description

A practical course that teaches learners how to build a chatbot for a personal portfolio website using Markdown content, retrieval, and an AI API.

## Course Outcome

By the end of the course, learners will understand how to:

- Prepare website Markdown content.
- Build a chatbot UI.
- Create a searchable content index.
- Use RAG to retrieve relevant content.
- Generate grounded AI answers.
- Add fallback behaviour.
- Deploy the chatbot on a real website.

## Lesson List

1. What Is a Personal Website Assistant?
2. Why Use Markdown as a Knowledge Base?
3. Preparing Obsidian Content for RAG
4. Building the Chatbot UI
5. Creating a JSON Content Index
6. Adding the Retriever Interface
7. Connecting an AI API
8. Adding Fallback and Safety Rules
9. Preparing for Supabase Later
10. Deploying and Testing the Chatbot

---

# How This Connects to My Existing Work

This learning experience can connect to my existing projects and notes:

- [[AGENTS]]
- [[agent-instruction]]
- [[memory]]
- [[work-instruction]]

The personal chatbot project can become one of the first learning paths or project-based tutorials.

Example learning path:

```txt
Build Your Own Personal Website Chatbot
1. Understand the chatbot goal
2. Prepare Markdown content
3. Create a content index
4. Build the chatbot UI
5. Add retrieval
6. Add AI response generation
7. Add fallback handling
8. Deploy the chatbot
```

---

# MVP Idea

## MVP Name

AI Learning Hero / AI Project Learning Hub

## MVP Goal

Create a small learning platform section on my website where users can follow one clear AI project path.

## First Learning Path

Build a Personal Portfolio Website Chatbot

## MVP Checklist

- [ ] Create one course landing page.
- [ ] Create one course sidebar.
- [ ] Create 5 to 10 lesson pages.
- [ ] Create one project brief page.
- [ ] Create one build plan page.
- [ ] Add checklists to each lesson.
- [ ] Add previous/next links.
- [ ] Add `Up Next` section.
- [ ] Add chatbot assistant support later.

---

# Adaptation Rules

When using AIHero as inspiration:

- Do not copy the branding.
- Do not copy the exact layout pixel by pixel.
- Do not copy course content.
- Adapt the learning flow and structure.
- Use my own voice, projects, examples, and visual style.
- Make the platform suitable for my portfolio and learning journey.

---

# Next Steps

- [ ] Define the first course: `Build a Personal Website Chatbot`.
- [ ] Convert Anna chatbot docs ([[memory]], [[agent-instruction]], [[work-instruction]]) into lesson pages.
- [ ] Design a course landing page layout.
- [ ] Design a lesson page layout with sidebar and `Up Next` section.
- [ ] Create reusable Markdown frontmatter for courses and lessons.
- [ ] Create a website section for learning paths.
- [ ] Add AI assistant support later.

## Related Notes

- [[AGENTS]]
- [[agent-instruction]]
- [[memory]]
- [[work-instruction]]
