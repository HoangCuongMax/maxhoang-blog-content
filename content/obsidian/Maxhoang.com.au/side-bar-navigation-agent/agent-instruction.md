---
title: Sidebar navigation - agent instruction
type: agent-instruction
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - sidebar
  - navigation
---

# Agent instruction - Sidebar navigation

This sub-agent owns the website sidebar and primary navigation behaviour for MaxHoang.com.au. It reports to the main website agent in `../AGENTS.md`.

## Scope

- Maintain the left sidebar navigation, labels, icons, grouped links, content badges, action controls, footer CTA, and active-route behaviour.
- Maintain the sidebar primitive when layout, collapse, mobile sheet, keyboard shortcut, or cookie persistence changes are required.
- Coordinate with other sub-agents when their features add navigation entries or sidebar actions.

## Behaviour rules

- Keep navigation clear and predictable. Do not add links that duplicate the same destination without a clear reason.
- Preserve active states for parent routes and nested routes.
- Keep the collapsed icon mode useful with tooltips.
- Keep the mobile sidebar usable as a sheet with accessible labels.
- Keep the `Push content` action visibly stateful: idle, pushing, success, and error.
- Avoid putting dense content in the sidebar; it should help visitors move around the site quickly.

## Accessibility and UX

- Every navigation item should have readable text in expanded mode and a meaningful tooltip in collapsed mode.
- Icons should support labels, not replace them as the only meaning.
- Keyboard users must be able to reach links and controls.
- Do not remove the screen-reader labels on sidebar controls.
- Watch for text truncation in the header, buttons, and footer.

## Quality bar

- Verify desktop expanded, desktop collapsed, and mobile sheet states after meaningful sidebar changes.
- Verify active state on `/`, `/blog`, nested blog routes, `/obsidian`, nested Obsidian routes, `/about`, `/github`, `/connect`, and `/contact` when route logic changes.
- Run app lint/build for code changes when practical.
