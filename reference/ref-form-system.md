# ref-form-system.md
← Back to [SKILL.md](../SKILL.md)

---

## Form Layout

```tsx
// Vertical (default)
<FieldGroup>
  <Field>
    <FieldLabel htmlFor="email">Email</FieldLabel>
    <Input id="email" type="email" />
  </Field>
</FieldGroup>

// Horizontal (settings pages)
<Field orientation="horizontal">
  <FieldLabel>Theme</FieldLabel>
  <ToggleGroup>...</ToggleGroup>
</Field>
```

---

## InputGroup

```tsx
<InputGroup>
  <InputGroupInput placeholder="Search..." />
  <InputGroupAddon>
    <Button size="icon"><SearchIcon data-icon="inline-start" /></Button>
  </InputGroupAddon>
</InputGroup>
```

---

## Form Control Selection Guide

| Need | Component |
|------|-----------|
| Text input | `Input` |
| Dropdown (predefined) | `Select` |
| Searchable dropdown | `Combobox` |
| Boolean toggle (settings) | `Switch` / `Toggle` |
| Boolean toggle (forms) | `Checkbox` |
| Single choice (few options) | `RadioGroup` |
| Toggle 2–5 options | `ToggleGroup` |
| Multi-line text | `Textarea` |
| Range/slider | `Slider` |
| OTP/verification | `InputOTP` |

---

## Validation (React Hook Form + Zod)

```tsx
const schema = z.object({ email: z.string().email() })
const form = useForm({ resolver: zodResolver(schema), mode: "onChange" })

<Field data-invalid={!!errors.email}>
  <FieldLabel>Email</FieldLabel>
  <Input aria-invalid={!!errors.email} {...register("email")} />
  {errors.email && (
    <FieldDescription>{errors.email.message}</FieldDescription>
  )}
</Field>
```
