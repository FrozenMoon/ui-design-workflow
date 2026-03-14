# Component Library Template

Template structure for Demo mode Tab 2 (Component Library).

> **Key principle**: The showcase page imports and displays **real project components** — it does NOT write separate inline implementations. Components are created as real files first, then the showcase page renders them.

## Existing Project Components

For projects that already have components, **scan and include them first** before creating new components.

### Scan Strategy

1. Search component directories (`src/components/`, `src/ui/`, `components/`, etc.)
2. Identify each component's variants, states, and usage patterns
3. Include all existing components in the showcase

### Display Rules

- **Preserve existing components as-is** — do not modify their code during the demo phase
- Display existing components in a dedicated "Project Components" section at the top of Tab 2
- Label each as "Existing" to distinguish from newly created components
- If an existing component overlaps with a template component below (e.g., project already has a Button), show the existing version and skip creating a new one
- New components should match the existing project's visual style

### Assessment Notes

After displaying existing components, include a brief assessment:
- Components with consistent styling: no action needed
- Components with minor inconsistencies (e.g., mixed border-radius): note for future `iterate` updates
- Components with severe issues (e.g., broken accessibility): recommend fixing, but do not auto-modify

---

## Demo Phase: Create Components Then Showcase

The demo phase produces TWO outputs:

### Output 1: Real Component Files

Create actual reusable component files in the project. These are the **single source of truth** for each component's implementation.

**File location** (adapt to project structure):
```
src/components/ui/
├── button.tsx        # Button with variants and states
├── input.tsx         # Text input with label and error
├── card.tsx          # Card with composable sub-components
├── modal.tsx         # Modal with overlay and animation
├── toast.tsx         # Toast notification system
├── select.tsx        # Dropdown select
├── checkbox.tsx      # Custom styled checkbox
├── radio.tsx         # Custom styled radio
├── switch.tsx        # Animated toggle switch
├── alert.tsx         # Alert with semantic colors
├── skeleton.tsx      # Loading skeleton
└── spinner.tsx       # Loading spinner
```

**Each component file must**:
- Export a reusable component with typed props
- Support all defined variants (via `variant` prop or similar)
- Support all defined states (disabled, loading, error, etc.)
- Use design tokens (CSS variables) — never hardcode colors/spacing
- Include appropriate transitions and animations
- Be accessible (keyboard navigation, ARIA attributes, focus states)

### Output 2: Showcase Page

The showcase page **imports** the components from Output 1 and renders them in all variants/states.

**Showcase file location**:
- Next.js: `app/ui-showcase/page.tsx`
- Vite: `src/pages/UIShowcase.tsx`

---

## Showcase Sections

The following sections define the **minimum set** for a complete showcase. Skip any section where the project already has an equivalent component.

### 1. Color System
- Background colors (main background, surface/card backgrounds)
- Primary brand color with light/dark variants
- Accent colors (1-2 sharp accents for CTAs and emphasis)
- Text color hierarchy (Primary, Secondary, Muted)
- System feedback colors (Success, Error, Warning, Info)
- Show colors with their CSS variable names

### 2. Typography System
- Display the chosen font pairing (heading + body font names and sources)
- Type scale: Display / H1 / H2 / H3 / Body / Small / Caption
- Font weight variants
- Letter spacing and line height examples
- Show the font pairing in action (heading + body text together)

### 3. Buttons
- Import `Button` from the real component file
- Show all style variants: Primary, Secondary, Ghost, Outline
- Show all sizes: Small, Medium, Large
- Show all states: Normal, Hover, Active, Disabled, Loading
- Show icon variants

### 4. Form Components
- Import `Input`, `Select`, `Checkbox`, `Radio`, `Switch` from real component files
- Show all states: Normal, Focus, Error, Disabled

### 5. Feedback Components
- Import `Toast`, `Alert`, `Modal` from real component files
- Toast: Trigger buttons to show each type (Success, Error, Warning, Info)
- Alert: Display all types inline
- Modal: Trigger button to open

### 6. Cards
- Import `Card` from real component file
- Show all variants: shadow, bordered, flat
- Show interactive hover effects

