# Beyond Work — Design Tokens

Source: `src/ts/neui/src/app/globals.css`

---

## Color system

The neui app uses **Tailwind CSS v4** with **OKLch color space** for perceptually uniform colors.
All colors are exposed as CSS custom properties and consumed via Tailwind semantic classes.

### Semantic color tokens

| CSS variable | Tailwind class | Usage |
|---|---|---|
| `--background` | `bg-background` | Page background |
| `--foreground` | `text-foreground` | Primary text |
| `--card` | `bg-card` | Card surfaces |
| `--card-foreground` | `text-card-foreground` | Text on cards |
| `--popover` | `bg-popover` | Popover / dropdown surfaces |
| `--popover-foreground` | `text-popover-foreground` | Text in popovers |
| `--primary` | `bg-primary` / `text-primary` | Primary actions |
| `--primary-foreground` | `text-primary-foreground` | Text on primary bg |
| `--secondary` | `bg-secondary` | Secondary surfaces |
| `--secondary-foreground` | `text-secondary-foreground` | Text on secondary bg |
| `--muted` | `bg-muted` | Muted / subdued backgrounds |
| `--muted-foreground` | `text-muted-foreground` | De-emphasized text |
| `--accent` | `bg-accent` | Accent highlights |
| `--accent-foreground` | `text-accent-foreground` | Text on accent |
| `--destructive` | `bg-destructive` / `text-destructive` | Danger / delete actions |
| `--border` | `border-border` | Default borders |
| `--input` | `border-input` | Form input borders |
| `--ring` | `ring-ring` | Focus rings |

### Chart tokens (for data visualisation)

`--chart-1` through `--chart-5` — use sequentially for multi-series charts.

### Sidebar-specific tokens

| CSS variable | Usage |
|---|---|
| `--sidebar` | Sidebar background |
| `--sidebar-foreground` | Sidebar text |
| `--sidebar-primary` | Active item in sidebar |
| `--sidebar-primary-foreground` | Text on active sidebar item |
| `--sidebar-accent` | Hover state in sidebar |
| `--sidebar-accent-foreground` | Text on hovered sidebar item |
| `--sidebar-border` | Sidebar border |
| `--sidebar-ring` | Focus ring inside sidebar |

### Beyond Work brand colors

These come from `src/website2/tailwind.config.ts` (marketing site) and inform the product palette:

| Name | Value | Usage |
|---|---|---|
| `bw-green` | `#c3e86b` | Primary CTA, highlight |
| `bw-green-muted` | `#686745` | Muted green, icons |
| `bw-pink` | `#ff80ff` | Secondary accent |
| `bw-purple` | `#8074db` | Tertiary accent |
| `bw-grey-light` | `#e5e4eb` | Light backgrounds |
| `bw-grey` | `#9c99ae` | Neutral text / borders |
| `bw-grey-dark` | `#252528` | Dark surfaces |
| `bw-grey-darker` | `#313239` | Darker surfaces |

---

## Border radius

```css
--radius: 0.75rem   /* base radius */
```

Tailwind utilities derived from this variable:
- `rounded-sm` → `calc(var(--radius) - 4px)`
- `rounded-md` → `calc(var(--radius) - 2px)`
- `rounded-lg` → `var(--radius)`
- `rounded-xl` → `calc(var(--radius) + 4px)`

---

## Shadows

| Variable | Value | Usage |
|---|---|---|
| `--shadow-sm` | `0px 0.5px 1px 0px rgba(0,0,0,0.08)` | Subtle lift (chips, badges) |
| `--shadow-md` | `0px 1px 2px 0px rgba(0,0,0,0.12)` | Cards, dropdowns |
| `--shadow-lg` | `0px 4px 12px rgba(0,0,0,0.08)` | Modals, popovers |

---

## Layout tokens

| CSS variable | Value | Usage |
|---|---|---|
| `--navbar-height` | `3.5rem` | Top navigation bar height |
| `--main-card-padding` | `0.4rem` | Inner padding on main content cards |
| `--main-card-topbar-height` | `2.5rem` | Height of in-card top bars |
| `--container-compact` | `360px` | Compact column width |

### Layout utility classes

```css
.h-navbar            /* height: var(--navbar-height) */
.h-navbar-layout     /* height: calc(100vh - var(--navbar-height)) */
.h-main-card         /* height: calc(100% - var(--main-card-topbar-height) - ...) */
.max-h-navbar-layout /* max-height: calc(100vh - var(--navbar-height)) */
```

---

## Typography

Beyond Work uses a **two-font system** from the identity assets:

| Role | Font | Weight | Usage |
|------|------|--------|-------|
| **Display / Headlines** | **Syne** | 600–700 | Hero titles, section headers, brand moments |
| **Body / UI** | **Inter** | 400–600 | All product UI, labels, body copy |

- Syne files: `assets/fonts/Syne.zip` (from identity kit)
- Inter files: `assets/fonts/Inter.zip` (from identity kit)
- **Scale:** Tailwind default typographic scale (`text-xs` through `text-4xl`)
- **Weights:** `font-normal` (400), `font-medium` (500), `font-semibold` (600), `font-bold` (700)

**Brand principle (from whitepaper):** "Light weight for body, heavier for headlines. A serious display face for moments of weight." Syne is the display face — use it for hero sections, onboarding titles, marketing pages. Never use it for dense product UI (data tables, forms, labels).

### Loading fonts (Next.js App Router)
```tsx
import { Inter, Syne } from 'next/font/google'

const inter = Inter({ subsets: ['latin'], variable: '--font-inter' })
const syne  = Syne({ subsets: ['latin'], variable: '--font-syne', weight: ['600', '700'] })
```

---

## Brand Aesthetic Principles

From the May 2026 strategic whitepaper — these are hard constraints, not suggestions:

| ✅ Do | ❌ Never |
|-------|---------|
| Enterprise infrastructure feel (Stripe, Linear, Datadog) | Consumer chatbot / startup pitch aesthetic |
| Near-black + white as primaries | Gradients (no decorative gradients) |
| `#c3e86b` lime/chartreuse accent **used sparingly** | Glow effects |
| Restrained secondary accents | Glassmorphism |
| Minimal shadows (only for functional clarity) | Drop shadows beyond what's structurally required |
| Real working-environment photography | Generic happy office workers or abstract AI imagery |
| Sans-serif, modern, neutral body type | Kinetic typography that doesn't serve content |

**The core visual test:** "Does this look like serious enterprise infrastructure, or like it's racing for attention?"

---

## Animations

Custom keyframes defined in globals.css:

- `bwlogo1`, `bwlogo2` — logo animation sequences
- Standard Tailwind animations (`animate-spin`, `animate-pulse`, `animate-bounce`)
- Motion library (`framer-motion` / `motion`) for page transitions and interactive elements

---

## Scrollbar utilities

```css
.scrollbar-hide    /* hides scrollbar while keeping scroll functional */
.scrollbar-default /* restores default scrollbar */
```
