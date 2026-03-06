# Component Library Integration Guide

This document provides guidance on how to adapt each workflow phase when the user chooses to use a component library (rather than custom components).

---

## Project Analysis Protocol

During the demo phase, **before generating UI**, analyze the user's project:

### Step 1: Read Project Information

1. **`package.json`** — Identify the framework and existing dependencies:
   - Detect UI library dependencies (`@radix-ui/*`, `antd`, `element-plus`, `@chakra-ui/*`, etc.)
   - Identify the framework (React / Vue / Svelte / Angular)
   - Identify the styling solution (Tailwind / CSS Modules / SCSS / styled-components)

2. **Scan the code directory** — Identify existing patterns:
   - Check if `src/components/ui/` already contains shadcn/ui components
   - Check if import statements reference a specific UI library
   - Check if a theme configuration file already exists

3. **Determine project type**:
   - Marketing site / Landing page → Custom components or shadcn/ui
   - Admin panel / Dashboard → shadcn/ui or Ant Design
   - Enterprise application → Ant Design or Element Plus
   - Vue project → Element Plus or Naive UI
   - Mobile-first → Custom components or a dedicated mobile library

### Step 1.5: Scan Existing Components

For projects with existing code, scan for components already in use:

1. **Search component directories** — `src/components/`, `src/ui/`, `components/`, etc.
2. **Identify each component** — name, file path, variants, states
3. **Assess consistency** — check if existing components follow a unified style (colors, spacing, border-radius, transitions)
4. **Classify findings**:
   - Consistent: no action needed
   - Minor inconsistencies: note for future iteration
   - Severe issues (broken accessibility, broken layouts): recommend fixing, but **do not auto-modify**

**Key principle**: Existing components are preserved as-is. The demo showcase should include them alongside the template components. New template components should match the existing project's visual patterns.

### Step 2: Present the Analysis to the User

```
Project Analysis:

Tech stack: [Next.js 14 / Vite + React / Vue 3 / ...]
Styling solution: [Tailwind CSS / CSS Modules / SCSS / ...]
Existing UI library: [None / shadcn/ui / Ant Design / ...]
Project type: [Marketing site / Admin panel / SaaS / E-commerce / ...]

Existing Components: [N] found
- [Component list with file paths]
- Assessment: [Consistent / Minor inconsistencies in X / Severe issues in Y]

Recommended component solution: [Solution name]
Reason: [One-line explanation]

Alternative options:
1. [Option A] - [Description]
2. [Option B] - [Description]
3. Custom components - Fully hand-coded, maximum flexibility

Please select a component solution:
```

### Step 3: User Confirmation

- The user selects the recommended solution or specifies another
- If the user already specified a library in their command (e.g., "use shadcn/ui"), skip the analysis and use it directly
- If the user explicitly says "custom components", skip the analysis

---

## Phase-Specific Behavior

### Demo Phase

| Aspect | Custom Components | Component Library |
|--------|-------------------|-------------------|
| Tab 1 final preview | Hand-code all components | Use library components + project theme |
| Tab 2 component library | Display hand-coded component states | Display library components + themed configuration |
| Code style | Native HTML + Tailwind | Import library components, use library API |
| Components not in the library | Hand-code everything | Hand-code and label as "Custom" |

### Spec Phase

Add a "Component Solution" section to the spec document (see spec-template.md), documenting:
- Solution type and version
- Theme configuration method and file paths
- Library component usage rules
- List of custom components
- Component mapping table

### Implement Phase

| Aspect | Custom Components | Component Library |
|--------|-------------------|-------------------|
| Component source | Hand-code per spec | Prefer library components |
| Style customization | Write Tailwind/CSS directly | Configure via the library's theme system |
| Missing components | Hand-code | Build following the library's extension patterns |
| Import style | No special requirements | Use the library's standard import paths |

**Key rules for component library mode**:
- Prefer library components; do not reinvent the wheel
- Customize styles through the library's theme/configuration system; do not override library component internals with raw CSS
- When a component not available in the library is needed, follow the library's extension patterns
- Use Context7 or documentation queries to look up correct library usage when needed

### Check Phase

Additional checks for component library mode:
- Whether any hand-coded components duplicate components already available in the library
- Whether style customizations use the library's theme system rather than direct overrides
- Whether library component props are used correctly
- Whether there are unnecessary className overrides of library component default styles

### Iterate Phase

- When adding new components, first check whether the library already provides them
- Support switching component solutions (e.g., from custom to shadcn/ui)
- When switching, list the components that need to be migrated
