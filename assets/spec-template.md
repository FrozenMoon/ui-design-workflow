# [Project Name] UI Design Spec

> **Version**: 1.0
> **Status**: Active
> **Last Updated**: [Current Date]

This document defines the visual and interaction standards for [Project Name]. All UI-related development must comply with this spec.

> **Core principle — Less is More**: This spec defines the minimum viable set of design tokens. Each dimension (spacing, border-radius, shadows, etc.) uses the fewest levels necessary. Additional levels can be added through the `iterate` workflow when a genuine need arises. Do not add tokens "just in case."

---

## 1. Design Philosophy

[Core design language extracted from the Demo]

### Core Keywords
- **[Keyword 1]**: [Description]
- **[Keyword 2]**: [Description]
- **[Keyword 3]**: [Description]

### Design Goals
- [Goal 1: e.g., Provide a clean and intuitive user experience]
- [Goal 2: e.g., Maintain visual consistency and brand recognition]
- [Goal 3: e.g., Ensure accessibility and inclusive design]

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
| **Configuration Method** | [CSS Variables / ConfigProvider / SCSS Variables / Hand-written styles] |

### Usage Rules

- ✅ Prefer library components; do not reinvent the wheel
- ✅ Customize styles through the library's theming system
- ✅ Follow the library's component API and props naming conventions
- ❌ Do not directly override library component internal styles with CSS
- ❌ Do not hand-write equivalents of components already available in the library

> The rules above do not apply when using a **custom solution**; all components are hand-written according to this spec.

### Custom Component List

The following components are not provided by the library and use custom implementations:

| Component Name | Description | Reference Style |
| :--- | :--- | :--- |
| [Component Name] | [Purpose] | [Reference library component style] |

### Component Mapping Table

| Common Name | Library Component | Import Path |
| :--- | :--- | :--- |
| Button | [e.g., `<Button>`] | [e.g., `@/components/ui/button`] |
| Input | [e.g., `<Input>`] | [e.g., `@/components/ui/input`] |
| Card | [e.g., `<Card>`] | [e.g., `@/components/ui/card`] |
| Modal | [e.g., `<Dialog>`] | [e.g., `@/components/ui/dialog`] |
| Toast | [e.g., `<Sonner>`] | [e.g., `@/components/ui/sonner`] |
| Select | [e.g., `<Select>`] | [e.g., `@/components/ui/select`] |
| ... | ... | ... |

> The mapping table is not required for **custom solutions**.

---

## 3. Color System

### 2.1 Core Palette

| Role | Variable Name | Value / CSS Class | Description |
| :--- | :--- | :--- | :--- |
| **Primary** | `primary` | `#000000` / `bg-primary` | Primary action points (buttons, links) |
| **Secondary** | `secondary` | `#666666` / `bg-secondary` | Secondary action points |
| **Background** | `background` | `#FFFFFF` / `bg-background` | Global background color |
| **Card** | `card` | `#FAFAFA` / `bg-card` | Card/container background |

### 2.2 Text Colors

| Role | Variable Name | Value / CSS Class | Description |
| :--- | :--- | :--- | :--- |
| **Heading** | `foreground` | `#000000` / `text-foreground` | Headings, important text |
| **Body** | `text-body` | `#333333` / `text-body` | Body content |
| **Muted** | `muted-foreground` | `#999999` / `text-muted-foreground` | Supporting info, secondary text |
| **Disabled** | `text-disabled` | `#CCCCCC` / `text-disabled` | Disabled state text |

### 2.3 Functional Colors

Use sparingly; only for status feedback.

| Role | Value / CSS Class | Description |
| :--- | :--- | :--- |
| **Success** | `#10B981` / `text-green-600` | Success state, confirmation actions |
| **Error** | `#EF4444` / `text-red-600` | Error state, destructive actions |
| **Warning** | `#F59E0B` / `text-amber-600` | Warning state, items requiring attention |
| **Info** | `#3B82F6` / `text-blue-600` | Informational messages, general notifications |

### 2.4 Color Usage Principles

- ✅ **Prefer** colors from the core palette
- ✅ Use functional colors consistently (success = green, error = red)
- ❌ **Do not** use bright colors in core UI (except functional colors)
- ❌ **Do not** use more than 3 primary colors

