# Beyond Work — Identity Assets Catalog

All assets live in `assets/` at the root of this skill.
Reference them in code via their path relative to the project's `public/` folder
(copy the relevant files into `public/brand/` in the neui project).

---

## Logos

### When to use which variant

| Variant | File | Use when |
|---------|------|---------|
| **Logomark** (mark only) | `assets/logo/positive/Logomark.svg` | Favicons, app icons, small spaces, dark-on-light |
| **Logotype** (wordmark only) | `assets/logo/positive/Logotype.svg` | When the mark is already present nearby |
| **Combination Horizontal** | `assets/logo/positive/Logo_CombinationHorizontal.svg` | Default for headers, navbars, footers |
| **Combination Vertical** | `assets/logo/positive/Logo_CombinationVertical.svg` | Splash screens, onboarding, centered layouts |
| **Logomark ® (registered)** | `assets/logo/positive/Logomark_Registred.svg` | Legal/official documents, external comms |

### Negative (white) variants — use on dark backgrounds

| File | Use when |
|------|---------|
| `assets/logo/negative/Logomark_White.svg` | Dark headers, dark panels, over photos |
| `assets/logo/negative/Logo_CombinationHorizontal_White.svg` | Dark navbar |
| `assets/logo/negative/Logo_CombinationVertical_White.svg` | Dark splash/onboarding |
| `assets/logo/negative/Logotype_White.svg` | Dark background, wordmark only |
| `assets/logo/negative/Logomark_Registred_White.svg` | Dark background, legal use |

### Logo usage rules
- **Never recolor** the logo — use positive (dark) on light, negative (white) on dark. No other colors.
- **Minimum clear space**: equal to the height of the "B" in the wordmark on all sides.
- **Never stretch, rotate, add effects, or apply drop shadows** to the logo.
- The existing `BWLogoMark` React component at `src/ts/neui/src/domains/app/atoms/bw-logo-mark.tsx` renders the logomark path inline — use it for UI where SVG file loading is impractical.

---

## Icons

Custom Beyond Work icons — distinct from Lucide icons. Use for feature illustrations,
empty states, and brand moments. **Do not use as navigation icons** (use Lucide for that).

All files are in `assets/icons/`. Each icon comes in up to 3 color variants:

| Suffix | Color | Use on |
|--------|-------|--------|
| *(none)* | Neutral dark | Light backgrounds |
| `_dark` | Dark / `#1f1d1a` | Light backgrounds, emphasis |
| `_green` | BW green `#c3e86b` | Dark backgrounds, highlights |

### Icon catalog

| Icon | Files | Concept |
|------|-------|---------|
| **Atomic** | `Ico_atomic.svg`, `Ico_atomic_dark.svg`, `Ico_atomic_green.svg` | Core logic / primitive |
| **Authoring** | `Ico_authoring_dark.svg`, `Ico_authoring_1_dark.svg` | Content creation, editing |
| **Arrow Up** | `Ico_arrow_up.svg`, `Ico_arrow_up_dark.svg`, `Ico_arrow_up_green.svg` | Progression, export |
| **Circle Arrow Right** | `Ico_circle_arrow_right.svg`, `..._dark.svg`, `..._green.svg` | Navigation, next step |
| **Cross Square** | `Ico_cross_square.svg`, `..._dark.svg`, `..._green.svg` | Close, remove, cancel |
| **Flow** | `Ico_flow_dark.svg` | Workflow, pipeline |
| **Intelligence** | `Ico_intelligence_dark.svg` | AI, reasoning, insights |
| **Star** | `Ico_star.svg`, `Ico_star_dark.svg`, `Ico_star_green.svg` | Favorites, quality, highlight |
| **Timeline** | `Ico_timeline_dark.svg` | Scheduling, history, sequence |
| **Workblock** | `Ico_workblock_dark.svg` | Core BW concept — work units |

### Using icons in React/Next.js
```tsx
// Prefer inline SVG for color control via currentColor
import WorkblockIcon from '@/public/brand/icons/Ico_workblock_dark.svg'

// Or as an img tag for static use
<img src="/brand/icons/Ico_flow_dark.svg" alt="Flow" className="h-6 w-6" />
```

---

## Patterns

Decorative SVG patterns for backgrounds, section dividers, and brand texture.
All files in `assets/patterns/`.

| File | Description | Use case |
|------|-------------|---------|
| `bw_pattern_truchet_fillLoose.svg` | Truchet tile pattern, loose fill, dark | Section backgrounds, hero texture |
| `bw_pattern_truchet_fillLoose_white.svg` | Same, white variant | Dark section backgrounds |
| `bw_patterns_truchet_fillTight.svg` | Truchet tile, tight fill, dark | Dense texture, cards |
| `bw_patterns_truchet_fillTight_white.svg` | Same, white variant | Dark cards |
| `bw_pattern_truchet_lines.svg` | Truchet outline only, dark | Subtle background |
| `bw_pattern_truchet_lines_white.svg` | Same, white variant | Dark subtle background |
| `bw_pattern_dotGrid.svg` | Dot grid, dark | Technical / data feel |
| `bw_pattern_dotGrid_white.svg` | Same, white variant | Dark panels |

### Pattern usage rules
- Use patterns at **low opacity** (10–20%) as texture, never as primary visual
- Never use patterns over body text — only behind empty sections or large visual areas
- Prefer SVG `<pattern>` element for responsive tiling over `background-image`

```tsx
// Responsive SVG pattern background
<div className="relative overflow-hidden">
  <img
    src="/brand/patterns/bw_pattern_dotGrid_white.svg"
    className="absolute inset-0 h-full w-full object-cover opacity-10 pointer-events-none"
    aria-hidden="true"
  />
  {/* content */}
</div>
```

---

## Motion

| File | Description |
|------|-------------|
| `assets/motion/Spinner.gif` | BW branded loading spinner |

Use the spinner for full-page loading states where the standard Tailwind `animate-spin` doesn't feel branded enough. For component-level loading, prefer the skeleton approach.

---

## Fonts

| Font | File | Role |
|------|------|------|
| **Syne** | `assets/fonts/Syne.zip` | Display / headlines — weight 600–700 |
| **Inter** | `assets/fonts/Inter.zip` | Body / UI — weight 400–600 |

Both are available on Google Fonts. Prefer `next/font/google` for loading in Next.js (no self-hosting needed). The zip files are provided for offline or self-hosted scenarios.
