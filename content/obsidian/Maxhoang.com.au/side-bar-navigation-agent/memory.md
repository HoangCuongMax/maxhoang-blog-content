---
title: Sidebar navigation - memory
type: project-memory
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - sidebar
  - navigation
  - memory
---

# Memory - Sidebar navigation

## Parent

- Main website agent: `../AGENTS.md`

## Stable paths

- Website app: `/Users/hoangcuong/Library/Mobile Documents/iCloud~md~obsidian/Documents/Max Hoang Blog/MaxHoang_Notion`
- Sidebar agent folder: `maxhoang-blog-content/content/obsidian/Maxhoang.com.au/side-bar-navigation-agent`

## Key app files

| Area | Path |
|---|---|
| Product sidebar | `MaxHoang_Notion/components/workspace-sidebar.tsx` |
| Sidebar primitive and provider | `MaxHoang_Notion/components/ui/sidebar.tsx` |
| Site layout mount point | `MaxHoang_Notion/app/layout.tsx` |
| Navigation labels and link data | `MaxHoang_Notion/lib/site-config.ts` |
| Sidebar theme tokens | `MaxHoang_Notion/app/globals.css` |
| Push content endpoint used by sidebar action | `MaxHoang_Notion/app/api/push-content/route.ts` |

## Current structure

`app/layout.tsx` wraps the site with `SidebarProvider`, renders `WorkspaceSidebar`, then renders page content inside `SidebarInset`. It also sets `--sidebar-width` to `18rem`.

`WorkspaceSidebar` renders:

- Header: logo/home link, "Max Hoang Journal" LinkedIn link, site tagline, mobile trigger.
- Pages group: links from `pageLinks`.
- Content group: badges from `categoryLinks`.
- Actions group: `Push content` button calling `/api/push-content` and refreshing the router.
- Footer: "AI & data" badge, professional headline, Contact button.

## Navigation data

Current `pageLinks` in `lib/site-config.ts`:

- `/` - Blog, icon `blog`, active paths `/` and `/blog`.
- `/obsidian` - Obsidian, icon `obsidian`.
- `/about` - About me, icon `home`.
- `/github` - GitHub, icon `github`.
- `/connect` - Connect, icon `connect`.
- `/contact` - Contact, icon `contact`.

Current `categoryLinks`:

- `/` - Writing
- `/obsidian` - Notes
- `/github` - Code
- `/connect` - Social

## Sidebar primitive behaviour

`components/ui/sidebar.tsx` provides:

- Desktop expanded/collapsed state.
- Mobile sheet state.
- Cookie persistence with `sidebar_state`.
- Keyboard shortcut `Cmd/Ctrl+B`.
- `SidebarTrigger`, `SidebarInset`, groups, menu items, tooltips, and skeleton helper.
- Collapsed icon width `3.5rem`.

## Design tokens

Sidebar colors are defined in `app/globals.css` using CSS variables:

- `--sidebar`
- `--sidebar-foreground`
- `--sidebar-primary`
- `--sidebar-primary-foreground`
- `--sidebar-accent`
- `--sidebar-accent-foreground`
- `--sidebar-border`
- `--sidebar-ring`