---

## 4. Typography

### 3.1 Font Families

**Heading Font**:
- Latin: [Font name, e.g., Inter, -apple-system, system-ui]
- CJK: [Font name, e.g., PingFang SC, Microsoft YaHei]
- Font Stack: `[Full font-family definition]`

**Body Font**:
- Latin: [Font name]
- CJK: [Font name]
- Font Stack: `[Full font-family definition]`

### 3.2 Type Scale

| Level | Font Style | CSS Class | Size / Line Height | Weight | Usage |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Display** | Sans-serif | `text-4xl lg:text-6xl` | 48-60px / 1.1 | 700 | Landing page hero |
| **H1** | Sans-serif | `text-3xl` | 30px / 1.2 | 600 | Page / section title |
| **H2** | Sans-serif | `text-xl` | 20px / 1.4 | 600 | Card heading, sub-section |
| **Body** | Sans-serif | `text-base` | 16px / 1.5 | 400 | Default body text |
| **Small** | Sans-serif | `text-sm` | 14px / 1.5 | 400 | Buttons, inputs, secondary info |

> Add more levels (e.g., H3, Caption) through the `iterate` workflow when needed.

### 3.3 Font Weight Standards

| Weight Name | Value | Usage |
| :--- | :--- | :--- |
| Regular | 400 | Body text, descriptions |
| Semibold | 600 | Headings, buttons, emphasis |

### 3.4 Typography Principles

- ✅ Use heavier font weights (600+) for headings
- ✅ Use Regular (400) for body text
- ✅ Line height should be at least 1.5 (readability)
- ❌ Avoid using more than 2 font weights by default
- ❌ Avoid all-caps text (UPPERCASE); it reduces readability

---

## 5. Spacing & Border Radius

### 4.1 Spacing Scale

Based on a **[4px / 8px] grid system**.

| Token | Value | Tailwind Class | Usage |
| :--- | :--- | :--- | :--- |
| **S** | 8px | `p-2`, `m-2`, `gap-2` | Component internal spacing |
| **M** | 16px | `p-4`, `m-4`, `gap-4` | Standard padding |
| **L** | 24px | `p-6`, `m-6`, `gap-6` | Card padding, component gaps |
| **XL** | 48px | `p-12`, `m-12`, `gap-12` | Section spacing |

> Finer values (e.g., 4px for icon-text gaps) can be used directly from the grid without a named token. Add more levels through `iterate` when needed.

### 4.2 Border Radius

| Token | Value | Tailwind Class | Usage |
| :--- | :--- | :--- | :--- |
| **Default** | 8px | `rounded-lg` | Button, Input, Badge, Card |
| **Large** | 16px | `rounded-2xl` | Modal, Dialog, large containers |
| **Full** | 9999px | `rounded-full` | Pill button, Avatar |

> Most components should share a single border-radius. Add more levels through `iterate` only when needed.

### 4.3 Spacing & Border Radius Principles

- ✅ All spacing values should conform to the grid system (multiples of [4/8]px)
- ✅ Use smaller spacing between related elements, larger spacing between unrelated ones
- ✅ Maintain consistent border radius (same radius for components of the same type)
- ❌ Avoid odd spacing values (e.g., 7px, 13px)
- ❌ Avoid border radius too small (< 4px); visually insignificant

---

## 6. Shadows & Animations

### 5.1 Shadow System

| Level | Tailwind Class | Box Shadow Value | Usage |
| :--- | :--- | :--- | :--- |
| **None** | `shadow-none` | `none` | No elevation needed |
| **Default** | `shadow` | `0 4px 6px rgba(0,0,0,0.1)` | Cards, elevated surfaces |
| **Large** | `shadow-lg` | `0 10px 15px rgba(0,0,0,0.1)` | Dropdown, Modal, Popover |

> Avoid over-using shadows. Most elements need no shadow; reserve them for clear elevation changes.

### 5.2 Animation Standards

**Transition Configuration**:
```css
transition: all 0.2s ease-out; /* Default */
transition: all 0.3s ease-out; /* Slower, for larger elements */
```

**Common Animations**:
- **Hover Lift**: `hover:-translate-y-0.5 hover:shadow-lg`
- **Click Scale**: `active:scale-95`
- **Fade In**: `transition-opacity duration-200`

