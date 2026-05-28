---
title: Google Design implementation plan
type: implementation-plan
status: active
published: false
project: maxhoang-website
tags:
  - maxhoang-website
  - ui
  - ux
  - google-design
  - material-design
---

# Google Design implementation plan

## Source

This plan applies the principles from `Google_Design.md` to the MaxHoang.com.au website and the `ui-ux-improvement-agent` workflow.

The goal is not to copy Google branding. The goal is to apply the deeper Material / Google Design mindset: clarity, task focus, consistent systems, adaptive layout, accessible defaults, useful motion, and a trustworthy AI assistant.

## Current website read

Main app surface: `MaxHoang_Notion`.

Relevant files:

- `app/globals.css` - global tokens, theme colours, prose styles, media placeholders, Anna surface styling.
- `app/layout.tsx` - site shell, sidebar, footer, Anna chatbot mounting.
- `components/workspace-sidebar.tsx` - desktop sidebar navigation and content category links.
- `components/blog-index.tsx` - home/blog listing, tag filters, featured post, empty state.
- `components/chatbot/ChatbotWidget.tsx` - minimized Anna prompt and quick question UI.
- `components/chatbot/ChatbotWindow.tsx` - full Anna assistant, onboarding, sources, suggestions, feedback, admin mode.
- `app/about/page.tsx`, `app/contact/page.tsx`, route pages - major content layouts.
- `components/ui/*` - reusable shadcn-style primitives.

Existing strengths:

- Semantic CSS variables already support light and dark themes.
- Sidebar gives the site an app-like information architecture.
- Buttons, cards, badges, inputs, sheets, and tooltips already exist as reusable primitives.
- Anna has source links, suggestions, feedback, reduced-motion handling, and useful onboarding.
- Blog cards and media placeholders already use structured surfaces instead of random decoration.

Current gaps against the Google Design note:

- Colour roles are only partially Material-like. The current warm tan/orange palette is distinctive, but it can read more editorial than clean product UI.
- Design tokens exist for colour and radius, but spacing, elevation, motion, and type roles are not explicitly named.
- The homepage is currently a blog index only, so first-time visitors do not get a clear "what can Max help with?" path before content browsing.
- Anna's minimized widget is visually prominent and can compete with page reading, especially on mobile.
- Cards, badges, and controls use mixed emphasis. Some secondary actions visually compete with primary actions.
- Empty, loading, and error states exist in places, but they are not yet standardized across pages.
- Page sections use similar card patterns, but the hierarchy across Blog, About, GitHub, Contact, Obsidian, and Daily Journal can be tightened.

## Design direction

Use a Google-inspired product direction:

- Light, neutral surfaces with one confident primary accent and one Anna-specific accent.
- Strong hierarchy: page title, short help text, primary next action, scannable content.
- Material-style colour roles: `primary`, `onPrimary`, `primaryContainer`, `secondary`, `tertiary`, `surface`, `surfaceVariant`, `outline`, `error`, `onSurface`, `onSurfaceVariant`.
- Subtle Material Expressive moments for Anna, onboarding, empty states, and success feedback.
- Clean developer / AI portfolio tone: practical, calm, trustworthy, lightly warm.
- Keep current content-first website identity. Do not turn it into a decorative landing page.

## Implementation phases

### Phase 1 - Token foundation

Purpose: make the design system explicit before changing many screens.

Tasks:

- Refactor `app/globals.css` theme variables into clearer Material-style roles while preserving compatibility with existing shadcn variables.
- Add token comments for colour roles, surface roles, radius, shadow, motion duration, and easing.
- Introduce `--surface`, `--surface-variant`, `--on-surface`, `--on-surface-variant`, `--primary-container`, `--on-primary-container`, `--tertiary`, and `--outline` aliases.
- Reduce the one-note warm palette by moving large backgrounds closer to neutral off-white / neutral dark and using warm tones only as supporting accents.
- Keep `--anna` and `--anna-soft`, but tune them as a controlled tertiary/accent role instead of letting purple dominate the chat UI.
- Add shadow tokens: `--shadow-1`, `--shadow-2`, `--shadow-3`.
- Add motion tokens: `--duration-fast`, `--duration-medium`, `--duration-slow`, `--ease-standard`, `--ease-emphasized`.

