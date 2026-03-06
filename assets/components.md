# Component Library Template

Template structure for Demo mode Tab 2 (Component Library). Applicable to both custom components and component library approaches.

## Existing Project Components

For projects that already have components, **scan and include them first** before adding template components.

### Scan Strategy

1. Search component directories (`src/components/`, `src/ui/`, `components/`, etc.)
2. Identify each component's variants, states, and usage patterns
3. Include all existing components in the showcase

### Display Rules

- **Preserve existing components as-is** — do not modify their code during the demo phase
- Display existing components in a dedicated "Project Components" section at the top of Tab 2
- Label each as "Existing" to distinguish from newly generated template components
- If an existing component overlaps with a template component below (e.g., project already has a Button), show the existing version and skip the template version
- New template components should match the existing project's visual style

### Assessment Notes

After displaying existing components, include a brief assessment:
- Components with consistent styling: no action needed
- Components with minor inconsistencies (e.g., mixed border-radius): note for future `iterate` updates
- Components with severe issues (e.g., broken accessibility): recommend fixing, but do not auto-modify

---

## Template Component Sections

The following sections define the **minimum set** of components for a complete showcase. Skip any section where the project already has an equivalent component (shown above).


### 1. Color System
- Primary colors (Primary, Secondary, Background)
- Text color hierarchy (Heading, Body, Muted)
- Brand accent colors (Positive/Negative, used for business comparisons)
- System feedback colors (Success, Error, Warning, Info)

### 2. Typography System
- Display / H1 / H2 / H3 / Body / Small / Caption
- Font weight variants
- Line height examples

### 3. Buttons
- Styles: Primary, Secondary, Ghost, Outline
- Sizes: Small, Medium, Large
- States: Normal, Hover, Active, Disabled
- Icon variants

### 4. Form Components
- Input (text input)
- Textarea (multiline text)
- Select (dropdown)
- Checkbox - custom styled
- Radio - custom styled
- Switch (toggle)
- States: Normal, Focus, Error, Disabled

### 5. Feedback Components
- Toast (brief notification) - Success, Error variants
- Alert (alert message) - Success, Error, Warning, Info
- Modal (dialog)

### 6. Cards
- Basic card (bordered)
- Shadow card
- Interactive card

### 7. Loading States
- Spinner (loading indicator)
- Skeleton (placeholder)
- Progress Bar

## Component Display Principles

Each component should display:
1. All variants (styles, sizes)
2. All states (normal, hover, disabled, etc.)
3. Interactive examples (e.g., a button to open a Modal)

## Code Structure Example

```tsx
<section className="component-section">
  <h2>3. Buttons</h2>

  <div className="subsection">
    <h3>Style Variants</h3>
    <div className="examples">
      <button className="primary">Primary</button>
      <button className="secondary">Secondary</button>
      <button className="ghost">Ghost</button>
      <button className="outline">Outline</button>
    </div>
  </div>

  <div className="subsection">
    <h3>Sizes</h3>
    <div className="examples">
      <button className="small">Small</button>
      <button className="medium">Medium</button>
      <button className="large">Large</button>
    </div>
  </div>

  <div className="subsection">
    <h3>States</h3>
    <div className="examples">
      <button>Normal</button>
      <button className="hover">Hover</button>
      <button disabled>Disabled</button>
    </div>
  </div>
</section>
```

## Custom Form Controls

Checkbox and Radio should use custom styles with the native controls hidden:

```tsx
// Checkbox example
<label className="flex items-center gap-3 cursor-pointer">
  <div className="relative w-5 h-5">
    <input type="checkbox" className="peer sr-only" />
    <div className="absolute inset-0 bg-zinc-100 rounded-lg
                    peer-checked:bg-zinc-900 transition-all" />
    <Check className="absolute inset-0 w-3.5 h-3.5 m-auto text-white
                      opacity-0 peer-checked:opacity-100" />
  </div>
  <span>Option text</span>
</label>

// Radio example
<label className="flex items-center gap-3 cursor-pointer">
  <div className="relative w-5 h-5">
    <input type="radio" className="peer sr-only" />
    <div className="absolute inset-0 bg-zinc-100 rounded-full
                    peer-checked:bg-zinc-900 transition-all" />
    <div className="absolute inset-0 w-2 h-2 m-auto bg-white rounded-full
                    opacity-0 peer-checked:opacity-100" />
  </div>
  <span>Option text</span>
</label>
```

---

## Display Adjustments When Using a Component Library

When a component library is selected (e.g., shadcn/ui, Ant Design, Element Plus), the display strategy for Tab 2 changes as follows:

### Display Content

1. **Library components**: Use the library's actual components with the project theme applied
2. **Theme comparison**: Show library default styles vs. project-themed styles
3. **Custom components**: Components not available in the library are still hand-coded, labeled as "Custom"
4. **Same component sections**: All sections listed above (colors, typography, buttons, forms, etc.) are still displayed

### Code Structure Example (Component Library Mode)

```tsx
// Example using shadcn/ui (similar pattern for other libraries, with corresponding imports)
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Card, CardHeader, CardTitle, CardContent } from "@/components/ui/card"
import { Switch } from "@/components/ui/switch"
import { Checkbox } from "@/components/ui/checkbox"

<section className="component-section">
  <h2>3. Buttons</h2>

  <div className="subsection">
    <h3>Style Variants</h3>
    <div className="examples">
      <Button variant="default">Primary</Button>
      <Button variant="secondary">Secondary</Button>
      <Button variant="ghost">Ghost</Button>
      <Button variant="outline">Outline</Button>
    </div>
  </div>

  <div className="subsection">
    <h3>Sizes</h3>
    <div className="examples">
      <Button size="sm">Small</Button>
      <Button size="default">Medium</Button>
      <Button size="lg">Large</Button>
    </div>
  </div>
</section>
```

### Important Notes

- Import paths should match the actual paths in the project
- Use the library's defined variant / size props; do not override with custom className
- Components not included in the library (e.g., certain loading animations) should be custom-built and labeled as "Custom"
- Display the library's theme configuration file contents (e.g., color/border-radius definitions in tailwind.config.ts)
