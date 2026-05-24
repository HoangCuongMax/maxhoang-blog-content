---
title: Blog cover generator - work log
type: work-log
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - cover-generator
  - work-log
---

# Work log

Short dated entries. **Newest first.**

## 2026-05-25

- Regenerated all blog post covers with `npm run generate:covers -- --force`.
- Created static 1200x630 PNG covers for Anna, Common NLP Questions and Answers, and both Data Analyst/Data Analysis portfolio posts.
- Refreshed the existing Agent Memory cover into the current `max-journal` style.
- Fixed the portfolio post frontmatter titles by quoting `#1` and `#3` titles so YAML does not treat the number markers as comments.

## 2026-05-24

- Finished the cover generator implementation direction in `MaxHoang_Notion/scripts/generate-covers.mjs`.
- Standardised generated covers on one `max-journal` visual system with deterministic accent colours.
- Updated generation rules so YouTube/Vimeo values in cover fields are replaced by real static PNG covers.
- Improved the website fallback media cover so posts without generated assets still display a consistent branded cover, and video watch URLs are not treated as images in rendering or metadata.
- Added generated `mediaAltText` updates and documented current behaviour in memory/plan notes.
- Could not run `npm run generate:covers`, lint, or build in this shell because `node`/`npm` are not available on PATH.

## 2026-05-20

- Added cover-generator sub-agent docs and reporting link to the main `Maxhoang.com.au` website agent.
