# ref-interaction-patterns.md
← Back to [SKILL.md](../SKILL.md)

---

## Overlay Components

| Component | Trigger | Use Case |
|-----------|---------|----------|
| `Dialog` | Click | Focused task / input |
| `AlertDialog` | Click | Destructive confirmation |
| `Sheet` | Click | Side panel (details, filters) |
| `Drawer` | Click | Mobile bottom panel |
| `Popover` | Click | Small contextual content |
| `Tooltip` | Hover | Quick info on hover |

**All overlays require a Title** (`sr-only` if visually hidden).

---

## Command Palette

```tsx
// Cmd+K global shortcut
<CommandDialog open={open} onOpenChange={setOpen}>
  <CommandInput placeholder="搜索..." />
  <CommandList>
    <CommandEmpty>No results found.</CommandEmpty>
    <CommandGroup heading="建议">
      <CommandItem>
        <Icon />
        Label
        <CommandShortcut>⌘K</CommandShortcut>
      </CommandItem>
    </CommandGroup>
  </CommandList>
</CommandDialog>
```

---

## Toast (Sonner)

```tsx
toast.success("Changes saved.")
toast.error("Something went wrong.")
toast.warning("Careful!")
toast("Deleted.", { action: { label: "Undo", onClick: () => undoDelete() } })
toast.promise(fn, { loading: "Saving...", success: "Done!", error: "Failed." })
```

---

## Card & Component Composition

### Card Structure

```tsx
<Card>
  <CardHeader>
    <CardTitle>Team Members</CardTitle>
    <CardDescription>Manage your team.</CardDescription>
    <CardAction><Button variant="outline" size="sm">Add</Button></CardAction>
  </CardHeader>
  <CardContent>...</CardContent>
  <CardFooter><Button>Invite</Button></CardFooter>
</Card>
```

### Icon Rules

```tsx
// In Button — data-icon, no sizing classes
<Button><SearchIcon data-icon="inline-start" />Search</Button>
<Button>Next<ArrowRightIcon data-icon="inline-end" /></Button>

// In MenuItem — no sizing classes
<DropdownMenuItem><SettingsIcon />Settings</DropdownMenuItem>

// Pass as component object, not string
<StatusBadge icon={CheckIcon} />    // ✅
<StatusBadge icon="check" />        // ❌
```

### Icon Visual Spec (SVG inline)

```
Size in nav items       : 16×16px, stroke-width 1.5, stroke-linecap round
Size in header          : 18×18px, stroke-width 1.5
Size in buttons         : 14×14px (secondary/ghost), 13×13px (small)
Size in tool cards      : 16×16px
Corner radius (container): 6–8px
```

### Avatar

```tsx
<Avatar className="size-8">
  <AvatarImage src="/avatar.png" alt="User" />
  <AvatarFallback>YL</AvatarFallback>   {/* Always required */}
</Avatar>
// User avatar gradient: linear-gradient(135deg, gl-600, gl-800), white text
```

### Badge

```tsx
<Badge variant="success">● 成功</Badge>   // success-bg + success-fg
<Badge variant="error">● 失败</Badge>     // error-bg + error-fg
<Badge variant="warning">● 超时</Badge>   // warning-bg + warning-fg
<Badge variant="neutral">○ 排队中</Badge> // bg-tertiary + text-tertiary
// padding: 2px 7–8px, border-radius: full, font: body-1-medium
```

### Stat Card (Dashboard)

```tsx
<div className="stat-card">               // border-radius: xl (12px), border: secondary
  <p className="stat-label">总运行次数</p>  // body-2, text-tertiary
  <p className="stat-value">48,293</p>    // 28px bold, tracking-tight
  <div className="stat-trend up">         // success-fg, or dn = error-fg
    <TrendIcon /> +12.4% <span className="stat-sub">较上月</span>
  </div>
</div>
```
