# ref-component-states.md
← Back to [SKILL.md](../SKILL.md)

---

## State Types

### Disabled

```tsx
className="disabled:pointer-events-none disabled:opacity-50"
```

### Invalid / Error

```tsx
<Field data-invalid>
  <Input aria-invalid />
  <FieldDescription>Invalid email address.</FieldDescription>
</Field>
```

### Active

```tsx
data-active={isActive}    // Sidebar menu items
data-state="active"       // Tabs trigger
```

### Loading

```tsx
<Button disabled>
  <Spinner data-icon="inline-start" />
  Saving...
</Button>

<Skeleton className="h-4 w-3/4" />
```

### Focus

```tsx
"focus-visible:ring-[3px] focus-visible:ring-ring/50 focus-visible:border-ring outline-hidden"
```

### Hover

```tsx
"hover:bg-accent hover:text-accent-foreground"   // Menu items
"hover:bg-primary/90"                             // Primary button
```

---

## Data Attribute Reference

| Attribute | Purpose |
|-----------|---------|
| `data-slot` | Component ID & CSS targeting |
| `data-state` | `open` / `closed` / `active` |
| `data-active` | Active flag (sidebar items) |
| `data-invalid` | Error/invalid flag (Field) |
| `data-disabled` | Disabled flag |
| `data-icon` | Icon position: `inline-start` / `inline-end` |
