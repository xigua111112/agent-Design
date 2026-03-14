# ref-color-system.md
← Back to [SKILL.md](../SKILL.md)

---

## Primitive Scales (_Primitives collection)

### Gray Light Mode (浅色模式原始色阶)

| Stop | Hex | Usage |
|------|-----|-------|
| 25 | `#F5F5F6` | Sidebar background |
| 50 | `#F9FAFB` | Page secondary background |
| 100 | `#F0F1F1` | Tertiary bg, active state, divider |
| 200 | `#ECECED` | Secondary border |
| 300 | `#CECFD2` | Primary border |
| 400 | `#94969C` | Disabled fg, quinary |
| 500 | `#85888E` | Placeholder, muted text |
| 600 | `#61646C` | Tertiary text |
| 700 | `#333741` | Secondary text, nav items |
| 800 | `#1F242F` | Strong text, hover states |
| 900 | `#161B26` | Primary text, **primary button bg** |
| 950 | `#0C111D` | Darkest, primary button hover |

### Gray Dark Mode (深色模式原始色阶)

| Stop | Hex | Note |
|------|-----|------|
| 25 | `#FAFAFA` | ← different from Light-25 |
| 50 | `#F5F5F6` | ← different from Light-50 |
| 100–950 | same hex as Light 100–950 | — |

### Brand (品牌色 = Gray Light 镜像)

Brand stops mirror Gray Light exactly. `Brand/600` = `#61646C`, `Brand/900` = `#161B26`.

### Status Palettes

| Palette | 500 | 600 | Usage |
|---------|-----|-----|-------|
| Error | `#F04438` | `#D92D20` | Destructive, form error |
| Warning | `#F79009` | `#DC6803` | Caution states |
| Success | `#17B26A` | `#079455` | Positive states |

### Extended Palettes (24 色板)

Gray-blue · Gray-cool · Gray-modern · Gray-neutral · Gray-iron · Gray-true · Gray-warm ·
Moss · Green-light · Green · Teal · Cyan · Blue-light · Blue · Blue-dark ·
Indigo · Violet · Purple · Fuchsia · Pink · Rose · Orange-dark · Orange · Yellow

每个 12 stops（25→950），所有值存储于 Figma `_Primitives` 变量集合。

---

## Semantic Tokens — CSS Variables (Light Mode)

```css
:root {
  /* Background */
  --bg-primary:       #ffffff;
  --bg-secondary:     #F9FAFB;   /* gl-50 */
  --bg-tertiary:      #F0F1F1;   /* gl-100 */
  --bg-sidebar:       #F5F5F6;   /* gl-25 */
  --bg-active:        #F0F1F1;   /* gl-100 */
  --bg-brand-primary: #161B26;   /* gl-900 — primary button */
  --bg-brand-hover:   #0C111D;   /* gl-950 — primary button hover */

  /* Text */
  --text-primary:     #161B26;   /* gl-900 */
  --text-secondary:   #333741;   /* gl-700 */
  --text-tertiary:    #61646C;   /* gl-600 */
  --text-muted:       #85888E;   /* gl-500 */
  --text-placeholder: #85888E;   /* gl-500 */
  --text-white:       #ffffff;

  /* Border */
  --border-primary:   #CECFD2;   /* gl-300 */
  --border-secondary: #ECECED;   /* gl-200 */
  --border-tertiary:  #F0F1F1;   /* gl-100 */

  /* Status */
  --error-fg:   #D92D20;  --error-bg:   #FEF3F2;
  --warning-fg: #B54708;  --warning-bg: #FFFAEB;
  --success-fg: #067647;  --success-bg: #ECFDF3;
}
```

---

## Semantic Token Reference Table

| Category | Token | Light Value | Dark Value |
|----------|-------|-------------|------------|
| **Text** | text-primary-900 | gl-900 | gd-50 |
| | text-secondary-700 | gl-700 | gd-300 |
| | text-tertiary-600 | gl-600 | gd-400 |
| | text-muted / placeholder | gl-500 | gd-500 |
| **Border** | border-primary | gl-300 | gd-700 |
| | border-secondary | gl-200 | gd-800 |
| **Background** | bg-primary | white | gl-950 |
| | bg-secondary | gl-50 | gd-900 |
| | bg-tertiary | gl-100 | gd-800 |
| | bg-brand-primary | gl-900 | br-500 |
| **Foreground** | fg-primary-900 | gl-950 | gd-25 |
| | fg-brand-primary | br-600 | br-500 |
| | fg-error / warning / success | status-600 | status-500 |

---

## Color Usage Rules

```css
/* CORRECT — semantic tokens */
background: var(--bg-primary);
color: var(--text-secondary);
border: 1px solid var(--border-primary);

/* WRONG — raw primitives in component styles */
background: #F9FAFB;
color: #333741;
```

```tsx
// CORRECT — Tailwind semantic
<div className="bg-background text-foreground">
<p className="text-muted-foreground">
<span className="text-destructive">Error</span>

// WRONG — raw Tailwind colors
<div className="bg-gray-50 text-gray-700">
<div className="bg-blue-500 text-white">
```

---

## Dark Mode

- **Mechanism:** Class-based (`.dark` on `<html>`) via `next-themes`
- **Provider:** `<ThemeProvider attribute="class" defaultTheme="system" enableSystem>`
- **Rule:** Never use `dark:` color overrides — semantic tokens handle both modes automatically.
- **Figma:** Switch `1. Color modes` collection between `Light-mode` / `Dark-mode`

---

## Button Color Decision

```css
/* Primary button — confirmed gl-900 (#161B26), hover gl-950 (#0C111D) */
.btn-primary       { background: #161B26; color: #fff; }
.btn-primary:hover { background: #0C111D; }
/* WCAG contrast ratio > 11:1 on white bg — AAA compliant */

/* Secondary button */
.btn-secondary       { background: var(--bg-secondary); border: 1px solid var(--border-primary); }
.btn-secondary:hover { background: var(--bg-active); }
```

---

## Icon Color by Context

| Context | Color token |
|---------|-------------|
| Nav item (default) | `--text-secondary` `#333741` |
| Nav item (active) | `--text-primary` `#161B26` |
| Header actions | `--text-muted` `#85888E` |
| Destructive | `--error-fg` `#D92D20` |
| Success indicator | `--success-fg` `#067647` |
