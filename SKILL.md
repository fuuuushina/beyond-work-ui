---
name: beyond-work-ui
description: >
  Design system and UI/UX conventions for the Beyond Work application (repo: bwllaming/code).
  USE THIS SKILL whenever implementing a feature, component, page, or any UI element for Beyond Work.
  Triggers: "add a page", "create a component", "implement a feature", "build a UI", "new route",
  "new view", "new modal", "new sidebar", anything referencing the neui or bport app, any work on
  src/ts/neui or src/ts/bport. Load this skill before writing a single line of code — it defines
  the tokens, components, patterns, and file conventions that keep the codebase consistent.
---

# Beyond Work — UI Skill

This skill documents the design system, component library, and code conventions used in the
Beyond Work application. Always read the relevant reference file(s) before implementing.

## Reference files — when to load each

| File | Load when… |
|------|-----------|
| `references/design-tokens.md` | Choosing colors, spacing, radius, shadows, typography, animations, or brand principles |
| `references/components.md` | Using or creating a UI component (button, card, dialog, sidebar, …) |
| `references/conventions.md` | Creating files, routes, hooks, state, or any structural code |
| `references/assets-catalog.md` | Using logos, brand icons, patterns, fonts, or motion assets |
| `references/deck-visual-style.md` | Creating or designing a Beyond Work slide deck / presentation |

Load all four for a greenfield feature. Load selectively for targeted changes.

## Identity assets

Brand assets (logos, icons, patterns, fonts, motion) live in `assets/` at the root of this skill.
See `references/assets-catalog.md` for the full catalog with usage rules.

**Key assets at a glance:**
- **Logos** — `assets/logo/positive/` (dark on light) and `assets/logo/negative/` (white on dark)
- **Icons** — `assets/icons/` — 21 custom BW icons (atomic, workblock, flow, intelligence, timeline…)
- **Patterns** — `assets/patterns/` — truchet and dot-grid SVG patterns
- **Fonts** — Syne (display/headings) + Inter (body/UI) — both in `assets/fonts/`
- **Motion** — `assets/motion/Spinner.gif` — branded loading spinner

## App context

The primary UI app lives at `src/ts/neui/`. A legacy Bulma-based app (`src/ts/bport/`) exists
but new features go into **neui** unless explicitly told otherwise.

**Stack:**
- Next.js 15 · App Router · React 19 · TypeScript 5.8
- Tailwind CSS v4 (OKLch color space) · shadcn/ui · Radix UI primitives
- Jotai (atomic state) · TanStack Query · Nuqs (URL state)
- CVA (Class Variance Authority) for component variants
- Lucide React icons · Framer Motion / Motion animations

## Quick rules (always apply)

1. **Never hardcode colors.** Use CSS variables (`var(--primary)`, `var(--muted-foreground)`, …)
   or Tailwind semantic classes (`bg-primary`, `text-muted-foreground`, …). See design-tokens.md.

2. **Reach for shadcn/ui first.** Check `src/ts/neui/src/domains/shadcn/ui/` before building
   anything from scratch. See components.md for the full list.

3. **Follow the domain folder structure.** New pages go under `src/ts/neui/src/app/w/`, new
   shared components under the appropriate domain. See conventions.md.

4. **Support both light and dark mode.** All tokens have both `:root` and `.dark` variants — never
   use hard-coded light-only values.

5. **Use CVA for components with variants.** Don't build ad-hoc className strings.
