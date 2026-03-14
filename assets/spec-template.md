# [Project Name] UI Design Spec

> **Version**: 1.0
> **Status**: Active
> **Last Updated**: [Current Date]

This document defines the visual and interaction standards for [Project Name]. All UI-related development must comply with this spec.

> **Core principle — Less is More**: This spec defines the minimum viable set of design tokens. Each dimension (spacing, border-radius, shadows, etc.) uses the fewest levels necessary. Additional levels can be added through the `iterate` workflow when a genuine need arises. Do not add tokens "just in case."

> **Single source of truth**: Design tokens and rules live in this spec. Component implementations live in the project code. This spec does NOT duplicate component code — use the Component Registry to find and read actual component files.

---

## 1. Design Philosophy

[Core design language extracted from the Demo]

### Aesthetic Direction
- **Tone**: [Chosen aesthetic direction — e.g., "Editorial luxury with warm undertones"]
- **Memorable Element**: [The ONE thing that makes this design distinctive — e.g., "Dramatic serif typography with oversized display text"]
- **Mood**: [The emotion the design evokes — e.g., "Sophisticated warmth, refined craftsmanship"]

### Core Keywords
- **[Keyword 1]**: [Description]
- **[Keyword 2]**: [Description]
- **[Keyword 3]**: [Description]

### Design Goals
- [Goal 1: e.g., Create a distinctive, memorable visual identity]
- [Goal 2: e.g., Maintain cohesive aesthetic across all pages]
- [Goal 3: e.g., Ensure accessibility without compromising creative vision]

### Anti-patterns (Do NOT)
- Use generic fonts (Inter, Roboto, Arial, Helvetica) as primary choices
- Default to purple-on-white gradients or cliched AI color schemes
- Create uniform centered-container layouts with no variation
- Produce a design that could belong to any product

---

## 2. Component Solution

### Solution Details

| Property | Value |
| :--- | :--- |
| **Solution** | [Custom / shadcn/ui / Ant Design / Element Plus / Other] |
| **Library Version** | [Version, e.g., "antd@5.x"; enter "N/A" for custom solutions] |
| **Installation Method** | [e.g., "npx shadcn@latest add"; enter "N/A" for custom] |

### Theme Configuration

| Property | Value |
| :--- | :--- |
| **Config File** | [Path, e.g., "tailwind.config.ts"; enter "N/A" for custom] |
| **CSS Variables File** | [Path, e.g., "src/styles/globals.css"] |
| **Configuration Method** | [CSS Variables / ConfigProvider / SCSS Variables / Hand-written styles] |

### Usage Rules

- ✅ Prefer library components; do not reinvent the wheel
- ✅ Customize styles through the library's theming system
- ✅ Follow the library's component API and props naming conventions
- ❌ Do not directly override library component internal styles with CSS
- ❌ Do not hand-write equivalents of components already available in the library

> The rules above do not apply when using a **custom solution**; all components are hand-written according to this spec.

---

## 3. Color System

### Core Palette

| Role | Variable Name | Value | CSS Class | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Primary** | `--primary` | `[value]` | `bg-primary` | Primary brand color, CTAs |
| **Primary Light** | `--primary-light` | `[value]` | `bg-primary-light` | Primary hover/light variant |
| **Accent** | `--accent` | `[value]` | `bg-accent` | Sharp accent for emphasis |
| **Background** | `--background` | `[value]` | `bg-background` | Global background |
| **Surface** | `--surface` | `[value]` | `bg-surface` | Card/container background |

### Text Colors

| Role | Variable Name | Value | CSS Class | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Primary Text** | `--foreground` | `[value]` | `text-foreground` | Headings, important text |
| **Body Text** | `--text-body` | `[value]` | `text-body` | Body content |
| **Muted Text** | `--text-muted` | `[value]` | `text-muted` | Supporting info |

### Functional Colors

Use sparingly; only for status feedback.

