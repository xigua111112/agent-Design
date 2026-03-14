# ref-typography.md
← Back to [SKILL.md](../SKILL.md)

---

## Font System

```css
--font-sans: 'PingFang SC', -apple-system, system-ui, 'Segoe UI', Helvetica, Arial, sans-serif;
--font-mono: 'Geist Mono', 'SF Mono', 'Fira Code', ui-monospace, monospace;
```

- **Sans** (`--font-sans`): 所有 UI 文字
- **Mono** (`--font-mono`): 代码、数据、终端输出、代码块

---

## Font Weights

| Token | Value | Usage |
|-------|-------|-------|
| Regular | 400 `font-normal` | 正文、描述、表单标签 |
| Medium | 500 `font-medium` | 强调文字、导航项、按钮 |
| SemiBold | 600 `font-semibold` | 标题、CardTitle |
| Bold | 700 `font-bold` | 大标题、重点标注 |

---

## Type Scale (13 Levels)

| Token | Size | Weight | Tailwind | Usage |
|-------|------|--------|----------|-------|
| `display-3` | 36px | 600 | `text-4xl font-semibold tracking-[-0.03em]` | Hero 首屏大标题 |
| `display-2-1` | 32px | 600 | `text-[32px] font-semibold tracking-[-0.02em]` | 页面主标题 |
| `display-2` | 30px | 600 | `text-[30px] font-semibold tracking-[-0.02em]` | 大区块标题 |
| `display-1` | 24px | 600 | `text-2xl font-semibold tracking-[-0.01em]` | Section 标题 |
| `title-3` | 20px | 600 | `text-xl font-semibold` | 子区块标题 |
| `title-2` | 18px | 600 | `text-lg font-semibold` | 卡片标题 |
| `title-1` | 16px | 600 | `text-base font-semibold` | CardTitle、列表项标题 |
| `body-3` | 14px | 400 | `text-sm font-normal` | 正文、描述、表单标签 |
| `body-3-medium` | 14px | 500 | `text-sm font-medium` | 强调正文、导航项 |
| `body-2` | 13px | 400 | `text-[13px] font-normal` | 辅助正文、说明文字 |
| `body-2-medium` | 13px | 500 | `text-[13px] font-medium` | Tab、按钮文字 |
| `body-1` | 12px | 400 | `text-xs font-normal` | Badge、元数据、时间戳 |
| `body-1-medium` | 12px | 500 | `text-xs font-medium` | 标签强调、小按钮 |

---

## Typography Rules

- 大标题 (display 系列) 使用负 `letter-spacing`（-0.01em ~ -0.03em）
- 正文 `line-height: 1.5`；多行段落用 `leading-relaxed`（1.625）
- 次要文字用语义 token，不直接写灰色色值
- 代码/数据/终端 → `--font-mono`
- 使用 `truncate` 而非 `overflow-hidden text-ellipsis whitespace-nowrap`
