# Design System

Inspired by Anthropic's website — clean, minimal, professional, and trustworthy.

---

## Color Palette

### Primary Colors
| Token | Value | Usage |
|---|---|---|
| `--color-bg` | `#FAFAF8` | Page background — warm off-white, not harsh pure white |
| `--color-surface` | `#FFFFFF` | Cards, panels, modals |
| `--color-surface-subtle` | `#F5F5F0` | Sidebar backgrounds, secondary panels |
| `--color-border` | `#E5E5E0` | Dividers, card borders, input borders |
| `--color-border-strong` | `#D4D4CE` | Focused inputs, emphasized separators |

### Text Colors
| Token | Value | Usage |
|---|---|---|
| `--color-text-primary` | `#1A1A18` | Headlines, body copy — near-black with warmth |
| `--color-text-secondary` | `#4A4A45` | Subheadings, descriptions, labels |
| `--color-text-muted` | `#8A8A82` | Timestamps, placeholders, meta text |
| `--color-text-inverse` | `#FFFFFF` | Text on dark backgrounds |

### Brand / Action Colors
| Token | Value | Usage |
|---|---|---|
| `--color-primary` | `#D4760A` | Primary buttons, active states, links — Anthropic's warm orange-brown |
| `--color-primary-hover` | `#B8640A` | Button hover states |
| `--color-primary-light` | `#FDF3E7` | Light tint for badges, highlights, selected states |
| `--color-accent` | `#2D2D2B` | Dark accent for secondary buttons, nav items |

### Semantic Colors
| Token | Value | Usage |
|---|---|---|
| `--color-success` | `#2E7D52` | Success states, confirmations |
| `--color-success-light` | `#E8F5EE` | Success backgrounds |
| `--color-error` | `#C0392B` | Error states, destructive actions |
| `--color-error-light` | `#FDECEA` | Error backgrounds |
| `--color-warning` | `#B7791F` | Warning states |
| `--color-warning-light` | `#FEF3C7` | Warning backgrounds |

---

## Typography

### Font Families
```css
--font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
--font-mono: 'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace;
```

### Type Scale
| Token | Size | Line Height | Weight | Usage |
|---|---|---|---|---|
| `--text-xs` | `11px` | `1.5` | 400 | Micro labels, badges |
| `--text-sm` | `13px` | `1.5` | 400 | UI labels, secondary text |
| `--text-base` | `15px` | `1.6` | 400 | Body text, chat messages |
| `--text-md` | `17px` | `1.5` | 500 | Subheadings, card titles |
| `--text-lg` | `20px` | `1.4` | 600 | Section headers |
| `--text-xl` | `24px` | `1.3` | 600 | Page titles |
| `--text-2xl` | `30px` | `1.2` | 700 | Hero headings |

### Font Weights
```css
--font-normal: 400;
--font-medium: 500;
--font-semibold: 600;
--font-bold: 700;
```

---

## Spacing

Base unit: `4px`

```css
--space-1:  4px
--space-2:  8px
--space-3:  12px
--space-4:  16px
--space-5:  20px
--space-6:  24px
--space-8:  32px
--space-10: 40px
--space-12: 48px
--space-16: 64px
--space-20: 80px
```

---

## Border Radius

```css
--radius-sm:   4px    /* Tags, badges, small inputs */
--radius-md:   8px    /* Buttons, input fields */
--radius-lg:   12px   /* Cards, panels */
--radius-xl:   16px   /* Modals, large cards */
--radius-full: 9999px /* Pills, avatars */
```

---

## Shadows

```css
--shadow-sm:  0 1px 2px rgba(0, 0, 0, 0.05);
--shadow-md:  0 2px 8px rgba(0, 0, 0, 0.08);
--shadow-lg:  0 4px 16px rgba(0, 0, 0, 0.10);
--shadow-xl:  0 8px 32px rgba(0, 0, 0, 0.12);
```

---

## Components

### Buttons

**Primary Button**
```
Background: --color-primary (#D4760A)
Text: --color-text-inverse (#FFFFFF)
Padding: 10px 20px
Border radius: --radius-md
Font: --text-sm, --font-semibold
Hover: --color-primary-hover, slight scale(1.01)
Transition: 150ms ease
```

**Secondary Button**
```
Background: transparent
Border: 1px solid --color-border-strong
Text: --color-text-primary
Padding: 10px 20px
Border radius: --radius-md
Hover: --color-surface-subtle background
```

**Ghost Button**
```
Background: transparent
Text: --color-text-secondary
No border
Hover: --color-surface-subtle background
```

---

### Input Fields

```
Background: --color-surface (#FFFFFF)
Border: 1px solid --color-border
Border radius: --radius-md
Padding: 10px 14px
Font size: --text-base
Color: --color-text-primary
Placeholder: --color-text-muted

Focus:
  Border: 1px solid --color-primary
  Box shadow: 0 0 0 3px rgba(212, 118, 10, 0.12)
  Outline: none
```

---

### Cards

```
Background: --color-surface (#FFFFFF)
Border: 1px solid --color-border
Border radius: --radius-lg
Padding: --space-6 (24px)
Shadow: --shadow-sm
```

---

### Sidebar

```
Background: --color-surface-subtle (#F5F5F0)
Border right: 1px solid --color-border
Width: 260px
Padding: --space-4 (16px)

Nav item (default):
  Padding: 8px 12px
  Border radius: --radius-md
  Text: --color-text-secondary, --text-sm

Nav item (active/hover):
  Background: --color-primary-light
  Text: --color-primary
  Font weight: --font-medium
```

---

### Chat Bubbles

**User message**
```
Background: --color-primary (#D4760A)
Text: --color-text-inverse
Border radius: 16px 16px 4px 16px
Padding: 10px 16px
Max width: 72%
Align: right
```

**Assistant message**
```
Background: --color-surface (#FFFFFF)
Border: 1px solid --color-border
Text: --color-text-primary
Border radius: 16px 16px 16px 4px
Padding: 10px 16px
Max width: 72%
Align: left
```

---

### Navigation / Top Bar

```
Background: --color-surface (#FFFFFF)
Border bottom: 1px solid --color-border
Height: 56px
Padding: 0 --space-6
Shadow: --shadow-sm
Font: --text-sm, --font-medium
```

---

## Layout

```
Max content width: 1200px
Page padding (desktop): 0 40px
Page padding (mobile): 0 16px

Dashboard layout:
  Left sidebar: 260px fixed
  Main content: flex-1
  Right panel (optional): 300px fixed
```

---

## Motion

```css
--transition-fast:   100ms ease;
--transition-base:   150ms ease;
--transition-slow:   250ms ease;
--transition-spring: 200ms cubic-bezier(0.34, 1.56, 0.64, 1);
```

Only animate: opacity, transform, background-color, border-color, box-shadow.
Never animate layout properties (width, height, padding, margin).

---

## Iconography

Use **Lucide React** icons throughout.
- Default size: 16px for inline, 20px for standalone
- Stroke width: 1.5px
- Color: inherit from parent text color

---

## Writing Style (UI Copy)

- Short, direct, sentence case (not Title Case) for labels
- Action-oriented button labels: "Upload contract", "Start review", "Save changes"
- Error messages explain what happened and what to do next
- No jargon — write for a non-technical user