| Role | Value | CSS Class | Description |
| :--- | :--- | :--- | :--- |
| **Success** | `[value]` | `text-success` | Success state |
| **Error** | `[value]` | `text-error` | Error state |
| **Warning** | `[value]` | `text-warning` | Warning state |
| **Info** | `[value]` | `text-info` | Informational |

### Color Usage Principles

- ✅ All colors use CSS variables — never hardcode hex values in components
- ✅ Dominant + accent model: primary establishes mood, accent creates focal points
- ✅ Functional colors are used consistently (success = green, error = red)
- ❌ Do not use more than 2 primary/accent colors
- ❌ Do not use unmodified Tailwind gray scales — customize neutrals to match palette

---

## 4. Typography

### Font Families

> **Important**: Choose distinctive, characterful fonts. NEVER use generic fonts (Inter, Roboto, Arial, Helvetica) as primary choices.

**Heading Font**:
- Name: [Distinctive font name, e.g., Playfair Display, Clash Display, Fraunces]
- Source: [Google Fonts / Adobe Fonts / Self-hosted]
- CJK Fallback: [Font name, e.g., PingFang SC, Microsoft YaHei]
- Font Stack: `[Full font-family definition]`
- Character: [Why this font was chosen — e.g., "Strong serifs create editorial authority"]

**Body Font**:
- Name: [Refined body font, e.g., Source Serif Pro, Plus Jakarta Sans, DM Sans]
- Source: [Google Fonts / Adobe Fonts / Self-hosted]
- CJK Fallback: [Font name]
- Font Stack: `[Full font-family definition]`
- Character: [Why this font pairs well with the heading font]

### Type Scale

| Level | CSS Class | Size / Line Height | Weight | Usage |
| :--- | :--- | :--- | :--- | :--- |
| **Display** | `text-4xl lg:text-6xl` | 48-60px / 1.1 | 700 | Landing page hero |
| **H1** | `text-3xl` | 30px / 1.2 | 600 | Page / section title |
| **H2** | `text-xl` | 20px / 1.4 | 600 | Card heading, sub-section |
| **Body** | `text-base` | 16px / 1.5 | 400 | Default body text |
| **Small** | `text-sm` | 14px / 1.5 | 400 | Buttons, inputs, secondary info |

> Add more levels (e.g., H3, Caption) through the `iterate` workflow when needed.

### Font Weight Standards

| Weight Name | Value | Usage |
| :--- | :--- | :--- |
| Regular | 400 | Body text, descriptions |
| Semibold | 600 | Headings, buttons, emphasis |

### Typography Principles

- ✅ Use heavier font weights (600+) for headings
- ✅ Use Regular (400) for body text
- ✅ Customize letter-spacing and line-height per font (defaults are rarely optimal)
- ❌ Avoid using more than 2 font weights by default
- ❌ Avoid all-caps text (UPPERCASE); it reduces readability

---

## 5. Spacing & Border Radius

### Spacing Scale

Based on a **[4px / 8px] grid system**.

| Token | Value | Tailwind Class | Usage |
| :--- | :--- | :--- | :--- |
| **S** | 8px | `p-2`, `m-2`, `gap-2` | Component internal spacing |
| **M** | 16px | `p-4`, `m-4`, `gap-4` | Standard padding |
| **L** | 24px | `p-6`, `m-6`, `gap-6` | Card padding, component gaps |
| **XL** | 48px | `p-12`, `m-12`, `gap-12` | Section spacing |

> Finer values (e.g., 4px for icon-text gaps) can be used directly from the grid without a named token. Add more levels through `iterate` when needed.

### Border Radius

| Token | Value | Tailwind Class | Usage |
| :--- | :--- | :--- | :--- |
| **Default** | 8px | `rounded-lg` | Button, Input, Badge, Card |
| **Large** | 16px | `rounded-2xl` | Modal, Dialog, large containers |
| **Full** | 9999px | `rounded-full` | Pill button, Avatar |

> Most components should share a single border-radius. Add more levels through `iterate` only when needed.

### Principles

