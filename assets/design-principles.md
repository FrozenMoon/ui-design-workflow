# UI Design Principles

**Applicable phase**: Demo phase (before the spec has been defined)

When producing UI demos, the spec document does not yet exist. At this stage, follow these principles to ensure every design is **distinctive, production-grade, and avoids generic AI aesthetics**.

> **Core principle — Intentional Design**: Every design choice must be deliberate and context-specific. Default to bold, distinctive choices over safe, generic ones. A design should feel like it was made *for this specific project*, not generated from a template.

> **Supporting principle — Less is More**: Keep the token set minimal (border-radius 3 levels, spacing 4 levels, shadows 3 levels, font weights 2). Add more through `iterate` when genuinely needed. Minimal tokens ≠ minimal aesthetics — a small set of well-chosen tokens creates more cohesion than an exhaustive one.

**CRITICAL**: Before designing, read the full **[Frontend Aesthetics Guide](../references/frontend-aesthetics.md)** for detailed guidance on typography, color, motion, layout, and the anti-AI-slop checklist.

---

## 1. Design Thinking (Start Here)

### Principle
Before writing any code, commit to a clear aesthetic direction. The design must have a point of view.

### Process

1. **Understand context**: What is this product? Who uses it? What feeling should it evoke?
2. **Choose an aesthetic direction**: Pick a tone — brutally minimal, luxury refined, editorial, organic, retro-futuristic, etc. See the [Frontend Aesthetics Guide](../references/frontend-aesthetics.md) for a full list.
3. **Define the memorable element**: What is the ONE thing someone will remember about this design? An unusual layout? A striking color? A bold typographic choice?
4. **Execute with precision**: Match code complexity to the aesthetic vision. Maximalist designs need elaborate code; minimal designs need perfect spacing and typography.

### Anti-pattern
Starting to code without a design direction. This produces generic, personality-free interfaces.

---

## 2. Typography

### Principle
Typography is the single most impactful design decision. Choose fonts that are beautiful, unique, and characterful.

### Rules

1. **NEVER use generic fonts as primary choices**: Arial, Inter, Roboto, Helvetica, system-ui, sans-serif. These are the hallmark of AI-generated design.
2. **Pair fonts deliberately**: Combine a distinctive display/heading font with a refined body font.
3. **Vary across projects**: Never converge on the same "safe" choice across different designs.

### Font Size Hierarchy
- Use at least 3 levels of font size with a noticeable ratio (1.5-2x between levels)
- Example scale: Display 48px → H1 36px → H2 28px → H3 22px → Body 16px → Small 14px → Caption 12px

### Font Weight
- Headings: Semibold (600) or Bold (700)
- Body: Regular (400) or Medium (500)
- Auxiliary: Regular with reduced color contrast

### Letter Spacing & Line Height
- Customize these per font — defaults are rarely optimal
- Display text: tighter letter-spacing (-0.02em to -0.05em)
- Body text: slightly looser line-height (1.5-1.7)
- All caps text: wider letter-spacing (0.05em-0.1em)

