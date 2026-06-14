# Beyond Work — Component Library

Source: `src/ts/neui/src/domains/shadcn/ui/` and `src/ts/neui/src/components/`

---

## shadcn/ui components

All live in `src/ts/neui/src/domains/shadcn/ui/`. Always check here before building from scratch.

| Component | File | Notes |
|---|---|---|
| Accordion | `accordion.tsx` | Radix-based collapsible sections |
| Alert | `alert.tsx` | Info / warning / error banners |
| Alert Dialog | `alert-dialog.tsx` | Destructive confirmation modal |
| Avatar | `avatar.tsx` | User avatar with fallback initials |
| Badge | `badge.tsx` | Small status / label chip |
| Breadcrumb | `breadcrumb.tsx` | Navigation path |
| Button | `button.tsx` | **See full spec below** |
| Button Group | `button-group.tsx` | Joined buttons |
| Calendar | `calendar.tsx` | Date picker calendar |
| Card | `card.tsx` | **See full spec below** |
| Carousel | `carousel.tsx` | Embla-based image / content carousel |
| Checkbox | `checkbox.tsx` | Radix checkbox |
| Collapsible | `collapsible.tsx` | Toggle show/hide sections |
| Command | `command.tsx` | Keyboard-first command menu |
| Command Bar | `command-bar.tsx` | In-page action bar |
| Context Menu | `context-menu.tsx` | Right-click menu |
| Date Time Picker | `date-time-picker.tsx` | Combined date + time input |
| Dialog | `dialog.tsx` | Modal dialog |
| Drawer | `drawer.tsx` | Side / bottom sheet panel |
| Dropdown Menu | `dropdown-menu.tsx` | Trigger + popover menu |
| Empty State | `empty-state.tsx` | Zero-data placeholder |
| File Viewer | `file-viewer.tsx` | Inline file preview |
| Hover Card | `hover-card.tsx` | Rich tooltip on hover |
| Input | `input.tsx` | Text input field |
| Item | `item.tsx` | Generic list / menu item |
| Keyboard | `keyboard.tsx` | Keyboard shortcut display (`⌘K`) |
| Label | `label.tsx` | Accessible form label |
| Menu | `menu.tsx` | Navigation menu primitive |
| Navigation Menu | `navigation-menu.tsx` | Horizontal nav with submenus |
| Pagination | `pagination.tsx` | Page navigation |
| Popover | `popover.tsx` | Floating content panel |
| Progress | `progress.tsx` | Progress bar |
| Radio Group | `radio-group.tsx` | Radio button set |
| Resizable | `resizable.tsx` | Drag-to-resize panels |
| Scroll Area | `scroll-area.tsx` | Custom scrollable container |
| Searchable Popover | `searchable-popover.tsx` | Popover with search input |
| Select | `select.tsx` | Native-feeling select dropdown |
| Separator | `separator.tsx` | Horizontal / vertical divider |
| Sheet | `sheet.tsx` | Side panel / drawer |
| Sidebar | `sidebar.tsx` | **See full spec below** |
| Skeleton | `skeleton.tsx` | Loading placeholder |
| Sonner | `sonner.tsx` | Toast notifications |
| Split Action Button | `split-action-button.tsx` | Button + dropdown split |
| Switch | `switch.tsx` | Toggle switch |
| Table | `table.tsx` | Data table (use with TanStack Table) |
| Tabs | `tabs.tsx` | Tab navigation |
| Toggle | `toggle.tsx` | On/off toggle button |
| Toggle Group | `togglegroup.tsx` | Group of toggle buttons |
| Tooltip | `tooltip.tsx` | Hover tooltip |

---

## Component specs

### Button

File: `src/ts/neui/src/domains/shadcn/ui/button.tsx`

**Variants:**

| Variant | Use case |
|---|---|
| `default` | Primary action |
| `secondary` | Secondary action |
| `destructive` | Delete / irreversible action |
| `outline` | Low-emphasis action |
| `ghost` | Tertiary / icon-only contexts |
| `ghostDark` | Ghost on dark backgrounds |
| `link` | Inline text link |

**Sizes:**

| Size | Dimensions | Use case |
|---|---|---|
| `default` | h-9 px-4 | Standard |
| `xs` | h-6 px-2 text-xs | Dense toolbars |
| `sm` | h-8 px-3 | Compact |
| `lg` | h-10 px-6 | Prominent CTAs |
| `icon` | h-9 w-9 | Square icon button |
| `iconSm` | h-8 w-8 | Small icon button |
| `iconXs` | h-6 w-6 | Tiny icon button |

