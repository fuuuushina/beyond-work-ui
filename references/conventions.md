# Beyond Work — Code & Project Conventions

Source: `src/ts/neui/` (primary app)

---

## Repository structure

```
code/
└── src/ts/
    ├── neui/          ← PRIMARY app (new UI — use this for all new features)
    ├── bport/         ← Legacy Bulma UI (do not add new features here)
    ├── packages/      ← Shared libraries (@bw/ws-api, @beyondwork/sandbox-types, …)
    └── config/        ← Shared tooling config (@bw/prettier-config, …)
```

**Package manager:** pnpm (v10.6.5)  
**Monorepo:** Turbo (turbo.json at root)  
**Build system:** Bazel (for CI/CD)

---

## neui app structure

```
src/ts/neui/src/
├── app/                     ← Next.js App Router
│   ├── layout.tsx           ← Root layout (Inter font, NuqsAdapter, metadata)
│   ├── globals.css          ← Design tokens, Tailwind base
│   └── w/                   ← Main authenticated workspace
│       ├── layout.tsx
│       ├── explore/         ← Home / discovery
│       ├── studio/          ← Editor / studio
│       ├── work/            ← Work management
│       │   ├── active/
│       │   ├── available/
│       │   └── overview/
│       ├── blocks/          ← Workblock management
│       ├── client/          ← Client portal
│       ├── partner/         ← Partner management
│       ├── spaces/          ← Orgs / spaces
│       ├── app/[stream_id]/ ← Individual stream
│       └── admin/           ← Admin section
├── domains/
│   ├── shadcn/ui/           ← shadcn/ui component library
│   └── app/                 ← App-level components (atoms / molecules / organisms)
├── components/
│   └── ai-elements/         ← AI-specific UI elements
└── packages/                ← Internal utilities / hooks / types
```

---

## Routing conventions (Next.js App Router)

| Pattern | Meaning |
|---|---|
| `app/w/[route]/page.tsx` | A top-level workspace route |
| `app/w/[route]/[id]/page.tsx` | Dynamic nested route |
| `app/w/[route]/layout.tsx` | Shared layout for a route group |
| `(group)/` | Route group — affects layout without adding URL segment |
| `[[...path]]` | Optional catch-all (deep nested navigation) |

**New route checklist:**
1. Create `src/app/w/<route-name>/page.tsx`
2. Add a `layout.tsx` if the route needs its own chrome
3. Register in the navbar if it needs a nav link (`app-navbar.tsx`)
4. Add any route params to the Nuqs schema if they live in the URL

---

## File naming

| Item | Convention | Example |
|---|---|---|
| Components | kebab-case `.tsx` | `user-profile-card.tsx` |
| Pages | `page.tsx` (fixed by Next.js) | `page.tsx` |
| Layouts | `layout.tsx` (fixed) | `layout.tsx` |
| Hooks | `use-` prefix, kebab-case | `use-workspace.ts` |
| Server actions | `actions.ts` or `<name>.action.ts` | `update-profile.action.ts` |
| API routes | `route.ts` (Next.js convention) | `route.ts` |
| Utilities | kebab-case `.ts` | `format-date.ts` |
| Types | kebab-case `.types.ts` or inline | `workspace.types.ts` |

---

## Component organisation

Follows **atoms → molecules → organisms** within `src/domains/app/`:

| Level | What goes here |
|---|---|
| `atoms/` | Primitives: logo, avatar, icon wrapper — no internal state or data fetching |
| `molecules/` | Composed from atoms: command palette, error dialog — limited local state OK |
| `organisms/` | Full sections: navbar, sidebar, layout — may fetch data, own significant state |

For **feature-level** components, co-locate them with their route:
```
app/w/blocks/
├── page.tsx
├── _components/         ← private to this route (leading underscore = not a route)
│   ├── block-list.tsx
│   └── block-card.tsx
└── _hooks/
    └── use-blocks.ts
```

---

## State management

| Layer | Tool | Use case |
|---|---|---|
| URL state | **Nuqs** (`useQueryState`) | Filters, tabs, pagination, selected IDs |
| Local component | `useState` / `useReducer` | UI-only ephemeral state |
| Global app state | **Jotai** atoms | Cross-component shared state |
| Server state / cache | **TanStack Query** | Data fetching, caching, mutations |
| Immutable updates | **Immer** / `use-immer` | Complex nested state updates |

**Prefer URL state for anything shareable** (so users can copy a link and see the same view).

---

## Data fetching

Use **TanStack Query** for all server data:

```tsx
// Fetching
const { data, isLoading } = useQuery({
  queryKey: ['blocks', workspaceId],
  queryFn: () => fetchBlocks(workspaceId),
})

// Mutations
const { mutate } = useMutation({
  mutationFn: updateBlock,
  onSuccess: () => queryClient.invalidateQueries({ queryKey: ['blocks'] }),
})
```

Next.js Server Actions are acceptable for simple form submissions. For complex workflows,
use TanStack Query mutations to get loading / error / cache-invalidation for free.

---

## Forms

Use **Formik** for forms with validation:

```tsx
const formik = useFormik({
  initialValues: { name: '' },
  onSubmit: async (values) => { … },
})
```

For simple single-field inline edits, plain controlled `useState` is fine.

---

## Styling rules

1. **Tailwind only** — no inline styles, no CSS modules, no separate `.css` files per component.
2. **Use `cn()` helper** to merge Tailwind classes conditionally (re-exports `clsx` + `tailwind-merge`).
3. **Semantic tokens over raw values** — `text-muted-foreground` not `text-gray-500`.
4. **Responsive:** use Tailwind breakpoints (`sm:`, `md:`, `lg:`). The md breakpoint is 1024px
   and lg is 1440px (overridden in website2 tailwind config — check neui's config for app values).
5. **Dark mode** is class-based (`.dark`). All colors use the CSS variable system so dark mode
   is automatic as long as you use semantic tokens.

---

## TypeScript conventions

- Strict mode is on — no `any`, no `@ts-ignore` without a comment explaining why.
- Prefer `interface` for object shapes, `type` for unions / mapped types.
- Co-locate types with their feature; only promote to a shared types file when used in 3+ places.
- Import order (enforced by ESLint): external packages → internal aliases → relative imports.

---

## Testing

**Framework:** Vitest (`vitest.config.ts` at package root)

- Unit tests: co-located `.test.ts` / `.test.tsx` files
- No Playwright / e2e tests in the codebase currently

---

## Key dependencies (quick reference)

| Package | Version | Purpose |
|---|---|---|
| `next` | 15.5.18 | Framework |
| `react` | 19.0.0 | UI library |
| `tailwindcss` | 4.1.18 | Styling |
| `jotai` | latest | Global state |
| `@tanstack/react-query` | 5.72.2 | Server state |
| `@tanstack/react-table` | 8.21.3 | Data tables |
| `nuqs` | 2.8.2 | URL state |
| `formik` | 2.4.6 | Forms |
| `motion` | 12.8.0 | Animations |
| `framer-motion` | 12.20.2 | Animations (legacy) |
| `lucide-react` | latest | Icons |
| `date-fns` | 3.6.0 | Date utilities |
| `immer` / `use-immer` | latest | Immutable state |
| `class-variance-authority` | latest | Component variants |
| `clsx` + `tailwind-merge` | latest | Class merging (`cn()`) |
