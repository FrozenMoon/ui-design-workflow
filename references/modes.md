# Mode Details

Detailed execution flows and output formats for each command.

---

## demo Mode

### Three Entry Points

**Flow A: From Scratch**
- User has no existing spec
- **Step 1**: Analyze the project (package.json, code structure, tech stack, project type)
- **Step 2**: Recommend a component solution based on the analysis; user selects or specifies one
- Step 3: Confirm style preferences with the user
- Step 4: Generate a complete UI showcase page

**Flow B: Based on Existing Spec**
- User has an existing spec document
- Read the spec and identify the component solution
- Generate the corresponding Demo
- Flag components missing from the spec

**Flow C: Specified Component Library**
- User specifies a library directly in the command (e.g., "use shadcn/ui")
- Skip the recommendation step and use the specified library directly
- Style preferences still need to be confirmed

### Project Analysis (Flow A)

Analyze the user's project and present the results:

```
📋 Project Analysis:

Tech Stack: [Next.js 14 / Vite + React / Vue 3 / ...]
Styling Solution: [Tailwind CSS / CSS Modules / SCSS / ...]
Existing UI Library: [None / shadcn/ui / Ant Design / ...]
Project Type: [Landing Page / Admin Dashboard / SaaS / E-commerce / ...]

Recommended Component Solution: [Solution Name]
Recommendation Reason: [One-sentence explanation]

Other Available Options:
1. [Option A] - [Description]
2. [Option B] - [Description]
3. Custom Components - Fully hand-written, maximum flexibility

Please select a component solution:
```

Analysis criteria can be found in [assets/library-guide.md](../assets/library-guide.md).

### Questions to Confirm with User

1. **Component Solution**: Recommend based on project analysis; user confirms or specifies another
2. **Theme Mode**: Single theme / Light-dark toggle / Multi-theme?
3. **Style Preference**: Minimal / Techy / Warm / Professional?
4. **Border Radius Preference**: Sharp / Rounded / Fully rounded?

### Output Completion Prompt

```
✅ UI showcase page generated: [file path]

Component Solution: [Custom / shadcn/ui / ...]

Contents:
📱 Tab 1: Finished Product Showcase (Landing Page Demo)
- Hero, Features, Use Cases, CTA, Footer
- Uses [Solution Name] components

🎨 Tab 2: Component Library
- Color system, Typography
- [Solution Name] component showcase (Buttons, Forms, Feedback, Cards, etc.)
- Custom components: [list, if any]

Preview: Visit /ui-showcase after starting the dev server

You can continue adjusting colors, border radius, spacing, etc.
When satisfied, use /ui-design-workflow spec to generate the spec document.
```

---

## spec Mode

### Input

Confirmed Demo code

### Output

1. **Spec Document**: `doc/UI设计规范.md` (includes component solution section)
2. **Project Integration**: Update CLAUDE.md

### Spec Document Structure

```markdown
# [Project Name] UI Design Spec

## 1. Design Philosophy

## 2. Component Solution ← Records the chosen component solution
- Solution type (Custom / Library name)
- Library version (if applicable)
- Theme configuration method and file path
- Usage rules
- Custom component list
- Component mapping table

## 3. Color System

## 4. Typography System

## 5. Spacing & Border Radius

## 6. Shadows & Animations

## 7. Component Spec

## 8. Don'ts List

## 9. Code Examples

## 10. Responsive Design

## 11. Accessibility

## 12. Changelog
```

Detailed template available at [assets/spec-template.md](../assets/spec-template.md).

### CLAUDE.md Update

Add the following content:
```markdown
## UI Design Spec

This project follows the design spec defined in `doc/UI设计规范.md`.

When developing UI-related features, you must:
1. Read the UI Design Spec first
2. Use the colors, spacing, and component styles defined in the spec
3. Use the component solution specified in the spec (Custom / Component library)
4. New component styles must be consistent with the existing spec
```

---

## implement Mode

### Key Flow

```
1. Check whether the project has a UI spec
   ↓
2. If yes, read the spec document first
   ↓
3. Identify the component solution (Custom vs. Component library)
   ↓
4. If using a component library:
   - Use library components; do not hand-write equivalents
   - Customize styles through the library's theming system
   - For components not available in the library, create custom ones following the library's style
   If using custom components:
   - Hand-write all components according to the spec
   ↓
5. Implement the user's requested feature according to the spec
   ↓
6. Ensure styles comply with the spec
```

### Mandatory Rules

- **Read the spec before writing code**
- Use the color variables defined in the spec
- Use the border radius and spacing defined in the spec
- Reference the style of similar components in the spec for new components
- **Additional requirements for component library mode**:
  - Prefer library components; consult the component mapping table
  - Customize styles through the library's theme/configuration system
  - When a component not available in the library is needed, follow the library's extension patterns
  - When necessary, look up correct library usage via Context7 or documentation

---

## check Mode

### Input

File path or directory

### Checks

**General Checks**:
1. Whether colors use spec-defined values
2. Whether spacing conforms to the spec
3. Whether component styles are consistent
4. Whether there are undefined components

**Component Library-Specific Checks** (only when using a component library):
5. Whether library components are used instead of hand-written equivalents
6. Whether styles are customized through the theming system rather than direct overrides
7. Whether library component APIs are used correctly
8. Whether there are unnecessary className overrides on library component default styles

### Output Format

```markdown
## UI Spec Check Report

Scope: [path]
Check Time: [time]
Component Solution: [Custom / shadcn/ui / ...]

### Violations (N total)

#### Color Violations
- `src/components/Button.tsx:15` uses `#333`, should be `zinc-900`

#### Component Library Violations (if applicable)
- `src/pages/Home.tsx:23` hand-writes a Button component, should use {library}'s Button
- `src/components/Card.tsx:8` directly overrides component className, should customize through variants

#### Spacing Violations
- `src/pages/Home.tsx:42` padding uses `13px`, should be `12px` (3*4)

### Recommendations
1. Replace hardcoded color values uniformly
2. Check that spacing values are multiples of 4px
3. Replace hand-written components with library components (if applicable)

### Summary
- Files checked: X
- Violations found: Y
- Severity: Low / Medium / High
- Library component usage rate: Z% (if applicable)
```

---

## iterate Mode

### Trigger Scenarios

- A missing component is discovered in the spec
- A new component type needs to be added
- An existing spec needs adjustment
- **Switching component solutions** (e.g., from custom to a component library)

### Flow

```
1. Confirm the content to add/modify
   ↓
2. If a component solution change is involved:
   - List the components that need to be migrated
   - Update the component mapping table
   ↓
3. Update the spec document
   ↓
4. Update the Demo showcase page (if needed)
   ↓
5. Synchronize updates to related implementation code (if needed)
```

### Output

```
✅ Spec updated

Changes:
- [Added/Modified/Migrated] Component Name: Details

Files updated:
- doc/UI设计规范.md
- app/ui-showcase/page.tsx (if applicable)
```