**Loading state:** pass `loading={true}` — renders a spinner and disables the button.

**Icon support:** place `<LucideIcon />` inside the button; it sizes automatically.

```tsx
// Examples
<Button variant="default">Save</Button>
<Button variant="outline" size="sm">Cancel</Button>
<Button variant="ghost" size="icon"><Trash2 /></Button>
<Button loading={isSaving}>Saving…</Button>
```

---

### Card

File: `src/ts/neui/src/domains/shadcn/ui/card.tsx`

Sub-components: `Card`, `CardHeader`, `CardTitle`, `CardDescription`, `CardAction`, `CardContent`, `CardFooter`

- `CardHeader` uses CSS Grid for auto-layout between title and action.
- `CardAction` is right-aligned (placed inside `CardHeader`).
- Supports container queries.

```tsx
<Card>
  <CardHeader>
    <CardTitle>Title</CardTitle>
    <CardDescription>Subtitle</CardDescription>
    <CardAction><Button size="sm">Edit</Button></CardAction>
  </CardHeader>
  <CardContent>…</CardContent>
  <CardFooter>…</CardFooter>
</Card>
```

---

### Sidebar

File: `src/ts/neui/src/domains/shadcn/ui/sidebar.tsx`

Uses sidebar-specific CSS tokens (`--sidebar`, `--sidebar-primary`, etc. — see design-tokens.md).
Used in `src/ts/neui/src/domains/app/organisms/app-user-sidebar.tsx` as the reference implementation.
Width / collapsed state is controlled via context; don't set widths manually.

---

## AI / custom components

Located in `src/ts/neui/src/components/ai-elements/`

| Component | File | Usage |
|---|---|---|
| Chain of Thought | `chain-of-thought.tsx` | Visualise AI reasoning steps |
| Code Block | `code-block.tsx` | Syntax-highlighted code with copy button |
| Reasoning | `reasoning.tsx` | AI reasoning visualisation |
| Response | `response.tsx` | Streaming markdown response (uses Streamdown) |
| Shimmer | `shimmer.tsx` | Loading shimmer animation |
| Web Preview | `web-preview.tsx` | Inline web content preview |

**CodeBlock usage:** supports `language`, `showLineNumbers`, copy-on-click. Uses Prism.js.
Both light and dark themes are bundled — switch is automatic via `.dark` class.

---

## App-level components

Located in `src/ts/neui/src/domains/app/`

```
atoms/
  bw-logo.tsx        — Full horizontal BW logo
  bw-logo-mark.tsx   — Icon-only logo mark

molecules/
  command-palette.tsx  — Global ⌘K command palette
  error-dialog.tsx     — Standardised error modal

organisms/
  app-layout.tsx           — Root layout wrapper (wrap all pages in this)
  app-navbar.tsx           — Top navigation bar (feature-flagged items)
  app-spaces-shell.tsx     — Spaces container
  app-user-sidebar.tsx     — User profile / settings sidebar
```

---

## Icons

Use **Lucide React** exclusively. Import from `lucide-react`.

```tsx
import { Trash2, Plus, ChevronRight } from 'lucide-react'
```

Size via Tailwind: `<Trash2 className="h-4 w-4" />`. Default icon size in buttons is `h-4 w-4`.

---

## Component creation conventions

When building a **new** component:

1. Place it in the appropriate domain folder (see conventions.md).
2. Use **CVA** (`class-variance-authority`) for variants — do not concatenate class strings.
3. Forward `ref` with `React.forwardRef` if the component wraps an HTML element.
4. Export a typed `Props` interface or use `React.ComponentPropsWithoutRef<'element'>`.
5. Support `className` override via `cn()` (the project's `clsx` + `tailwind-merge` helper).

```tsx
// Pattern for a new component
import { cva, type VariantProps } from 'class-variance-authority'
import { cn } from '@/lib/utils'

const myComponentVariants = cva('base-classes', {
  variants: {
    variant: { default: '…', secondary: '…' },
    size: { sm: '…', default: '…', lg: '…' },
  },
  defaultVariants: { variant: 'default', size: 'default' },
})

interface MyComponentProps
  extends React.HTMLAttributes<HTMLDivElement>,
    VariantProps<typeof myComponentVariants> {}

export function MyComponent({ className, variant, size, ...props }: MyComponentProps) {
  return <div className={cn(myComponentVariants({ variant, size }), className)} {...props} />
}
```
