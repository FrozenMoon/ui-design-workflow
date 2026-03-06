---
name: ui-design-workflow
description: >
  MUST use when implementing UI components or frontend pages in this project.
  Triggers: 实现页面, 开发UI, 写组件, 前端开发, designing UI, implement page,
  create component, build interface, style page, frontend development,
  button, form, modal, toast, card, input, 样式, 界面,
  shadcn, ant design, antd, element plus, 组件库, UI库, component library.
  Before writing any UI code, load this skill to read the project's design spec.
---

# UI Design Workflow

Manage the full UI design workflow: Demo → Spec → Implement → Check → Iterate.
Supports both custom components and component libraries (shadcn/ui, Ant Design, Element Plus, etc.).

## Command Reference

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `demo` | Analyze project + generate UI showcase | Early stage: establish style & component solution |
| `spec` | Generate spec document | After Demo is confirmed |
| `implement` | Build features per spec | Daily development |
| `check` | Audit spec compliance | Before PR, periodic review |
| `iterate` | Update the spec | When gaps are discovered |

---

## Command Details

### demo - Generate UI Showcase Page

**Input**: User's UI style requirements (e.g., "minimal modern", "techy")

**Output**: Single page with two tabs:
- **Tab 1: Finished Product** - Complete landing page demo
- **Tab 2: Component Library** - All components in various states

**Flow**:
1. **Project Analysis**:
   - Read `package.json` to identify framework and existing dependencies
   - Scan code directory to identify existing patterns and tech stack
   - Determine project type (landing page, admin panel, SaaS, e-commerce, etc.)
2. **Recommend Component Solution**:
   - Suggest a solution based on analysis (custom / shadcn/ui / Ant Design / other)
   - Auto-detect existing library dependencies and suggest continuing with them
   - User can accept the recommendation or specify another
   - If user already specified a library in the command, skip recommendation
3. Confirm with user: theme mode (single / light-dark toggle), style preferences
4. Design color system, typography, component styles
5. Generate UI showcase based on the component solution:
   - **Custom components**: Hand-write all component implementations
   - **Component library**: Use library components + project theme configuration
6. Iterate with user

**Output location**:
- Next.js: `app/ui-showcase/page.tsx`
- Vite: `src/pages/UIShowcase.tsx`

**Templates**: See [assets/website.md](assets/website.md) and [assets/components.md](assets/components.md)
**Library guide**: See [assets/library-guide.md](assets/library-guide.md)

---

### spec - Generate Spec Document

**Prerequisite**: Confirmed Demo exists

**Output**:
1. Spec document: `doc/UI设计规范.md`
2. Project integration: Update CLAUDE.md with spec reference

**Flow**:
1. Read Demo code, extract design decisions
2. **Record component solution**: Document the chosen solution in the spec
   - Solution type (custom / library name)
   - Library version (if applicable)
   - Theme configuration method and file path
   - Custom component list and component mapping table
3. Generate structured spec document
4. Update CLAUDE.md with spec reference

---

### implement - Build Features Per Spec

**Prerequisite**: Project has a UI spec

**Flow**:
1. **Must** read the project's UI spec document first
2. **Identify component solution**: Read the component solution section in the spec
   - If library: prefer library components, do not hand-write equivalents
   - If a component not in the library is needed: build following the library's extension patterns
   - Theme customization goes through the library's configuration system
3. Implement the user's requested feature per spec
4. Ensure colors, spacing, and component styles comply with the spec

**Key**: Always load the spec before implementing. Never rely on memory. When using a library, use the library's component API.

---

### check - Audit Spec Compliance

**Input**: File or directory to check

**Flow**:
1. Read the project's UI spec
2. Identify the component solution type
3. Scan the specified code
4. **Library-specific checks** (only when using a component library):
   - Hand-written components that duplicate library components
   - Theme customization bypassing the library's configuration system
   - Incorrect library component prop usage
5. Output violation report

**Output format**:
```
## Check Results

### Violations
- [file:line] Issue description

### Library Violations (if applicable)
- [file:line] Hand-wrote a component available in the library
- [file:line] Directly overrode component styles; should use theme config

### Suggested Fixes
- Specific fix recommendations
```

---

### iterate - Update the Spec

**Trigger**: Missing spec coverage, new component needed, or switching component solution

**Flow**:
1. Confirm with user what needs to be added/modified
2. If switching component solution, flag components that need migration
3. Update spec document
4. Update Demo showcase page
5. Sync related implementation code

---

## Design Principles (General)

### Component Solution
- **Custom components**: Hand-write all UI components, full control
- **Component library**: Use an existing library (shadcn/ui, Ant Design, Element Plus, etc.)
- Choice is made during demo stage, recorded in the spec document
- All subsequent stages automatically follow this choice

### Color System
- **Primary colors**: Primary, Secondary, Background
- **Text colors**: Heading, Body, Muted (multiple levels)
- **Brand accent**: For positive/negative business comparisons
- **System feedback**: Success, Error, Warning, Info

### Typography
- Headings use Serif fonts, body uses Sans-serif
- Clear type scale hierarchy (Display → H1 → H2 → Body → Small)

### Component Styles
- Unified border radius system (e.g., xl, 2xl, 3xl, full)
- Consistent spacing rhythm (multiples of 4px)
- Consistent transition animations

### Responsive
- Mobile-first design
- Key breakpoints: sm(640px), md(768px), lg(1024px)

---

## File Structure

```
ui-design-workflow/
├── SKILL.md              # This file (overview)
├── README.md             # User documentation
├── assets/
│   ├── website.md        # Landing page template structure
│   ├── components.md     # Component library template
│   ├── design-principles.md  # UI design principles
│   ├── spec-template.md  # Spec document template
│   └── library-guide.md  # Component library integration guide
└── references/
    └── modes.md          # Detailed mode specifications
```

---

## Quick Decision Guide

**User says "design UI"** → Use `demo` (analyze project, recommend component solution)
**User says "use shadcn/ui"** → Use `demo` (skip recommendation, use specified library)
**User says "generate spec"** → Use `spec`
**User says "implement feature"** → Use `implement` (read spec first, identify component solution)
**User says "check code"** → Use `check`
**User says "add component spec"** → Use `iterate`
**User says "switch to Ant Design"** → Use `iterate` (switch component solution)
