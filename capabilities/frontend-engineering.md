---
name: frontend-engineering
type: capability
version: 0.1
owner: cto
tags: [agent-os, capability, frontend, nextjs, react, ui]
date: 2026-05
status: draft
primary_consumer: cto
changelog:
  - version: 0.1
    date: 2026-05
    note: Initial draft
---

# Frontend Engineering

## Purpose
Defines frontend architecture standards — component design, state
management, API integration, accessibility, and performance. Ensures
the Full Stack Developer builds a consistent, maintainable UI layer
and that UX decisions made by the Product Lead are implemented correctly.

## When to Load
Load for any session involving frontend architecture, component design,
state management decisions, UI performance review, or frontend
implementation standards.

## Framework Conventions
Assumes Next.js (App Router) unless overridden by ADR in project
grounding doc.

- Use **Server Components** by default — opt into Client Components
  only when interactivity requires it
- **App Router** over Pages Router for all new work
- Co-locate components with their routes — avoid deep import trees
- Keep pages thin — business logic belongs in hooks or services,
  not in page components

## Component Architecture
- One component per file; filename matches component name
- **Presentational vs. container split:** presentational components
  receive props and render only; containers handle data fetching
  and state
- Props must be typed — no `any` in TypeScript
- Avoid prop drilling beyond 2 levels — use context or state manager
- Components are testable in isolation — no hidden dependencies

## State Management
| State Type | Approach |
|---|---|
| Server data (fetch, cache) | React Query / SWR — not useState |
| UI state (modals, toggles) | useState / useReducer |
| Global app state | Zustand or React Context — not Redux unless justified |
| Form state | React Hook Form |

Choose the simplest tool that solves the problem. Do not reach for
global state when local state works.

## API Integration
- All API calls go through a typed service layer — components never
  call `fetch` directly
- Handle all three states: loading, error, success — no silent failures
- Use optimistic updates for actions the user expects to be instant
- Never expose API keys or tokens in client-side code

## Accessibility Baseline
Every UI component ships meeting these minimums:
- Semantic HTML — use the right element for the job
- All interactive elements keyboard-navigable
- Images have descriptive `alt` text
- Color contrast meets WCAG AA (4.5:1 for body text)
- Forms have associated labels

## Performance Standards
- **Core Web Vitals targets:** LCP < 2.5s, CLS < 0.1, INP < 200ms
- Lazy load images and below-the-fold components
- No unused dependencies in the client bundle
- Run Lighthouse before marking any page as done

## Sources
- Next.js documentation (nextjs.org/docs) — App Router, Server Components, conventions
- React documentation (react.dev) — component patterns, hooks, state management
- WCAG 2.1 (w3.org/WAI/standards-guidelines/wcag) — accessibility baseline
- Google Core Web Vitals (web.dev/vitals) — LCP, CLS, INP performance targets
- Vercel frontend patterns and Next.js best practices (vercel.com/docs)

## Anti-Patterns
- Client Components where Server Components would work
- Direct `fetch` calls inside components
- Prop drilling beyond 2 levels
- `any` types in TypeScript
- Skipping loading and error states
- Shipping UI without accessibility baseline
- Global state for data that only one component needs
