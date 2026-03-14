---
name: volcengine-design-system
description: "Use this skill when building UI components, pages, or applications that follow the Volcengine (火山引擎) / Huoshan Design System. Triggers include: any request to build dashboards, admin panels, data tables, forms, or UI components using the Volcengine or Huoshan design language; requests involving Volcengine color tokens, typography scale, sidebar layouts, or component patterns. Covers layout models, color system, typography, component architecture, states, interactions, and anti-patterns."
---

# Volcengine Design System Skill

火山引擎设计系统参考规范，基于 Huoshan Design System 标准。圆角 / 字体 / 色彩 token 均已替换为 Huoshan Design System 标准值。

> All design tokens (radius, typography, color) use Volcengine Design System standard values.

---

## Reference Files

| File | Contents |
|------|----------|
| [ref-layout-system.md](reference/ref-layout-system.md) | 4 layout models, container system, sidebar config, grid patterns |
| [ref-color-system.md](reference/ref-color-system.md) | Primitive scales, CSS variables, semantic token table, dark mode |
| [ref-typography.md](reference/ref-typography.md) | Font system, 13-level type scale, typography rules |
| [ref-component-architecture.md](reference/ref-component-architecture.md) | CVA pattern, cn(), data-slot, compound components, context |
| [ref-component-states.md](reference/ref-component-states.md) | Disabled / invalid / active / loading / focus / hover + data attributes |
| [ref-interaction-patterns.md](reference/ref-interaction-patterns.md) | Overlay components, Command palette, Toast (Sonner) |
| [ref-form-system.md](reference/ref-form-system.md) | Form layout, InputGroup, control selection guide, validation |
| [ref-component-taxonomy.md](reference/ref-component-taxonomy.md) | 54 core components by category, 72+ chart variants |

---

## 1. Layout — Quick Summary

**4 Core Models:**
- **Model A** Sidebar + Dashboard (fixed 256px sidebar + sticky header + main)
- **Model B** Sidebar + Docs (2-col grid on lg+)
- **Model C** Full-width / Marketing (container-wrapper > container)

**Container pattern:** two-level `container-wrapper > container` (max-w-[1400px])

**Sidebar widths:** desktop `256px` · mobile `288px` · collapsed icon `48px`

→ Full layout code: [ref-layout-system.md](reference/ref-layout-system.md)

---

## 2. Visual Hierarchy & Z-Index

| Z-Level | Usage |
|---------|-------|
| `z-10` | Sticky headers |
| `z-20` | Sidebar rail |
| `z-30` | Fixed nav sidebar |
| `z-50` | Modal overlays, dialogs, sheets |

**Rule:** Never manually set z-index on Dialog / Sheet / Drawer / Popover / Tooltip — they manage their own stacking.

---

## 3. Spacing — Critical Rules

| Token | Value | Usage |
|-------|-------|-------|
| `gap-2` | 8px | Icon + text |
| `gap-4` | 16px | Between related elements |
| `gap-6` | 24px | Within card sections |
| `gap-8` | 32px | Between major sections |

```tsx
// ✅ CORRECT
<div className="flex flex-col gap-4">
<Avatar className="size-10">

// ❌ WRONG
<div className="space-y-4">      // Never space-y-* / space-x-*
<Avatar className="w-10 h-10">  // Never separate w/h
```

---

## 4. Color — Key Rules

```tsx
// ✅ Semantic tokens (always use)
<div className="bg-background text-foreground">
<p className="text-muted-foreground">

// ❌ Raw colors (never use in components)
<div className="bg-gray-50 text-gray-700">
```

**Primary button:** `bg-[#161B26]` (gl-900) · hover `bg-[#0C111D]` (gl-950) — WCAG AAA

**Dark mode:** Class-based `.dark` via `next-themes`. Never use `dark:` color overrides — semantic tokens handle both modes.

→ Full color tokens & CSS variables: [ref-color-system.md](reference/ref-color-system.md)

---

## 5. Typography — Key Rules

- Display series: negative `letter-spacing` (-0.01em ~ -0.03em)
- Body text: `line-height: 1.5`; multi-line paragraphs use `leading-relaxed`
- Code / data / terminal → `font-mono`
- Use `truncate` not `overflow-hidden text-ellipsis whitespace-nowrap`

→ Full 13-level type scale: [ref-typography.md](reference/ref-typography.md)

---

## 6. Component Architecture — Core Pattern

```tsx
const componentVariants = cva("base-classes", {
  variants: { variant: { default: "...", outline: "..." }, size: { default: "...", sm: "..." } },
  defaultVariants: { variant: "default", size: "default" },
})

function Component({ className, variant, size, ...props }) {
  return <element data-slot="component-name" className={cn(componentVariants({ variant, size, className }))} {...props} />
}
```

→ Full patterns (CVA, cn, compound, context): [ref-component-architecture.md](reference/ref-component-architecture.md)

---

## 7. Component States — Summary

| State | Mechanism |
|-------|-----------|
| Disabled | `disabled:pointer-events-none disabled:opacity-50` |
| Invalid | `<Field data-invalid>` + `aria-invalid` on input |
| Active | `data-active` (sidebar) / `data-state="active"` (tabs) |
| Loading | `<Button disabled><Spinner />` or `<Skeleton>` |
| Focus | `focus-visible:ring-[3px] focus-visible:ring-ring/50` |

→ Full state code + data attribute reference: [ref-component-states.md](reference/ref-component-states.md)

