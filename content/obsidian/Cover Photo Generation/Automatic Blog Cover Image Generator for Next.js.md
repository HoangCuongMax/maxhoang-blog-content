
## Purpose

Create an automatic blog cover image generator for a Next.js website.

The generator should read blog post metadata from Markdown or MDX frontmatter. If a post does not have a cover image, it should automatically create a clean, modern blog cover image and save it into the website's public folder.

This is designed for a personal AI / technology blog using a clean, minimal website style.

---

## Main Requirements

### 1. Read Blog Post Metadata

The generator should read metadata from Markdown or MDX frontmatter.

Required frontmatter fields:

```yaml
title: "Agent Memory, Skills, and Browser Automation"
description: "A personal note on persistent agent memory, reusable agent skills, and browser automation."
date: "2026-05-19"
tags: ["AI", "Agents", "Automation"]
slug: "agent-memory-skills-browser-automation"
cover: "auto"
```

The script should read:

- `title`
- `description`
- `date`
- `tags`
- `slug`
- `cover`
- optional `coverTemplate`

---

### 2. Generate Cover Only When Needed

If the blog post already has a real cover image, the script should skip it.

Example:

```yaml
cover: "/images/my-manual-cover.png"
```

If the blog post has no cover image, or the cover is set to `auto`, the script should generate a cover.

Example:

```yaml
cover: "auto"
```

or:

```yaml
# no cover field
```

---

### 3. Save Generated Cover Image

Generated covers should be saved into:

```bash
/public/blog-covers/[slug].png
```

Example:

```bash
/public/blog-covers/agent-memory-skills-browser-automation.png
```

---

## Design Style

The generated image should use a clean modern AI / technology style that matches the website.

### Visual Requirements

The cover should include:

- Minimal layout
- Soft background
- Large readable title
- Small category or tag pill
- Date or reading time
- Random abstract graphic

### Possible Abstract Graphics

The graphic can include:

- AI / network nodes
- Grid dots
- Gradient blobs
- Code lines
- Browser window cards
- Automation-style cards
- Simple geometric shapes

---

## Image Size

The generated image must be:

```text
1200 x 630 px
```

This size works well for:

- Blog cover image
- Open Graph image
- Social sharing preview
- LinkedIn sharing preview

---

## Recommended Technology

Use Node.js with a reliable image generation library.

Recommended stack:

```bash
satori + sharp
```

Also useful:

```bash
gray-matter
fast-glob
reading-time
react
```

### Install Dependencies

```bash
npm install gray-matter fast-glob satori sharp reading-time react
```

---

## Reusable Cover Templates

Create 3 reusable templates.

### 1. Clean Tech

Best for:

- AI
- Coding
- Automation
- Agents
- Technical tutorials

Style:

- Light grey or soft blue background
- Black or dark navy title
- Blue accent
- Abstract nodes, browser cards, or grid dots

---

### 2. Dark AI

Best for:

- AI engineering
- Technical deep dives
- Agent systems
- Automation architecture

Style:

- Dark navy background
- White title
- Blue / purple accent
- Glowing grid, nodes, or code panel

---

### 3. Minimal Editorial

Best for:

- Personal notes
- Learning logs
- Reflection posts
- Blog essays

Style:

- Off-white background
- Large clean title
- Subtle accent color
- Simple geometric graphic

---

## Template Selection Logic

If the blog post has a `coverTemplate`, use that template.

Example:

```yaml
coverTemplate: "dark-ai"
```

Supported values:

```text
clean-tech
dark-ai
minimal-editorial
```

If no template is specified, randomly select one template.

However, the randomness must be deterministic based on the post slug.

This means:

- Same slug = same cover every time
- The cover does not randomly change every time the script runs
- The website keeps a consistent look

---

## Suggested Folder Structure

```bash
my-nextjs-site/
├── content/
│   └── blog/
│       └── agent-memory-skills-browser-automation.md
├── public/
│   └── blog-covers/
│       └── agent-memory-skills-browser-automation.png
├── scripts/
│   └── generate-covers.js
├── assets/
│   └── fonts/
│       ├── Inter-Regular.ttf
│       └── Inter-Bold.ttf
└── package.json
```

---

## NPM Command

Add this command to `package.json`:

```json
{
  "scripts": {
    "generate:covers": "node scripts/generate-covers.js"
  }
}
```

Run the generator with:

```bash
npm run generate:covers
```

---

## Frontend Helper

Add a helper function so the website can automatically use the generated cover when no manual cover exists.

```js
export function getPostCover(post) {
  if (post.cover && post.cover !== "auto") return post.cover;
  return `/blog-covers/${post.slug}.png`;
}
```

Example usage in a blog card:

```jsx
<Image
  src={getPostCover(post)}
  alt={post.title}
  width={1200}
  height={630}
/>
```

---

## Safety Rules

The generator should be added as a separate script.

It should not:

- Break the existing website structure
- Rewrite blog post files
- Change routing
- Change the blog UI
- Change the content system
- Modify existing manual cover images

It should only write generated images to:

```bash
/public/blog-covers
```

Before making major structural changes, Codex should ask first.

---

## Codex Instruction

Use this prompt for Codex:

```text
Create an automatic blog cover image generator for my Next.js website.

Requirements:

1. Read blog post metadata from Markdown or MDX frontmatter:
   - title
   - description
   - date
   - tags
   - slug

2. If the post does not have a cover image, automatically generate one.

3. Save the generated image into:
   /public/blog-covers/[slug].png

4. Use a clean modern AI/tech style that matches my website:
   - minimal layout
   - soft background
   - large readable title
   - small category/tag pill
   - date or reading time
   - random abstract graphic such as nodes, grid dots, gradient blobs, code lines, or browser cards

5. Use Node.js with a reliable image generation library such as:
   - satori + sharp
   - or canvas
   - or @vercel/og for dynamic Open Graph images

6. Make sure the image size is 1200 x 630 px for blog cover and Open Graph sharing.

7. Add 3 reusable templates:
   - clean-tech
   - dark-ai
   - minimal-editorial

8. Randomly select one template if no template is specified.

9. Use deterministic randomness based on the blog slug, so the same post always gets the same cover.

10. Do not break the existing website structure. Add the generator as a separate script.

11. Add an npm command:
   "generate:covers": "node scripts/generate-covers.js"

12. Before making major structural changes, ask me first.
```

---

## Example Blog Frontmatter

```yaml
---
title: "Agent Memory, Skills, and Browser Automation"
description: "A personal note on persistent agent memory, reusable agent skills, and browser automation as the next practical AI layer."
date: "2026-05-19"
tags: ["AI", "Agents", "Automation"]
slug: "agent-memory-skills-browser-automation"
cover: "auto"
coverTemplate: "clean-tech"
---
```

---

## Expected Output

After running:

```bash
npm run generate:covers
```

The script should create:

```bash
/public/blog-covers/agent-memory-skills-browser-automation.png
```

The generated cover should look like a clean AI / tech editorial image with:

- Title
- Tag pill
- Date
- Reading time
- Abstract graphic
- Consistent website branding