### 7. Loading States
- Import `Spinner`, `Skeleton` from real component files
- Show size variants

---

## Aesthetic Requirements

The showcase page itself should reflect the chosen aesthetic direction — it is a design artifact, not just a catalogue.

- **Typography**: Use the project's distinctive font choices throughout. Section headings should feel designed.
- **Layout**: Visual interest — varied section backgrounds, interesting spacing rhythms, creative grouping.
- **Interactions**: Components should demonstrate their motion/animation design live. Hover states should be visible and interesting.
- **Atmosphere**: Subtle background treatments (gradient, noise, pattern) matching the project's aesthetic.

> **Anti-pattern**: A showcase page with a plain white background, Inter font, and components laid out in a boring grid with no visual personality.

---

## Code Structure Example (Showcase Page)

```tsx
// Showcase page IMPORTS real components — does NOT rewrite them
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import { Card } from '@/components/ui/card'
import { Modal } from '@/components/ui/modal'
import { Toast } from '@/components/ui/toast'
import { Select } from '@/components/ui/select'
import { Checkbox } from '@/components/ui/checkbox'
import { Switch } from '@/components/ui/switch'
import { Alert } from '@/components/ui/alert'
import { Spinner } from '@/components/ui/spinner'
import { Skeleton } from '@/components/ui/skeleton'

export default function UIShowcase() {
  return (
    <div>
      {/* Tab 1: Landing Page Demo (uses the same components) */}
      {/* Tab 2: Component Library */}

      <section>
        <h2>Color System</h2>
        {/* Color palette swatches with CSS variable names */}
      </section>

      <section>
        <h2>Typography</h2>
        {/* Font pairing display + type scale */}
      </section>

      <section>
        <h2>Buttons</h2>
        <div>
          <Button variant="primary">Primary</Button>
          <Button variant="secondary">Secondary</Button>
          <Button variant="ghost">Ghost</Button>
          <Button variant="outline">Outline</Button>
        </div>
        <div>
          <Button size="sm">Small</Button>
          <Button size="default">Medium</Button>
          <Button size="lg">Large</Button>
        </div>
        <div>
          <Button disabled>Disabled</Button>
          <Button loading>Loading</Button>
        </div>
      </section>

      <section>
        <h2>Form Components</h2>
        <Input label="Email" placeholder="your@email.com" />
        <Input label="Error" error="This field is required" />
        <Input label="Disabled" disabled />
        <Select options={[...]} />
        <Checkbox label="Option A" />
        <Switch label="Enable notifications" />
      </section>

      <section>
        <h2>Feedback</h2>
        <Alert variant="success" message="Operation completed" />
        <Alert variant="error" message="Something went wrong" />
        <Button onClick={() => toast.success('Saved!')}>Show Toast</Button>
        <Button onClick={() => setModalOpen(true)}>Open Modal</Button>
      </section>

      <section>
        <h2>Cards</h2>
        <Card variant="shadow">Shadow Card</Card>
        <Card variant="bordered">Bordered Card</Card>
        <Card variant="flat">Flat Card</Card>
      </section>

      <section>
        <h2>Loading</h2>
        <Spinner size="sm" />
        <Spinner size="md" />
        <Spinner size="lg" />
        <Skeleton width="100%" height="20px" />
      </section>
    </div>
  )
}
```

---

## Display Adjustments When Using a Component Library

When a component library is selected (e.g., shadcn/ui, Ant Design, Element Plus):

### What Changes

1. **Component files may be library-generated**: e.g., `npx shadcn@latest add button` creates the file
2. **Theme configuration** replaces custom styling: colors/radius defined in `tailwind.config.ts` or `ConfigProvider`
3. **Showcase imports library components**: same pattern, just different source components
4. **Components not in the library** are still custom-built, labeled as "Custom" in the showcase

### What Stays the Same

- Showcase still imports real component files (library or custom)
- All sections (colors, typography, buttons, forms, etc.) are still displayed
- The aesthetic requirements still apply to the showcase page itself

### Important Notes

- Import paths must match the actual paths in the project
- Use the library's defined variant / size props; do not override with custom className
- Display the library's theme configuration (e.g., color/border-radius in tailwind.config.ts)
