# ref-component-architecture.md
← Back to [SKILL.md](../SKILL.md)

---

## 1. CVA Variants — Full Pattern

```tsx
import * as React from "react"
import { cva, type VariantProps } from "class-variance-authority"
import { cn } from "@/lib/utils"

const componentVariants = cva("base-classes", {
  variants: {
    variant: { default: "...", outline: "..." },
    size: { default: "...", sm: "..." },
  },
  defaultVariants: { variant: "default", size: "default" },
})

function Component({ className, variant, size, ...props }:
  React.ComponentProps<"element"> & VariantProps<typeof componentVariants>) {
  return (
    <element
      data-slot="component-name"
      className={cn(componentVariants({ variant, size, className }))}
      {...props}
    />
  )
}
```

---

## 2. cn() Utility

```tsx
import { clsx } from "clsx"
import { twMerge } from "tailwind-merge"

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs))
}
```

---

## 3. data-slot

Every component has `data-slot="component-name"` for CSS targeting.

```tsx
// Allows parent selectors to target children
[&_[data-slot='card-header']]:px-0
```

---

## 4. Compound Components

```tsx
export {
  Card, CardHeader, CardFooter, CardTitle, CardAction, CardDescription, CardContent
}

export {
  Dialog, DialogTrigger, DialogPortal, DialogClose, DialogOverlay, DialogContent,
  DialogHeader, DialogFooter, DialogTitle, DialogDescription
}
```

---

## 5. asChild / render Pattern

```tsx
// Radix UI style
<DialogTrigger asChild>
  <Button>Open</Button>
</DialogTrigger>

// Base UI style
<DialogTrigger render={<Button />}>
  Open
</DialogTrigger>
```

---

## 6. Context Pattern

```tsx
const SidebarContext = React.createContext<SidebarContextProps | null>(null)

function useSidebar() {
  const ctx = React.useContext(SidebarContext)
  if (!ctx) throw new Error("useSidebar must be used within SidebarProvider")
  return ctx
}
```
