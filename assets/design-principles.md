# UI Design Principles

**Applicable phase**: Demo phase (before the spec has been defined)

When producing UI demos, the spec document does not yet exist. At this stage, follow these general UI design principles to ensure design quality and maintainability.

> **Core principle — Less is More**: Default to the minimum viable set of design tokens and component variants. Provide only what is clearly needed. Resist the urge to over-specify — every additional token adds cognitive overhead and maintenance burden. Users will request more through `iterate` when a genuine need arises.

---

## 1. Visual Hierarchy

### Principle
Information should have clear hierarchical differentiation to guide the user's attention.

### Best Practices

**Font size hierarchy**:
- Use at least 3 levels of font size: headings, body text, auxiliary information
- The difference between levels should be noticeable (recommended ratio of 1.5-2x)
- For example: H1: 32px, H2: 24px, Body: 16px, Small: 12px

**Font weight hierarchy**:
- Use heavier weights for headings (Semibold 600, Bold 700)
- Use medium weights for body text (Regular 400, Medium 500)
- Use lighter weights or reduced color contrast for auxiliary information

**Color contrast**:
- Primary content: High contrast (e.g., black text #000000)
- Secondary content: Medium contrast (e.g., dark gray #333333 or #555555)
- Auxiliary information: Low contrast (e.g., light gray #999999 or #AAAAAA)

**Spacing hierarchy**:
- Tight spacing between related elements (4-8px)
- Medium spacing within components (12-16px)
- Large spacing between sections (24-48px)

---

## 2. Component-Based Design

### Principle
Identify and design reusable UI patterns to avoid redundant work.

### Core Component Checklist

**Basic components**:
- Button
- Input
- Checkbox / Radio / Switch
- Select / Dropdown

**Feedback components**:
- Toast (brief notification)
- Alert (alert message)
- Modal (dialog)
- Tooltip

**Layout components**:
- Card
- Container
- Divider

### Best Practices

1. **Unify component styles**:
   - All buttons should use the same border-radius, padding, and font
   - All cards should use the same shadow, border-radius, and background

2. **Define component variants**:
   - Buttons: Primary, Secondary, Ghost, Outline
   - Sizes: Small, Medium, Large
   - States: Normal, Hover, Active, Disabled

3. **Maintain consistency**:
   - The same state of similar components should have a consistent visual appearance
   - For example: All components' Hover states should have the same transition effect

---

## 3. Consistency

### Principle
The entire design system should have a unified visual language.

### Theme System Design (Critical Architecture Decision)

Before starting the design, the theme strategy must be determined:

**Option 1: Single theme (light or dark)**
- Pros: Simple, low development cost, easy to maintain design consistency
- Cons: Cannot accommodate user preferences for different environments
- Best for: Utility products with a clear purpose and single-use-case scenarios

**Option 2: Light/dark theme toggle (Recommended)**
- Pros: Accommodates different user preferences; standard for modern applications
- Cons: Requires maintaining two sets of colors; doubles design and testing effort
- Best for: Most consumer-facing products
- Implementation:
  ```css
  /* Using CSS variables */
  :root {
    --color-bg: #FFFFFF;
    --color-text: #000000;
  }

  [data-theme="dark"] {
    --color-bg: #000000;
    --color-text: #FFFFFF;
  }
  ```

**Option 3: Multi-theme system**
- Pros: Highly customizable, brand differentiation
- Cons: Highest design and maintenance cost
- Best for: Products requiring white-labeling or multi-brand support

**Theme switching considerations**:
- It is not just about inverting colors: Dark mode requires redesigned contrast, shadows, and opacity
- Images and illustrations: May require separate assets for each theme
- Testing effort: All components need to be tested under both themes

### Color Consistency

**Limit the number of colors**:
- Primary: 1-2 colors (Primary, Secondary)
- Neutrals: A grayscale system (5-7 levels)
- Functional colors: Success, Error, Warning, Info (1 each)
- No more than 15 colors total
- **If supporting multiple themes**: Each theme needs its own set of these colors

**Establish a grayscale system**:
```
Very light gray (background): #F9F9F9, #F5F5F5
Light gray (dividers):        #E5E5E5, #DDDDDD
Medium gray (auxiliary text):  #999999, #888888
Dark gray (secondary text):    #666666, #555555
Very dark gray (primary text): #333333, #222222
Pure black (headings):         #000000
```

### Spacing Consistency

**Use a grid system**:
- 4px grid: All spacing values are multiples of 4 (4, 8, 12, 16, 20, 24, 32, 48, 64...)
- Or 8px grid: All spacing values are multiples of 8 (8, 16, 24, 32, 40, 48, 64...)

**Define semantic spacing** (4 levels):
```
S:  8px  - Component internal spacing
M:  16px - Standard padding
L:  24px - Card padding, component gaps
XL: 48px - Section spacing
```

> Finer values (e.g., 4px) can be used directly from the grid without a named token. Add more levels only when needed.

### Border Radius Consistency

**Unified border radius specification** (3 levels):
```
Default:    8px     - Most components (Button, Input, Card, Badge)
Large:      16px    - Modal, Dialog, large containers
Full:       9999px  - Pill buttons, Avatar
```

> Most components should share a single border-radius value. Add more levels only when needed.

---

## 4. Responsive Design

### Principle
The experience should be good across different devices and screen sizes.

### Best Practices

**Use breakpoints**:
```
Mobile:  < 768px
Tablet:  768px - 1024px
Desktop: > 1024px
```

**Layout adaptation**:
- Mobile: Single-column layout, vertical stacking
- Tablet: 2-column layout
- Desktop: 3-4 column layout

**Component adaptation**:
- Buttons should be larger on mobile (easier to tap)
- Navigation should use a Drawer or Bottom Nav on mobile
- Forms should be full-width on mobile

**Font size adaptation**:
- Font sizes can be slightly smaller on mobile (but no smaller than 14px)
- Headings can use a smaller scale on mobile

---

## 5. Accessibility

### Principle
Designs should be user-friendly for all users, including those with disabilities.

### Best Practices

**Color contrast**:
- Body text to background contrast ratio >= 4.5:1
- Large text (>= 18px) to background contrast ratio >= 3:1
- Use online tools to verify: https://webaim.org/resources/contrastchecker/

**Focus states**:
- All interactive elements (buttons, links, inputs) should have a clearly visible focus state
- Recommended: 2-3px outline or ring

**Tap/click targets**:
- Minimum tap target size on mobile: 44x44px
- Minimum click target size on desktop: 32x32px
- Icon buttons should have sufficient padding

**Semantic HTML**:
- Use correct HTML elements (button, input, nav, header, main)
- Add alt attributes to images
- Add labels to form inputs

**Keyboard navigation**:
- Ensure all functionality is accessible via keyboard
- Tab order should follow a logical sequence
- Enter and Space should trigger buttons

---

## 6. Performance Optimization

### Principle
Avoid over-engineering; keep the page smooth and responsive.

### Best Practices

**Avoid excessive shadows**:
- Do not apply shadows to every element
- Shadows should be used to convey elevation and layering
- Use subtle, soft shadows; avoid harsh, dark shadows

**Use animations judiciously**:
- Keep animation duration between 150-300ms
- Avoid complex keyframe animations
- Prefer transform and opacity (better performance)
- Avoid animating width, height, margin, etc. (poor performance)

**Image optimization**:
- Use appropriate image formats (WebP > JPEG > PNG)
- Responsive images: Load different sizes for different screens
- Lazy-load images below the fold

**Reduce DOM complexity**:
- Avoid deeply nested elements
- Reuse components instead of duplicating them

---

## 7. Interactive Feedback

### Principle
User actions should receive immediate and clear feedback.

### Best Practices

**Hover state** (desktop):
- Change color (darken or lighten)
- Slight scale-up or lift (transform: scale(1.05) or translateY(-2px))
- Change shadow (intensify or expand)
- Add transition effects (transition: all 0.2s)

**Active state** (on click):
- Slight scale-down (transform: scale(0.95))
- Or slight downward shift (translateY(1px))
- Reduce brightness

**Disabled state**:
- Reduce opacity (opacity: 0.5)
- Or use light gray
- Cursor: not-allowed

**Loading state**:
- Display a Spinner or Skeleton
- Disable interaction (prevent duplicate submissions)
- Provide progress indication (if progress is known)

**Success/error feedback**:
- Use Toast notifications
- Or display inline messages below the form
- Use appropriate colors (green for success, red for error)

---

## 8. Whitespace and Breathing Room

### Principle
Do not be afraid of whitespace; proper spacing makes designs clearer.

### Best Practices

**Inner padding for components**:
- Button padding: 16-24px horizontal, 8-12px vertical
- Card padding: 24-32px
- Input padding: 12-16px horizontal, 8-12px vertical

**Spacing between components**:
- Elements within the same group: 8-12px
- Elements in different groups: 24-32px
- Page sections: 48-64px

**Avoid overcrowding**:
- When in doubt, add more whitespace rather than cramming elements together
- Use cards to group content on dense pages
- Use dividers to separate regions

---

## 9. Progressive Enhancement

### Principle
Core functionality should work in any environment; advanced features serve as enhancements.

### Best Practices

**Baseline version**:
- Basic functionality that does not depend on JavaScript
- Simple CSS styles
- Plain HTML forms

**Enhanced version**:
- JavaScript interactions (e.g., real-time validation)
- CSS animations and transitions
- Advanced UI components

**Graceful degradation**:
- Older browsers display a simplified version
- Unsupported features have fallbacks
- Missing features should not cause crashes

---

## 10. Copy and Microinteractions

### Principle
Text and details determine the quality of the user experience.

### Copy Guidelines

**Clear and concise**:
- Button labels should start with a verb: "Save", "Delete", "Cancel"
- Avoid vagueness: "OK" (OK to do what?)
- Error messages should explain the cause and provide a solution

**Friendly and polite**:
- Error messages should not blame the user
- Use positive language
- For example: "Your password is too short" --> "Password must be at least 8 characters"

### Microinteractions

**Details define quality**:
- Buttons have a subtle bounce on click
- Modals open with a fade-in + scale animation
- Toasts slide in from the side
- Inputs have a breathing effect on focus (ring animation)

---

## Summary

These principles represent general UI design best practices that should be followed during the Demo phase (before the spec has been defined).

Once the demo is finalized, use the `spec` mode to codify these principles into a project-specific UI design spec document, establishing concrete constraints and standards for the project.

**Remember**: Good design is 80% fundamental principles + 20% creativity and personality. Master the basics first, then pursue uniqueness.