- ✅ All spacing values should conform to the grid system (multiples of [4/8]px)
- ✅ Use smaller spacing between related elements, larger spacing between unrelated ones
- ✅ Maintain consistent border radius (same radius for components of the same type)
- ❌ Avoid odd spacing values (e.g., 7px, 13px)

---

## 6. Shadows & Animations

### Shadow System

| Level | Tailwind Class | Box Shadow Value | Usage |
| :--- | :--- | :--- | :--- |
| **None** | `shadow-none` | `none` | No elevation needed |
| **Default** | `shadow` | `0 4px 6px rgba(0,0,0,0.1)` | Cards, elevated surfaces |
| **Large** | `shadow-lg` | `0 10px 15px rgba(0,0,0,0.1)` | Dropdown, Modal, Popover |

### Animation Standards

**Transition Defaults**:
- Duration: 200ms (micro-interactions), 300ms (larger elements), 500-800ms (page entrances)
- Easing: `cubic-bezier(0.16, 1, 0.3, 1)` (preferred) or `ease-out`
- Properties: Animate only `transform` and `opacity` for performance

**Motion Priority** (from highest to lowest impact):
1. Page load: Staggered reveals with `animation-delay`
2. Scroll-triggered: Elements animate on viewport entry
3. Hover / interaction: Tactile responses (lifts, scale, color shifts)
4. State transitions: Modal opens, tab switches

### Animation Principles

- ✅ Orchestrate page load animations — elements enter with purpose
- ✅ Hover states should surprise (not just color darkening)
- ✅ Use custom easing curves
- ❌ Avoid everything animating at once (no orchestration)
- ❌ Avoid animations that delay content readability

---

## 7. Component Registry

> **Key concept**: Component implementations live in the project code, not in this spec. This registry tells you WHAT exists and WHERE to find it. To understand HOW a component works, read its source file directly.

### How to Use This Registry

1. **Before implementing a feature**: Check this registry for existing components that can be reused
2. **When you need a component**: Read its source file at the listed path to understand its API (props, variants, states)
3. **When creating a new component**: Follow the design tokens from this spec, then add the new component to this registry via `iterate`
4. **Do not duplicate**: If a component is listed here, import and use it — do not hand-write a new version

### Registry

| Component | Path | Variants | States | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **Button** | `src/components/ui/button.tsx` | primary, secondary, ghost, outline; sm, default, lg | hover, active, disabled, loading | [Icon support: leading/trailing] |
| **Input** | `src/components/ui/input.tsx` | default | focus, error, disabled | [Includes label and error message] |
| **Card** | `src/components/ui/card.tsx` | shadow, bordered, flat | hover | [Composable: CardHeader, CardContent] |
| **Modal** | `src/components/ui/modal.tsx` | default | open/closed | [Overlay + scale animation] |
| **Toast** | `src/components/ui/toast.tsx` | success, error, warning, info | entering, visible, exiting | [Auto-dismiss 3-5s] |
| **Select** | `src/components/ui/select.tsx` | default | focus, error, disabled, open | [Dropdown with search] |
| **Checkbox** | `src/components/ui/checkbox.tsx` | default | checked, unchecked, disabled | [Custom styled] |
| **Radio** | `src/components/ui/radio.tsx` | default | checked, unchecked, disabled | [Custom styled] |
| **Switch** | `src/components/ui/switch.tsx` | default | on, off, disabled | [Animated toggle] |
| **Alert** | `src/components/ui/alert.tsx` | success, error, warning, info | — | [Icon + dismissible] |
| ... | ... | ... | ... | ... |

> This is a living document. Add new components via `iterate` whenever a new reusable component is created.

### Library Component Mapping (only for component library solutions)

| Common Name | Library Component | Import Path |
| :--- | :--- | :--- |
| Button | [e.g., `<Button>`] | [e.g., `@/components/ui/button`] |
| Input | [e.g., `<Input>`] | [e.g., `@/components/ui/input`] |
| ... | ... | ... |