### 5.3 Animation Principles

- ✅ All interactive elements should have transition effects
- ✅ Keep duration between 150-300ms
- ✅ Use `ease-out` or `ease-in-out`
- ❌ Avoid excessively long animations (> 500ms)
- ❌ Avoid abrupt changes without transitions

---

## 7. Components

### 6.1 Button

**Style Variants**:

| Variant | Class Names | Usage |
| :--- | :--- | :--- |
| **Primary** | `bg-primary text-primary-foreground` | Primary action |
| **Secondary** | `bg-secondary text-secondary-foreground` | Secondary action |
| **Ghost** | `bg-transparent text-foreground hover:bg-secondary` | Lightweight action |
| **Outline** | `border border-primary text-primary bg-transparent` | Cancel action |

**Size Variants**:

| Size | Class Name | Padding | Font Size |
| :--- | :--- | :--- | :--- |
| **Small** | `btn-sm` | `px-3 py-1.5` | `text-sm` |
| **Default** | `btn` | `px-4 py-2` | `text-sm` |
| **Large** | `btn-lg` | `px-6 py-3` | `text-base` |

**States**:
- Normal: Default styles
- Hover: Background darkened 10%, slight lift
- Active: Background darkened 20%, slight scale down
- Disabled: `opacity-50 cursor-not-allowed`

**Code Example**:
```tsx
<button className="bg-primary text-white px-4 py-2 rounded-lg hover:-translate-y-0.5 hover:shadow-lg transition-all active:scale-95">
  Primary Button
</button>
```

---

### 6.2 Form Controls

#### Input

**Base Styles**:
```tsx
className="bg-white border border-gray-300 rounded-lg px-4 py-2 text-base focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all"
```

**States**:
- Normal: `border-gray-300`
- Focus: `ring-2 ring-primary`
- Error: `border-red-500 ring-2 ring-red-500`
- Disabled: `bg-gray-100 text-gray-400 cursor-not-allowed`

#### Select

Maintains the same styles as Input, with an arrow icon on the right side.

#### Checkbox / Radio

**Styles**:
- Size: 16x16px or 20x20px
- Border radius: Checkbox uses `rounded`, Radio uses `rounded-full`
- Checked state: Background uses `primary`
- Focus state: Outer ring

---

### 6.3 Feedback Components

#### Toast

**Position**: Top-right or top-center

**Styles**:
```tsx
className="bg-white rounded-lg shadow-lg px-4 py-3 border-l-4 border-[functional-color]"
```

**Types**:
- Success: Green left border
- Error: Red left border
- Warning: Yellow left border
- Info: Blue left border

**Animation**: Slides in from the right, stays for 3-5 seconds, then fades out

#### Alert

**Styles**:
```tsx
className="bg-[functional-color]-50 border border-[functional-color]-200 rounded-lg px-4 py-3 text-[functional-color]-800"
```

#### Modal

**Overlay**: `bg-black/50 backdrop-blur-sm`
**Container**: `bg-white rounded-2xl shadow-2xl p-6`
**Animation**: Fade in + scale (from 0.95 to 1)

---

### 6.4 Card

**Base Styles**:
```tsx
className="bg-white rounded-2xl shadow p-6"
```

**Hover Effect**:
```tsx
className="hover:-translate-y-1 hover:shadow-lg transition-all duration-300"
```

**Variants**:
- Borderless with shadow: `shadow`
- With border: `border border-gray-200`
- Flat: `bg-gray-50` (no shadow)

---

### 6.5 Navigation Components

#### Tabs

**Container**: `border-b border-gray-200`
**Tab**:
- Inactive: `text-gray-600 hover:text-gray-900`
- Active: `text-primary border-b-2 border-primary`

#### Breadcrumb

**Styles**: `text-sm text-gray-600`
**Separator**: `/` or `>` or arrow icon
**Current Page**: `text-foreground font-medium`

#### Pagination

**Styles**:
- Buttons: Same as Secondary Button
- Current page: Uses Primary Button style

---

### 6.6 Other Components

#### Custom Scrollbar

```css
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}
```

#### Loading