Acceptance checks:

- Light and dark mode both remain readable.
- Body background, cards, sidebars, inputs, and popovers still map correctly.
- Contrast remains strong for primary text, muted text, buttons, and focus rings.

### Phase 2 - Component alignment

Purpose: make repeated UI elements behave like a system.

Tasks:

- Update `components/ui/button.tsx` so filled, tonal, outlined, ghost, destructive, and icon button styles match the Material hierarchy.
- Review `components/ui/card.tsx`, `badge.tsx`, `input.tsx`, `textarea.tsx`, and `sidebar.tsx` for consistent radius, border, hover, focus, disabled, and selected states.
- Add or document a "tonal" button/badge pattern if current variants are not enough.
- Keep touch targets near 44-48px for mobile-critical controls, especially sidebar trigger, chatbot controls, and form actions.
- Standardize focus rings so keyboard navigation is visible and attractive.
- Avoid heavy shadows for normal cards. Use borders or tonal surfaces; reserve stronger elevation for overlays, menus, and the chatbot panel.

Acceptance checks:

- Primary action is visually obvious in each major section.
- Secondary actions do not overpower filled actions.
- Keyboard focus is visible on links, buttons, inputs, chatbot controls, and sidebar items.

### Phase 3 - Navigation and information architecture

Purpose: help visitors understand where they are and where to go next.

Tasks:

- Refine `components/workspace-sidebar.tsx` labels to be clearer and more visitor-friendly.
- Consider renaming `Obsidian` to `Notes` in visible navigation while keeping route path unchanged.
- Consider renaming `Presentation Slide` to `Slides`.
- Keep active states strong enough to identify the current page at a glance.
- Make category chips in the sidebar read as quick filters/shortcuts, not decorative badges.
- Coordinate with `side-bar-navigation-agent` before implementation.

Acceptance checks:

- A first-time visitor can identify Blog, Notes, About, GitHub, Connect, and Contact quickly.
- The sidebar remains compact when collapsed and clear when expanded.
- Mobile navigation remains reachable and does not conflict with Anna.

### Phase 4 - Homepage / blog-first experience

Purpose: keep the blog index useful while adding a clearer first-visit path.

Tasks:

- Improve `components/blog-index.tsx` hero so it explains Max's value in one glance, not only "Practical data notes."
- Add a compact path selector near the top: `Read`, `Explore projects`, `Ask Anna`, `Contact`.
- Keep blog filtering visible but reduce chip clutter if there are too many tags.
- Give the featured post a clearer Material-style surface with one primary action.
- Improve the empty tag state with a direct recovery action such as "View all posts".
- Consider search only if content volume justifies it; do not add a fake search pattern without implementation.

Acceptance checks:

- Homepage answers: who is this, what is here, what should I do next?
- Returning readers can still reach latest posts immediately.
- Mobile layout keeps hero, filters, and featured post readable without crowding.

### Phase 5 - Anna assistant refinement

Purpose: make Anna helpful and trustworthy without interrupting reading.

Tasks:

- In `components/chatbot/ChatbotWidget.tsx`, reduce the minimized widget's visual dominance on content pages.
- Prefer a compact floating action plus one short contextual message, with the full quick input appearing only after deliberate hover/focus/tap.
- Keep suggested prompts action-oriented: "Show Max's AI projects", "What services does Max offer?", "Read his AI learning journey", "How can I contact Max?"
- In `components/chatbot/ChatbotWindow.tsx`, simplify onboarding copy and reduce the number of competing cards.
- Keep source links and feedback, but use clearer Material groupings: Sources, Suggestions, Feedback.
- Make unknown/error responses honest and useful.
- Ensure all chatbot motion respects `prefers-reduced-motion`.
- Coordinate with `personal-chatbot-agent`, `motion-effect-agent`, and `accessibility-review-agent`.