---

## 8. Interaction — Summary

| Component | Use Case |
|-----------|----------|
| `Dialog` | Focused task / input |
| `AlertDialog` | Destructive confirmation |
| `Sheet` | Side panel (details, filters) |
| `Drawer` | Mobile bottom panel |
| `Popover` | Small contextual content |
| `Tooltip` | Quick info on hover |

**All overlays require a `<DialogTitle>`** (use `sr-only` if visually hidden).

→ Full overlay / command palette / toast code: [ref-interaction-patterns.md](reference/ref-interaction-patterns.md)

---

## 9. UI Composition — Card Structure

```tsx
<Card>
  <CardHeader>
    <CardTitle>Title</CardTitle>
    <CardDescription>Description</CardDescription>
    <CardAction><Button variant="outline" size="sm">Action</Button></CardAction>
  </CardHeader>
  <CardContent>...</CardContent>
  <CardFooter><Button>Submit</Button></CardFooter>
</Card>
```

**Icon Rules:**
```tsx
<Button><SearchIcon data-icon="inline-start" />Search</Button>   // ✅
<Button><SearchIcon className="mr-2 size-4" />Search</Button>    // ❌
```

---

## 10. Responsive Design

| Token | Width | Usage |
|-------|-------|-------|
| `sm` | 640px | Small tablets |
| `md` | 768px | Tablets |
| `lg` | 1024px | Desktop |
| `xl` | 1280px | Wide desktop |

Mobile-first. Sidebar auto-converts to Sheet on mobile. Toggle: `Cmd+B` / `Ctrl+B`

---

## 11. Animation & Transitions

Uses `tw-animate-css` (CSS-only, no Framer Motion).

```tsx
"transition-colors"               // hover/focus color changes (default)
"transition-all duration-120"     // button, nav item
duration-100 / 200 / 500          // fast / default / slow
```

---

## 12. Form — Quick Guide

| Need | Component |
|------|-----------|
| Text input | `Input` |
| Dropdown (predefined) | `Select` |
| Searchable dropdown | `Combobox` |
| Boolean (settings) | `Switch` / `Toggle` |
| Boolean (forms) | `Checkbox` |
| Single choice | `RadioGroup` |
| Toggle 2–5 options | `ToggleGroup` |

→ Full form layout & validation: [ref-form-system.md](reference/ref-form-system.md)

---

## 13. Component Taxonomy — Summary

**54 Core Components** across 8 categories: Form & Input (14) · Navigation (6) · Data Display (6) · Overlays (7) · Menus (3) · Feedback (5) · Layout (7) · Utility (4)

→ Full taxonomy + 72+ chart variants: [ref-component-taxonomy.md](reference/ref-component-taxonomy.md)

---

## 14. Anti-Patterns

### Styling

| ❌ Wrong | ✅ Right |
|---------|---------|
| `bg-gray-50 text-gray-700` | `bg-background text-foreground` |
| `space-y-4` | `flex flex-col gap-4` |
| `w-10 h-10` | `size-10` |
| `dark:bg-gray-950` | `bg-background` (semantic token) |
| `overflow-hidden text-ellipsis whitespace-nowrap` | `truncate` |
| `z-50` on Dialog | (Dialog manages its own z-index) |
| Raw hex `#333741` in component | `var(--text-secondary)` |

### Composition

| ❌ Wrong | ✅ Right |
|---------|---------|
| `<SelectItem>` directly in `<SelectContent>` | Wrap in `<SelectGroup>` |
| `<TabsTrigger>` directly in `<Tabs>` | Wrap in `<TabsList>` |
| `<Avatar>` without fallback | Always `<AvatarFallback>` |
| Dialog without `<DialogTitle>` | Include (use `sr-only` if hidden) |
| `<Button isPending>` | `<Button disabled><Spinner />Saving...</Button>` |
| Custom div for empty state | `<Empty><EmptyHeader>...</EmptyHeader></Empty>` |

### Icons

| ❌ Wrong | ✅ Right |
|---------|---------|
| `<SearchIcon className="mr-2 size-4" />` in Button | `<SearchIcon data-icon="inline-start" />` |
| `<SettingsIcon className="size-4" />` in MenuItem | `<SettingsIcon />` |
| `icon="check"` (string) | `icon={CheckIcon}` (component) |

---

## Quick Reference

### Component Selection

| Need | Use |
|------|-----|
| Button/action | `Button` with variant |
| Form inputs | `Input`, `Select`, `Combobox`, `Switch`, `Checkbox`, `Textarea` |
| Toggle 2–5 options | `ToggleGroup` |
| Data display | `Table`, `Card`, `Badge`, `Avatar` |
| Navigation | `Sidebar`, `Breadcrumb`, `Tabs`, `Pagination` |
| Overlays | `Dialog`, `Sheet`, `Drawer`, `AlertDialog` |
| Feedback | `sonner`, `Alert`, `Progress`, `Skeleton` |
| Charts | `Chart` (Recharts wrapper) |
| Empty states | `Empty` |

### Customization Hierarchy

1. **Built-in variants** — `variant="outline"`, `size="sm"`
2. **Semantic color tokens** — `bg-primary`, `text-muted-foreground`
3. **Huoshan CSS variables** — `var(--bg-brand-primary)`, `var(--text-secondary)`
4. **New CVA variant** — Add to component `cva()`
5. **Wrapper component** — Compose primitives into higher-level components