**Spinner**:
- Size: 16px (small), 24px (medium), 32px (large)
- Color: `primary`
- Animation: Rotate, 1s linear infinite

**Skeleton**:
- Background: `bg-gray-200`
- Animation: Left-to-right gradient sweep effect

#### Progress Bar

- Background: `bg-gray-200 rounded-full`
- Progress bar: `bg-primary rounded-full`
- Height: 4-8px

---

## 8. Don'ts

The following practices should be **avoided**:

### Colors
- ❌ Using too many colors (more than 3 primary colors)
- ❌ Insufficient color contrast (text-to-background contrast ratio < 4.5:1)
- ❌ Using functional colors in non-functional contexts (e.g., red as decoration)

### Typography
- ❌ Font size too small (< 12px)
- ❌ Line height too small (< 1.2)
- ❌ Using more than 4 font weights
- ❌ All-caps text (reduces readability)

### Spacing
- ❌ Using spacing values that don't conform to the grid (e.g., 7px, 13px)
- ❌ Spacing too small, causing crowded elements
- ❌ Inconsistent spacing (different spacing between elements at the same level)
- ❌ Over-specifying: defining more than 4 named spacing tokens when fewer suffice

### Border Radius
- ❌ Border radius too small (< 4px)
- ❌ Inconsistent border radius for components of the same type
- ❌ Mixing sharp and rounded corners (maintain a unified style)
- ❌ Over-specifying: defining more than 3 border-radius levels when fewer suffice

### Animations
- ❌ Animation duration too long (> 500ms)
- ❌ No transition effects (abrupt changes)
- ❌ Overusing animations (impacts performance)

### Other
- ❌ Click/tap target too small (< 32x32px)
- ❌ Missing focus states
- ❌ Missing hover feedback

---

## 9. Code Examples

> **Note**: The examples below vary depending on the project's component solution.
> - **Custom solution**: Uses native HTML + Tailwind CSS (as shown below)
> - **Component library solution**: Uses library components + project theme (refer to import paths in the component mapping table)

### Complete Button Component Example

```tsx
// Primary Button
<button className="bg-primary text-white px-4 py-2 rounded-lg font-medium hover:-translate-y-0.5 hover:shadow-lg active:scale-95 transition-all duration-200">
  Primary Button
</button>

// Secondary Button
<button className="bg-gray-100 text-gray-900 px-4 py-2 rounded-lg font-medium hover:bg-gray-200 active:scale-95 transition-all duration-200">
  Secondary Button
</button>

// Ghost Button
<button className="bg-transparent text-gray-700 px-4 py-2 rounded-lg font-medium hover:bg-gray-100 active:scale-95 transition-all duration-200">
  Ghost Button
</button>
```

### Complete Card Component Example

```tsx
<div className="bg-white rounded-2xl shadow p-6 hover:-translate-y-1 hover:shadow-lg transition-all duration-300">
  <h3 className="text-xl font-semibold text-foreground mb-2">
    Card Title
  </h3>
  <p className="text-sm text-body mb-4">
    Card description goes here.
  </p>
  <button className="bg-primary text-white px-4 py-2 rounded-lg text-sm font-medium hover:shadow-lg transition-all">
    Action
  </button>
</div>
```

### Complete Form Example

```tsx
<form className="space-y-4">
  <div>
    <label className="block text-sm font-medium text-foreground mb-1">
      Email
    </label>
    <input
      type="email"
      className="w-full bg-white border border-gray-300 rounded-lg px-4 py-2 text-base focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all"
      placeholder="your@email.com"
    />
  </div>

  <div>
    <label className="block text-sm font-medium text-foreground mb-1">
      Password
    </label>
    <input
      type="password"
      className="w-full bg-white border border-gray-300 rounded-lg px-4 py-2 text-base focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all"
      placeholder="••••••••"
    />
  </div>

  <button type="submit" className="w-full bg-primary text-white px-4 py-3 rounded-lg font-medium hover:shadow-lg transition-all">
    Sign In
  </button>
</form>
```

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
- Defined complete specs for colors, typography, spacing, border radius, components, etc.

---

**Spec Maintenance**:
- Review and update regularly (recommended quarterly)
- This document must be updated when new components or styles are added
- Use `/ui-design-workflow iterate` for spec iterations
