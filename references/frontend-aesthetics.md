# Frontend Aesthetics Guide

> Inspired by [Anthropic's frontend-design skill](https://github.com/anthropics/claude-code/tree/main/.skills/document-skills/frontend-design) (Apache 2.0 License).

**Purpose**: This guide is the core aesthetic reference for all UI design in this workflow. It ensures every generated interface is distinctive, production-grade, and avoids generic "AI slop" aesthetics. Read this guide before designing any UI.

---

## Design Thinking Process

Before writing any code, go through this mental framework:

### 1. Understand Context
- **Purpose**: What problem does this interface solve? Who uses it?
- **Audience**: Developers? Consumers? Enterprise? Creative professionals?
- **Constraints**: Framework, performance requirements, accessibility needs

### 2. Commit to a Bold Aesthetic Direction

Pick a **clear conceptual direction** and execute it with precision. The key is **intentionality**, not intensity — both bold maximalism and refined minimalism work when done deliberately.

Choose a tone. Here are starting points (use for inspiration, then make it your own):

| Direction | Character | When to Use |
|-----------|-----------|-------------|
| Brutally minimal | Extreme restraint, monochrome, vast whitespace | Developer tools, productivity apps |
| Maximalist chaos | Dense, layered, colorful, energetic | Creative tools, entertainment, marketing |
| Retro-futuristic | Retro typography + modern layout, CRT effects | Tech products, gaming, nostalgia brands |
| Organic / natural | Soft shapes, earthy tones, hand-drawn feel | Wellness, food, sustainability |
| Luxury / refined | Thin serif fonts, muted gold/black, generous spacing | Fashion, finance, premium SaaS |
| Playful / toy-like | Rounded shapes, bright colors, bouncy animations | Consumer apps, children, onboarding |
| Editorial / magazine | Strong typographic hierarchy, grid-based, image-heavy | Content sites, portfolios, blogs |
| Brutalist / raw | Exposed structure, monospace, harsh borders | Indie projects, art, experimental |
| Art deco / geometric | Symmetrical patterns, metallic accents, sharp lines | Events, architecture, luxury brands |
| Soft / pastel | Gentle gradients, rounded cards, light tones | Health, education, personal tools |
| Industrial / utilitarian | Functional, dense data, minimal decoration | Dashboards, monitoring, enterprise |
| Neo-grotesque | Swiss design, grid-heavy, neutral palette, clean | Corporate, institutional, minimal SaaS |

### 3. Define the Memorable Element
Ask: **"What's the one thing someone will remember about this design?"** Every design should have at least one signature element — an unusual layout, a striking color choice, a distinctive animation, or a bold typographic decision.

---

## Typography

Typography is the single most impactful design decision. Choose fonts that are **beautiful, unique, and characterful**.

### Rules

1. **NEVER use generic fonts**: Arial, Inter, Roboto, Helvetica, system-ui, sans-serif as primary choices. These are the hallmark of AI-generated design.
2. **Pair fonts deliberately**: Combine a distinctive display/heading font with a refined body font. The contrast between them should create visual interest.
3. **Vary across projects**: NEVER converge on the same "safe" choice (e.g., Space Grotesk) across different designs. Each project deserves its own typographic identity.

### Font Pairing Strategies

| Strategy | Heading Font Type | Body Font Type | Effect |
|----------|------------------|----------------|--------|
| Classic contrast | Serif (display) | Sans-serif (geometric) | Elegant, editorial |
| Modern contrast | Geometric sans | Humanist sans | Clean, contemporary |
| Expressive + neutral | Display / decorative | Neutral sans | Bold personality with readability |
| Monospace accent | Monospace (heading) | Sans-serif (body) | Technical, developer-oriented |
| All-serif | Serif (display) | Serif (text) | Literary, premium |
| Slab + sans | Slab serif (heading) | Clean sans (body) | Strong, architectural |

### Recommended Font Sources

Use Google Fonts, Adobe Fonts, or self-hosted fonts. Excellent distinctive choices include (but are not limited to):

**Display / Heading fonts**: Playfair Display, Clash Display, Cabinet Grotesk, Satoshi, General Sans, Instrument Serif, Fraunces, Syne, Space Mono, DM Serif Display, Outfit, Manrope, Unbounded, Bricolage Grotesque, Instrument Sans

**Body fonts**: Source Serif Pro, Libre Baskerville, Work Sans, Plus Jakarta Sans, Geist, DM Sans, Nunito Sans, Atkinson Hyperlegible, IBM Plex Sans, Literata

> **Key principle**: The font choice should feel like it was *designed for this specific project*, not pulled from a default template.

---

## Color & Theme

### Rules

1. **Commit to a cohesive palette**: Every color should feel intentional and interconnected.
2. **Dominant + accent model**: One dominant color establishes mood; one or two sharp accent colors create focal points. Outperforms timid, evenly-distributed palettes.
3. **Use CSS variables for consistency**: Define all colors as tokens. Enable easy theming.
4. **Avoid cliched AI color schemes**: Purple gradients on white backgrounds, blue-to-purple fades, generic teal/coral combos — these scream "AI generated."

### Palette Construction

```
┌─ Background (1-2 values) ──── Sets the overall mood
│
├─ Surface (1-2 values) ──── Cards, containers, elevated areas
│
├─ Text (2-3 levels) ──── Primary, secondary, muted
│
├─ Primary brand (1 color + light/dark variants)
│
├─ Accent (1-2 colors) ──── CTAs, highlights, emphasis
│
└─ Semantic (4 colors) ──── Success, error, warning, info
```

### Palette Strategies by Tone

| Tone | Background | Primary | Accent | Effect |
|------|-----------|---------|--------|--------|
| Dark luxury | Near-black (#0a0a0a) | Warm gold (#c4a35a) | Cream (#f5f0e8) | Premium, exclusive |
| Warm editorial | Off-white (#faf8f5) | Deep charcoal (#1a1a1a) | Terracotta (#c4654a) | Sophisticated, readable |
| Cold tech | Dark slate (#0f172a) | Electric blue (#3b82f6) | Lime (#84cc16) | Modern, technical |
| Organic | Warm beige (#f5f0eb) | Forest green (#2d5016) | Amber (#d97706) | Natural, approachable |
| Brutalist | Pure white (#ffffff) | Pure black (#000000) | Red (#ff0000) | Raw, striking |
| Pastel | Soft lavender (#f0e6ff) | Deep purple (#4c1d95) | Peach (#fbbf24) | Gentle, friendly |

> **Key principle**: The palette should evoke an emotion. If you can't describe the feeling your colors create, they're too generic.

---

## Motion & Animation

### Philosophy

Motion should create **delight and meaning**, not just movement. One well-orchestrated moment creates more impact than scattered micro-interactions everywhere.

### Priority Hierarchy

1. **Page load / first impression** (highest impact): Staggered reveals using `animation-delay`. Elements should enter with purpose — fade up, slide in, scale from center. Orchestrate timing so the eye follows a natural reading path.

2. **Scroll-triggered reveals**: Elements that animate as they enter the viewport. Use `IntersectionObserver` or CSS `@scroll-timeline`. Should feel like the page is coming alive as you explore.

3. **Hover & interaction states**: Buttons, cards, links that respond to the cursor. Should feel tactile — slight lifts, color shifts, scale changes. Surprise is welcome.

4. **Transitions between states**: Modal opens, tab switches, accordion expands. Smooth, purposeful, with appropriate easing.

### Technical Guidelines

- **Prefer CSS-only solutions** for HTML projects (transforms, transitions, keyframes)
- **Use Motion (Framer Motion) for React** when available — stagger, layout animations, exit animations
- **Performance**: Animate only `transform` and `opacity`. Avoid animating layout properties (`width`, `height`, `margin`)
- **Easing**: Use custom cubic-bezier curves instead of `ease` or `linear`. Example: `cubic-bezier(0.16, 1, 0.3, 1)` for a satisfying deceleration
- **Duration**: 200-400ms for micro-interactions, 500-800ms for entrances, 150-250ms for exits

### Anti-patterns
- Random elements bouncing for no reason
- Everything animating at once (no orchestration)
- Animations that delay critical content from being readable
- Using `ease-in-out` for everything (it's fine, but boring)

---

## Spatial Composition & Layout

### Think Beyond Standard Layouts

The most memorable interfaces break expectations. Not every section needs to be a centered container with evenly-spaced cards.

### Techniques

| Technique | Description | When to Use |
|-----------|-------------|-------------|
| **Asymmetry** | Off-center elements, unequal columns | Hero sections, feature showcases |
| **Overlap** | Elements layered on top of each other | Visual depth, image-text compositions |
| **Diagonal flow** | Content arranged on an angle or Z-pattern | Landing pages, storytelling sequences |
| **Grid-breaking** | One element that escapes the grid boundary | Drawing attention to key content |
| **Generous whitespace** | Extreme spacing between elements | Luxury, editorial, minimal designs |
| **Controlled density** | Tightly packed information grids | Dashboards, data-heavy interfaces |
| **Full-bleed sections** | Content that stretches edge to edge | Immersive experiences, hero images |
| **Sticky elements** | Scroll-anchored navigation or CTAs | Long-form pages, documentation |

### Layout Principles

1. **Don't default to centered, equal-width columns.** Ask: does this section *need* symmetry?
2. **Let content dictate layout**, not the other way around. A testimonial doesn't have to be a card. A feature list doesn't have to be a grid.
3. **Create visual rhythm** — alternate between dense and sparse sections, between full-width and contained.
4. **Use negative space as a design element**, not empty space to fill.

---

## Backgrounds & Visual Details

### Create Atmosphere

Solid white or solid dark backgrounds are the default of every AI-generated page. Break this pattern.

### Techniques

| Technique | Implementation | Best For |
|-----------|---------------|----------|
| **Gradient meshes** | Multi-point gradients with soft blending | Hero sections, backgrounds |
| **Noise / grain textures** | SVG filter or CSS `background-image` with noise | Organic feel, premium look |
| **Geometric patterns** | CSS or SVG repeating patterns | Tech, art deco, editorial |
| **Layered transparencies** | Semi-transparent overlapping shapes | Depth, modern feel |
| **Dramatic shadows** | Large, colored, or layered box-shadows | Card elevation, focal points |
| **Decorative borders** | Asymmetric, dashed, or gradient borders | Section dividers, cards |
| **Custom cursors** | CSS cursor property with custom SVG | Interactive, playful experiences |
| **Grain overlays** | CSS pseudo-element with noise texture | Film/photo aesthetic, premium |
| **Dot / line grids** | Background SVG patterns | Technical, blueprint aesthetic |
| **Glassmorphism** | `backdrop-filter: blur()` + semi-transparency | Modern, layered interfaces |
| **Radial highlights** | Radial gradients as ambient light effects | Hero sections, dark themes |

### Implementation Example: Noise Texture
```css
.grain-overlay::after {
  content: '';
  position: fixed;
  inset: 0;
  opacity: 0.03;
  background-image: url("data:image/svg+xml,..."); /* noise SVG */
  pointer-events: none;
  z-index: 9999;
}
```

---

## The Anti-AI-Slop Checklist

Before finalizing any design, verify it does NOT have these characteristics:

### ❌ Typography Red Flags
- [ ] Uses Inter, Roboto, Arial, Helvetica, or system-ui as the primary font
- [ ] All text is the same font family with no contrast
- [ ] Generic font sizes with no clear hierarchy
- [ ] Default letter-spacing and line-height everywhere

### ❌ Color Red Flags
- [ ] Purple-to-blue gradient on white background
- [ ] Generic teal + coral accent pairing
- [ ] All grays from Tailwind's default palette with no customization
- [ ] Indistinguishable pastel colors that lack contrast

### ❌ Layout Red Flags
- [ ] Every section is a centered container with max-width and auto margins
- [ ] All feature sections use equal 3-column grids
- [ ] Predictable alternating left-right layout for every section
- [ ] No variation in section spacing, rhythm, or density

### ❌ Component Red Flags
- [ ] All cards look the same (white bg, slight shadow, rounded corners)
- [ ] All buttons are rounded rectangles with gradient fills
- [ ] Generic hero with centered text + single CTA button
- [ ] No hover states or interactions that surprise

### ❌ Overall Red Flags
- [ ] The design could belong to any product — it has no personality
- [ ] You've seen this exact design generated by AI before
- [ ] Removing the text/content would make it unidentifiable
- [ ] Nothing is memorable or distinctive about it

> **If any box is checked, go back and make bolder choices.**

---

## Execution Calibration

Match implementation complexity to aesthetic vision:

| Vision | Code Complexity | Animation Budget | Detail Level |
|--------|----------------|-----------------|--------------|
| Maximalist | High — elaborate nested elements, multiple layers | Heavy — staggered entrances, parallax, interactive cursors | Every element has considered styling |
| Refined minimal | Medium — clean structure, precise spacing | Light — subtle fades, gentle hover states | Focus on typography and spacing perfection |
| Brutalist | Low — raw HTML structure, minimal abstraction | Minimal — harsh transitions or none | Character comes from rawness, not polish |
| Editorial | Medium-high — typographic system, grid layout | Medium — scroll reveals, image treatments | Strong typographic hierarchy is everything |
| Playful | High — custom shapes, illustrations, bouncy elements | Heavy — spring physics, playful transitions | Rounded everything, generous padding |

> **Key principle**: Elegance comes from executing the vision well. A minimalist design with sloppy spacing is worse than an elaborate design with considered details.

---

## Summary

1. **Start with design thinking** — understand context, pick a bold direction, define the memorable element
2. **Choose distinctive typography** — never use generic fonts; pair fonts for contrast and character
3. **Build a cohesive color palette** — dominant + accent model; avoid cliched AI palettes
4. **Orchestrate motion** — prioritize high-impact moments over scattered animations
5. **Break layout expectations** — asymmetry, overlap, rhythm variation
6. **Add atmospheric details** — textures, gradients, visual depth
7. **Run the anti-AI-slop checklist** — if anything is generic, make bolder choices
8. **Calibrate execution** — match code complexity to aesthetic vision

**Remember: Claude is capable of extraordinary creative work. Don't hold back — show what can truly be created when thinking outside the box and committing fully to a distinctive vision.**
