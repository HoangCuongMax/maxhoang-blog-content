# Website Database

This folder is the GitHub-backed content database for `maxhoang.com.au`.

The website reads Markdown records from these folders:

- [[09 Website Database/Blog]]
- [[09 Website Database/Awards]]
- [[09 Website Database/Events]]
- [[09 Website Database/Photos]]
- [[09 Website Database/Short Videos]]

## Publishing Rules

- Use `published: true` to show a record on the website.
- Use `published: false` or `status: draft` to keep it private.
- Keep one website record per Markdown file.
- Put public images in `99 Attachments/Images` and reference them by vault path, or use a full public URL.

## Common Fields

```yaml
---
title: Example Title
slug: example-title
published: true
featured: true
sortOrder: 1
tags: [AI, Data]
---
```

