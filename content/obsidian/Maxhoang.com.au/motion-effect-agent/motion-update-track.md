---
title: Motion Update Website Track
type: implementation-track
status: active
published: false
project: maxhoang-website
tags:
  - motion
  - animation
  - website-update
  - blog
---

# Motion Update Website Track

## Goal

Install and apply Motion for React to the blog experience on `maxhoang.com.au`.

The animation should make the blog feel smoother and more polished without distracting from reading.

## Source

- Motion docs: https://motion.dev/docs
- React install docs: https://motion.dev/docs/react-installation

## Implementation Scope

- [x] Install `motion` package in `MaxHoang_Notion`.
- [x] Add reusable Motion reveal components.
- [x] Animate the blog index header.
- [x] Animate the events section on the blog index.
- [x] Animate the featured blog card.
- [x] Add staggered reveal animation to the blog post list.
- [x] Add subtle hover/tap motion to blog cards.
- [x] Animate the blog detail page title/header.
- [x] Animate the blog cover image.
- [x] Animate media/gallery and related post sections.
- [x] Respect reduced-motion preferences.
- [ ] Visually review animation on desktop.
- [ ] Visually review animation on mobile.

## Animation Rules

- Use subtle entry animation only.
- Prefer `opacity`, `y`, and small hover movement.
- Avoid heavy layout animation.
- Avoid animating every paragraph.
- Keep blog reading calm and readable.
- Respect reduced motion.

## Files Updated

In `MaxHoang_Notion`:

- `package.json`
- `package-lock.json`
- `components/motion/reveal.tsx`
- `components/blog-index.tsx`
- `app/blog/[slug]/page.tsx`

## Verification Checklist

- [x] `npm run lint`
- [x] `npm run build`
- [ ] Check `/blog`
- [ ] Check one `/blog/[slug]` page
- [ ] Check tag filtering still works
- [ ] Check reduced-motion mode does not use movement-heavy animation

## Future Ideas

- Add small transition to related cards.
- Add scroll progress indicator for blog detail pages.
- Add animated table-of-contents highlight.
- Add view-transition style page transitions later if useful.
