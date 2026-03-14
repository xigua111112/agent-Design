# ref-layout-system.md
← Back to [SKILL.md](../SKILL.md)

---

## Four Core Layout Models

### Model A: Sidebar + Content (Dashboard/App)

```
Nav Sidebar (fixed, 256px, z-30)
  SidebarHeader   — Logo + workspace switcher
  SidebarContent  — Nav groups + menu items (scrollable)
  SidebarFooter   — User avatar + settings
SidebarInset (margin-left: 256px, flex-col)
  SiteHeader (sticky top-0, z-10, h-56px) — Trigger | Breadcrumb | Search | Actions
  Main (flex-1, overflow-y-auto, bg-secondary)
    Page title row  — h1 + action buttons
    Stats cards grid (4-col)
    Chart section (2-col: chart + supplementary)
    Data table (full width, with pagination)
```

### Model B: Sidebar + Docs (Documentation)

```
DocsSidebar (fixed, calc(var(--spacing) * 72))
SidebarInset
  2-column grid on lg+ screens
  Sidebar nav | Content area
```

### Model C: Full-width Content (Showcase/Marketing)

```
PageHeader (hero, title, description)
PageNav (tabs/filters)
container-wrapper > container > content sections
```

---

## Container System

```tsx
// Two-level wrapping
<div className="container-wrapper">   {/* mx-auto w-full px-2 */}
  <div className="container">          {/* mx-auto max-w-[1400px] px-4 lg:px-8 */}
    {children}
  </div>
</div>
```

---

## Sidebar Configuration

| Variable | Value | Purpose |
|----------|-------|---------|
| `--sidebar-width` | `256px` (16rem) | Desktop nav sidebar |
| `--sidebar-width-mobile` | `288px` (18rem) | Mobile sidebar sheet |
| `--sidebar-width-icon` | `48px` (3rem) | Collapsed icon-only mode |

**Sidebar Variants:** `sidebar` (default) · `floating` (border + shadow) · `inset`

**Collapsible Modes:** `offcanvas` (slide out) · `icon` (collapse to icons) · `none`

**Mobile:** Auto-converts to Sheet. Toggle: `Cmd+B` / `Ctrl+B`

---

## Grid Patterns

```tsx
// Dashboard card grid (container query responsive)
<div className="@container/main grid grid-cols-1 gap-4 px-4 lg:px-6
  @xl/main:grid-cols-2 @5xl/main:grid-cols-4">

// Standard responsive grid
<div className="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-4">

// Chart + supplement two-column
<div className="grid grid-cols-[1fr_360px] gap-4">
```

---

## Page Section Flow (Model A)

```
SiteHeader (sticky, z-10, h-56px)
  SidebarTrigger | Breadcrumb | Spacer | Search | IconActions | Avatar
Main (bg-secondary, px-7, py-7)
  Page Title Row  — display-2 + subtitle + action buttons
  Stats Cards     — 4-col grid, gap-4
  Chart Section   — 2-col grid (chart + model usage)
  Data Table      — card with header, table, pagination
```

---

## Layering Patterns (Z-Index)

```tsx
// Sticky header
<header className="sticky top-0 z-10 flex h-14 items-center border-b bg-background/90 backdrop-blur-sm">

// Fixed sidebar
<aside className="fixed inset-y-0 z-30 flex h-svh w-[256px] flex-col border-r bg-sidebar">

// Dialog overlay + content
<div className="fixed inset-0 z-50 bg-black/50" />
<div className="fixed top-1/2 left-1/2 z-50 -translate-x-1/2 -translate-y-1/2" />
```

---

## Padding Conventions

| Context | Value |
|---------|-------|
| Container | `px-4 lg:px-8` |
| Card internal | `px-6 py-6` |
| Sidebar header/footer | `p-2` / `p-3` |
| Page sections (main) | `px-7 py-7` |
| Table cells | `px-4 py-3` |
| Nav items | `px-2 py-1.5` |