> Not required for **custom solutions**.

---

## 8. Atmosphere & Visual Details

### Background Treatments

Document the atmospheric techniques used in this project:

| Technique | Implementation | Where Used |
| :--- | :--- | :--- |
| [e.g., Grain texture] | [e.g., CSS pseudo-element with SVG noise] | [e.g., Page backgrounds] |
| [e.g., Gradient mesh] | [e.g., Multi-point radial gradients] | [e.g., Hero section] |
| [e.g., Radial highlight] | [e.g., Radial gradient as ambient light] | [e.g., Dark theme backgrounds] |

### Shared Visual Utilities

| Utility | Path / Class | Description |
| :--- | :--- | :--- |
| [e.g., Grain overlay] | [e.g., `src/components/ui/grain.tsx` or `.grain-overlay` class] | [e.g., Adds subtle noise texture] |
| [e.g., Section divider] | [e.g., `src/components/ui/divider.tsx`] | [e.g., Gradient line between sections] |

---

## 9. Don'ts

The following practices should be **avoided**:

### Colors
- ❌ Hardcoding hex values instead of using CSS variables
- ❌ Insufficient color contrast (text-to-background contrast ratio < 4.5:1)
- ❌ Using functional colors in non-functional contexts (e.g., red as decoration)
- ❌ Using generic AI color schemes (purple-on-white, teal/coral)

### Typography
- ❌ Using generic fonts (Inter, Roboto, Arial, Helvetica) as primary choices
- ❌ Font size too small (< 12px)
- ❌ Line height too small (< 1.2)
- ❌ Using more than 2 font weights by default

### Spacing
- ❌ Using spacing values that don't conform to the grid (e.g., 7px, 13px)
- ❌ Inconsistent spacing between elements at the same level
- ❌ Over-specifying: defining more than 4 named spacing tokens when fewer suffice

### Components
- ❌ Duplicating a component that already exists in the registry
- ❌ Overriding library component styles with raw CSS (use theme system)
- ❌ Writing inline styles instead of using design tokens

### Layout
- ❌ Every section using the same centered-container + equal-column layout
- ❌ No variation in section spacing or visual rhythm
- ❌ Plain solid backgrounds for every section (add atmosphere)

### Animations
- ❌ No transition effects (abrupt changes)
- ❌ Everything animating at once with no orchestration
- ❌ Animations that delay critical content

### Accessibility
- ❌ Click/tap target too small (< 32x32px desktop, < 44x44px mobile)
- ❌ Missing focus states on interactive elements
- ❌ Missing hover feedback

---

## 10. Responsive Design

### Breakpoint Definitions

| Breakpoint | Screen Width | Device Type |
| :--- | :--- | :--- |
| `sm` | >= 640px | Large phones |
| `md` | >= 768px | Tablets |
| `lg` | >= 1024px | Laptops |
| `xl` | >= 1280px | Desktops |
| `2xl` | >= 1536px | Large screens |

### Responsive Rules

- Mobile First
- Use Tailwind's responsive prefixes (e.g., `md:text-lg`)
- Key breakpoints: `md` (768px) and `lg` (1024px)
- Minimum tap target: 44x44px on mobile

---

## 11. Accessibility

### Mandatory Rules

- ✅ Text-to-background contrast ratio >= 4.5:1
- ✅ All interactive elements must have a visible focus state
- ✅ Tap/click targets >= 44x44px (mobile) or >= 32x32px (desktop)
- ✅ Use semantic HTML (button, input, nav, header, main)
- ✅ Add alt attributes to images
- ✅ Add labels to form inputs
- ✅ Support keyboard navigation

---

## 12. Changelog

### v1.0 (Current Date)
- Initial version
- Spec extracted and generated from UI Demo
- Component Registry created with [N] components

---

**Spec Maintenance**:
- Review and update regularly (recommended quarterly)
- When new components are created, add them to the Component Registry via `iterate`
- Use `/ui-design-workflow iterate` for spec iterations
