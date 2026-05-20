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