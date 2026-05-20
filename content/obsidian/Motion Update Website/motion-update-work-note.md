---
title: Motion Update Website Work Note
type: work-note
status: active
published: true
project: maxhoang-website
tags:
  - motion
  - animation
  - work-log
  - blog
---

# Motion Update Website Work Note

This note records Codex work for the Motion animation update on the website.

## 2026-05-20

- Created Motion update tracking folder and notes.
- Installed the `motion` npm package in the `MaxHoang_Notion` Next.js app.
- Added reusable Motion client components:
  - `MotionReveal`
  - `MotionStagger`
  - `MotionStaggerItem`
- Applied animation to the blog index:
  - Header reveal
  - Events section reveal
  - Featured post reveal and hover lift
  - Staggered post list reveal
  - Subtle card hover/tap motion
- Applied animation to blog detail pages:
  - Back button reveal
  - Title/header reveal
  - Cover image reveal and hover lift
  - Video/gallery reveal
  - Article body reveal
  - Related posts reveal
- Used reduced-motion support so users who prefer less animation avoid movement-heavy effects.
- Verified with:
  - `npm run lint`
  - `npm run build`
- Build passed with the same sandbox remote-fetch warnings seen in previous builds.
- Blog routes now include the Motion runtime, so their first-load JS size increased as expected.

## Notes

- Animation is intentionally subtle.
- The blog should feel smoother, not like a motion demo.
- The implementation keeps the blog pages as server components and places animation in a small client wrapper.