Acceptance checks:

- Anna is easy to open but does not cover important page content by default.
- New visitors understand what Anna can do within 5 seconds.
- Chat controls are usable on mobile with the keyboard open.
- Sources, suggestions, feedback, and errors are visually distinct but not noisy.

### Phase 6 - Page-level polish

Purpose: apply the same structure across major routes.

Tasks:

- Review `app/about/page.tsx` for hero hierarchy, motion intensity, card density, and mobile readability.
- Review `app/contact/page.tsx` for form clarity, helper text, validation, and primary action prominence.
- Review `app/github/page.tsx` for project card hierarchy, tags, stats, and external-link clarity.
- Review `app/obsidian/page.tsx` and note detail pages for reading comfort, filtering, empty states, and long-line control.
- Review `app/daily-journal/page.tsx` as a private/content workflow surface; keep it calmer and more utility-focused.
- Standardize section headers: short label, clear heading, one useful sentence, optional action.

Acceptance checks:

- Each page has a clear first action and a clear content hierarchy.
- Cards are used for repeated content and framed tools, not as decoration around every section.
- Text length, spacing, and button layout work at mobile, tablet, and desktop widths.

### Phase 7 - State system

Purpose: make loading, empty, error, and success states feel intentional.

Tasks:

- Create small reusable state patterns if repetition appears: empty state, loading skeleton, inline error, success confirmation.
- Use simple icon + title + short explanation + recovery action.
- Add skeletons for data-heavy lists where pages can load slowly.
- Improve contact and chatbot error messages so they explain what happened and what to do next.

Acceptance checks:

- No blank-looking screen when content is missing or loading.
- Empty states guide visitors back to useful paths.
- Error messages do not blame the user and include a next step.

### Phase 8 - Accessibility and responsive QA

Purpose: verify the design works for real conditions.

Tasks:

- Run keyboard navigation checks for sidebar, tag filters, cards, forms, chatbot widget, and chatbot window.
- Check colour contrast in light and dark modes.
- Verify touch targets on mobile, especially floating Anna, close/expand buttons, sidebar trigger, tag chips, and forms.
- Verify text does not overflow cards, buttons, or chatbot bubbles.
- Check zoom and narrow mobile widths.
- Ensure motion-heavy surfaces pause or simplify under reduced-motion settings.

Acceptance checks:

- `npm run lint`, `npm run typecheck`, and `npm run build` pass after app code changes.
- Desktop and mobile screenshots show no overlapping UI.
- Important tasks can be completed with keyboard only.

## Suggested implementation order

1. Token foundation in `app/globals.css`.
2. Component primitives in `components/ui/*`.
3. Sidebar labels/states with the sidebar agent.
4. Homepage/blog index path and empty state.
5. Anna minimized widget and chat window simplification.
6. About, Contact, GitHub, Notes, and Daily Journal page polish.
7. Shared empty/loading/error states.
8. Accessibility and responsive QA pass.

## Agent workflow updates

For future UI/UX improvement-agent work:

- Start with `Google_Design.md` and this plan before visible UI changes.
- Prefer scoped component changes before route rewrites.
- When changing shared tokens or primitives, inspect multiple pages before and after.
- Coordinate cross-cutting changes with sidebar, motion, accessibility, performance, and personal-chatbot agents.
- Log meaningful changes in this folder's `work-log.md` and the parent `../work-log.md`.

## Definition of done

A Google-inspired improvement is done when:

- The user can understand the page goal quickly.
- Primary and secondary actions are visually distinct.
- Colours, type, radius, spacing, and states come from shared tokens.
- Mobile, desktop, light mode, and dark mode all work.
- The UI is accessible by keyboard and readable with strong contrast.
- Anna helps exploration without blocking the main website.
- The change has been verified with lint, typecheck, build, and responsive visual checks when app code changed.