See [Frontend Aesthetics Guide — Typography](../references/frontend-aesthetics.md#typography) for font pairing strategies and recommended font sources.

---

## 3. Color & Theme

### Principle
Build a cohesive palette that evokes an emotion. If you can't describe the feeling your colors create, they are too generic.

### Palette Structure
- **Primary**: 1 brand color with light/dark variants
- **Accent**: 1-2 sharp accent colors for CTAs and emphasis
- **Background**: 1-2 background values that set the mood
- **Surface**: 1-2 elevated surface colors for cards/containers
- **Text**: 2-3 levels (primary, secondary, muted)
- **Semantic**: Success, Error, Warning, Info

### Color Rules
1. **Dominant + accent model**: One dominant color establishes mood; accents create focal points. This outperforms timid, evenly-distributed palettes.
2. **Use CSS variables for all colors**: Enable easy theming and consistency.
3. **Avoid cliched AI palettes**: Purple gradients on white, blue-to-purple fades, generic teal/coral combos.
4. **Customize your neutrals**: Don't use Tailwind's default gray scale as-is. Warm your grays, cool them, or tint them to match your palette.

### Theme System

**Option 1: Single theme** — Simple, low cost. Best for utility products.

**Option 2: Light/dark toggle (Recommended)** — Modern standard. Dark mode requires redesigned contrast, shadows, and opacity — not just inverted colors.

**Option 3: Multi-theme** — Maximum customization. Best for white-label products.

See [Frontend Aesthetics Guide — Color & Theme](../references/frontend-aesthetics.md#color--theme) for palette strategies by tone.

---

## 4. Spatial Composition & Layout

### Principle
The most memorable interfaces break layout expectations. Not every section needs centered containers with evenly-spaced cards.

### Techniques
- **Asymmetry**: Off-center elements, unequal columns in hero sections and features
- **Overlap**: Elements layered for visual depth
- **Grid-breaking**: One element that escapes the grid to draw attention
- **Generous whitespace**: Extreme spacing as a design element (luxury, editorial)
- **Controlled density**: Tightly packed grids for data-heavy interfaces
- **Rhythm variation**: Alternate between dense and sparse sections

### Spacing System (4 levels)
```
S:  8px  - Component internal spacing
M:  16px - Standard padding
L:  24px - Card padding, component gaps
XL: 48px - Section spacing
```

Use a 4px grid (all values are multiples of 4). Finer values (4px) can be used directly without a named token.

### Border Radius (3 levels)
```
Default:    8px     - Most components
Large:      16px    - Modal, Dialog, large containers
Full:       9999px  - Pill buttons, Avatar
```

---

## 5. Motion & Animation

### Principle
Motion should create delight and meaning. One well-orchestrated moment creates more impact than scattered micro-interactions.

### Priority Hierarchy

1. **Page load** (highest impact): Staggered reveals with `animation-delay`. Elements enter with purpose — fade up, slide in, scale. Orchestrate timing so the eye follows a natural reading path.
2. **Scroll-triggered reveals**: Elements animate as they enter viewport. Use `IntersectionObserver`.
3. **Hover & interaction states**: Tactile responses — lifts, color shifts, scale changes. Should surprise.
4. **State transitions**: Modal opens, tab switches, accordion expands. Smooth, purposeful.

### Technical Rules
- Animate only `transform` and `opacity` (performance)
- Use custom cubic-bezier easing: `cubic-bezier(0.16, 1, 0.3, 1)` for satisfying deceleration
- Duration: 200-400ms for micro-interactions, 500-800ms for entrances, 150-250ms for exits
- Prefer CSS-only for HTML projects; use Motion (Framer Motion) for React when available

### Anti-patterns
- Random bouncing elements with no purpose
- Everything animating at once (no orchestration)
- Animations that delay content readability
- Using `ease-in-out` for everything

---

## 6. Backgrounds & Visual Details

### Principle
Solid white or solid dark backgrounds are the AI-generated default. Break this pattern with atmospheric depth.

### Techniques
- **Gradient meshes**: Multi-point gradients with soft blending for hero sections
- **Noise / grain textures**: SVG filter overlays for organic feel and premium look
- **Geometric patterns**: Repeating CSS/SVG patterns for tech or editorial aesthetic
- **Layered transparencies**: Semi-transparent overlapping shapes for depth
- **Dramatic shadows**: Large, colored, or layered box-shadows for focal points
- **Radial highlights**: Ambient light effects, especially on dark themes
- **Glassmorphism**: `backdrop-filter: blur()` + semi-transparency for modern feel

> Choose techniques that match the aesthetic direction. A brutalist design needs none of these; a luxury design might use subtle grain + gradients.

---

## 7. Component Design

### Principle
Components should have a consistent visual language while expressing the chosen aesthetic direction.

### Core Components
- **Basic**: Button, Input, Checkbox/Radio/Switch, Select
- **Feedback**: Toast, Alert, Modal, Tooltip
- **Layout**: Card, Container, Divider

### Component Rules
1. **Unify styles**: All buttons share border-radius, padding, font. All cards share shadow, radius, background.
2. **Define variants**: Primary, Secondary, Ghost, Outline for buttons. Sizes: Small, Medium, Large.
3. **Design states**: Normal, Hover, Active, Disabled, Focus, Loading.
4. **Make hover states interesting**: Go beyond simple color darkening. Consider lifts, shadow changes, border animations, background reveals.

---

## 8. Responsive Design

### Principle
The experience should adapt gracefully across devices.

### Breakpoints
```
Mobile:  < 768px
Tablet:  768px - 1024px
Desktop: > 1024px
```

### Adaptation Rules
- Mobile: Single-column, vertical stacking, larger tap targets (44x44px min)
- Tablet: 2-column layout
- Desktop: Full layout with all visual effects
- Font sizes scale down on mobile (minimum 14px body)
- Navigation collapses to Drawer or Bottom Nav on mobile

---

## 9. Accessibility

### Principle
Beautiful design and accessibility are not mutually exclusive. Bold aesthetics must still be usable.

### Requirements
- Text contrast ratio: ≥ 4.5:1 for body text, ≥ 3:1 for large text (≥ 18px)
- Focus states: Clearly visible on all interactive elements (2-3px outline or ring)
- Tap targets: Minimum 44x44px on mobile, 32x32px on desktop
- Semantic HTML: Correct elements (`button`, `nav`, `header`, `main`), `alt` on images, `label` on inputs
- Keyboard navigation: All functionality accessible via keyboard, logical tab order

---

## 10. Interactive Feedback & Copy

### Principle
Every interaction should feel responsive and intentional. Copy should be clear and action-oriented.

### Interaction States
- **Hover**: Color shift + lift/shadow change + transition
- **Active**: Slight scale-down or downward shift
- **Disabled**: Reduced opacity (0.5) + `cursor: not-allowed`
- **Loading**: Spinner/Skeleton + disabled interaction + progress indication
- **Success/Error**: Toast notifications or inline messages with semantic colors

### Copy Rules
- Button labels: Start with a verb ("Save", "Delete", "Get Started")
- Error messages: Explain cause + provide solution, never blame user
- Keep it concise: Every word must earn its place

---

## The Anti-AI-Slop Checklist

Before finalizing any design, verify it passes. See the [full checklist in the Frontend Aesthetics Guide](../references/frontend-aesthetics.md#the-anti-ai-slop-checklist).

Quick check:
- ❌ Uses Inter/Roboto/Arial as primary font?
- ❌ Purple gradient on white background?
- ❌ Every section is centered with equal columns?
- ❌ All cards look the same (white bg, slight shadow, rounded)?
- ❌ The design could belong to any product — no personality?
- ❌ You've seen this exact design generated by AI before?

> **If any box is checked, go back and make bolder choices.**

---

## Summary

1. **Start with design thinking** — context → direction → memorable element
2. **Choose distinctive typography** — never generic fonts; pair for contrast
3. **Build an emotional color palette** — dominant + accent; avoid AI cliches
4. **Break layout expectations** — asymmetry, rhythm, intentional whitespace
5. **Orchestrate motion** — high-impact moments over scattered animations
6. **Add atmospheric depth** — textures, gradients, visual details
7. **Run the anti-AI-slop checklist** — if anything is generic, make bolder choices

**Remember: Claude is capable of extraordinary creative work. Don't hold back — commit fully to a distinctive vision.**
