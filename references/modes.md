# Mode Details

Detailed execution flows and output formats for each command.

---

## demo Mode

### Four Entry Points

**How to determine which flow to use**:
1. Does the project have an existing spec (`doc/ui-design-spec.md`)? → **Flow B**
2. Did the user specify a component library in the command? → **Flow C**
3. Does the project have significant existing UI code (5+ components or 3+ pages with UI)? → **Flow D**
4. Otherwise → **Flow A**

**Flow A: From Scratch**
- User has no existing spec, project has little or no existing UI code
- **Step 1**: Analyze the project (package.json, code structure, tech stack, project type)
- **Step 1.5**: Scan existing components (see "Existing Component Scan" below)
- **Step 2**: Auto-select a component solution based on the analysis
- **Step 3**: ⛔ **Visual Style Preview** — Generate `style-preview.html` with 3 style previews. User opens in browser, picks one (see "Style Confirmation" below). DO NOT proceed without choice.
- **Step 3.5**: Ask theme mode (light / dark / toggle)
- **Step 4**: Design Thinking — refine the user's chosen direction with detailed tokens
- **Step 5**: Create real component files
- **Step 6**: Create showcase page that imports and displays the components
- **Step 7**: Tab 1 Landing Page also uses the same components

**Flow B: Based on Existing Spec**
- User has an existing spec document
- Read the spec and identify the component solution
- Read the Component Registry to find existing components
- Generate the corresponding Demo (importing existing components)
- Flag components missing from the registry

**Flow C: Specified Component Library**
- User specifies a library directly in the command (e.g., "use shadcn/ui")
- Skip the recommendation step and use the specified library directly
- Style preferences still need to be confirmed (Round 1 + Round 2)

**Flow D: Adopt Existing UI**
- Project has significant existing UI code but no spec document
- Focus is on **extraction and documentation**, not creation
- See "Flow D: Adopt Existing UI — Detailed Steps" below

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

### Existing Component Scan

For projects that already have code, scan for existing components and present the findings to the user:

**What to scan**:
- Component directories (e.g., `src/components/`, `src/ui/`, `components/`)
- Pages that use custom or library components
- Shared utilities, hooks, or wrappers related to UI

**Present scan results to the user**:

```
🔍 Existing Components Found:

Components (N total):
- Button (src/components/Button.tsx) — 3 variants
- Modal (src/components/Modal.tsx)
- DataTable (src/components/DataTable.tsx)
- ...

Assessment:
✅ Consistent: [list components with consistent styling]
⚠️ Inconsistent: [list components with style drift — e.g., mixed border-radius, hardcoded colors]
❌ Severe issues: [list components with major problems — e.g., accessibility violations, broken responsiveness]

Recommendation:
- Existing components will be preserved as-is and included in the showcase
- [If inconsistencies found]: Suggest unifying [specific aspects] in future iterations
- [If severe issues found]: Recommend fixing [specific components] — [reason]
```

**Key principles**:
- **Do not modify existing components** during the demo phase
- Include all existing components in the Tab 2 showcase alongside new components
- Only suggest modifications for severe issues (accessibility violations, broken layouts); present as recommendations, not automatic changes
- Record existing component inventory for the spec phase to reference
- New components should match the existing project's visual patterns (not the other way around)

### Design Thinking Step (CRITICAL)

> **Prerequisite**: User MUST have answered the style preference questions (Step 3) before this step begins. If the user has not answered, go back and ask.

After project analysis and **after receiving user's style preferences**, read [references/frontend-aesthetics.md](../references/frontend-aesthetics.md) and execute the design thinking process:

1. **Choose aesthetic direction**: Based on **user's stated preferences** and project context, pick a bold tone (brutalist, editorial, luxury, organic, retro-futuristic, etc.)
2. **Select distinctive typography**: Choose a characterful heading font + refined body font. NEVER use Inter, Roboto, Arial, or Helvetica as primary choices.
3. **Build emotional color palette**: Dominant + accent model. Palette must evoke a specific feeling. Avoid purple-on-white, teal/coral, or unmodified Tailwind grays.
4. **Plan atmospheric details**: Background treatments (gradients, textures, patterns), motion design (staggered page load, scroll reveals), visual depth
5. **Define the memorable element**: What ONE thing will someone remember about this design?

⛔ **BLOCKING**: Present the design direction to the user and **WAIT for their confirmation**. DO NOT generate any component code until the user approves or adjusts this direction:

```
🎨 Design Direction:

Aesthetic: [Chosen direction — e.g., "Editorial luxury with warm undertones"]
Memorable Element: [e.g., "Dramatic serif typography with oversized display text"]
Heading Font: [Font name] (from [source])
Body Font: [Font name] (from [source])
Color Mood: [e.g., "Warm cream background with deep charcoal and terracotta accent"]
Atmosphere: [e.g., "Subtle grain texture, soft radial highlights, staggered entrance animations"]

Please confirm this direction, or tell me what you'd like to adjust.
```

### Style Confirmation: Visual Preview Page (BLOCKING)

> ⛔ **BLOCKING CHECKPOINT**: You MUST generate a visual preview page and WAIT for the user to pick a style. DO NOT assume defaults. DO NOT skip. DO NOT proceed to component creation without the user's confirmed choice.

**Component solution is NOT asked here** — it is auto-determined from the project analysis in Step 2.

#### Step 1: Generate Preview Page + Start Server

1. Read the [style preview template](../assets/style-preview-template.md) and generate `style-preview.html` in the project root. The file contains 3 style direction previews, each with:
   - Real fonts loaded from Google Fonts CDN
   - Actual color palette rendered as color blocks
   - A mini Hero section (headline + body text + CTA button) rendered in the real fonts and colors
   - Background atmosphere (gradient, texture, etc.)
   - Border radius shown on buttons and card edges

2. Start the local Node.js preview server in background (see server script in the template). The server:
   - Serves `style-preview.html` at `http://localhost:19836`
   - Receives user's selection via POST `/choose` and writes `.style-choice` file

**Rules for generating the 3 options**:
- 3 **diverse** directions — don't offer 3 variants of the same style
- Real Google Fonts — NEVER Inter, Roboto, Arial, or Helvetica as primary heading fonts
- Context-aware — options should make sense for the project type
- Use the actual project name in sample headlines if available

#### Step 2: Tell User to Open Preview

```
🎨 Style preview ready! Open in your browser:
   http://localhost:19836

   A. [Style Name] — [One-sentence description]
   B. [Style Name] — [Description]
   C. [Style Name] — [Description]

Click a card and press "Confirm Selection" — I'll know your choice automatically.
Or tell me: "new batch" to regenerate / describe your own direction.
```

#### Step 3: Wait for User Choice

Poll for `.style-choice` file (check every 2 seconds). When it appears, read the JSON content:
```json
{"choice": "B", "name": "Editorial"}
```

Alternatively, the user may reply in chat instead of clicking — handle both:

| Source | Action |
|--------|--------|
| `.style-choice` file detected | Read choice, proceed to theme mode question. |
| User says "A" / "B" / "C" in chat | Use that direction. Proceed to theme mode question. |
| User says "new batch" / "换一批" | Regenerate 3 new options, overwrite `style-preview.html`. Tell user to refresh browser. |
| User describes a custom direction | Proceed with that direction. |

#### Step 4: Theme Mode (after style is confirmed)

Ask about theme mode (functional choice, no visual preview needed):
- Single theme (light)
- Single theme (dark)
- Light + Dark toggle

#### Step 5: Clean Up

After user confirms both style direction and theme mode:
1. Kill the preview server process
2. Delete `style-preview.html` and `.style-choice` from project root
3. Proceed to component creation with the confirmed direction

**DO NOT write any component code until the user confirms both the style direction and theme mode.**

### Component Creation Step

After design direction is confirmed, create real component files:

1. **Set up design tokens**: Create/update CSS variables file (colors, fonts, spacing)
2. **Create component files**: Each component as its own file in `src/components/ui/`
   - Export typed props with all variants and states
   - Use design tokens (CSS variables) — never hardcode
   - Include transitions, animations, focus states, ARIA attributes
3. **Skip components that already exist** in the project (found during scan)
4. **For component library mode**: Install/add library components, apply theme configuration

### Showcase Pages Creation Step

After component files are created, build **two separate pages** that import them:

1. **Landing Page Demo** (`/ui-showcase`): A real product page built with the components.
2. **Component Library** (`/ui-components`): Import and render each component in all variants/states.
3. Both pages share a **navigation bar** with links to each other (e.g., "Demo" / "Components" nav items). The nav bar should match the project's design style.
4. Both pages use the **same real components** — no separate inline implementations
5. Do NOT use tabs — these are independent pages

### Output Completion Prompt

```
✅ UI Demo generated:

Component Solution: [Custom / shadcn/ui / ...]

Files created:
📦 Components:
- src/components/ui/button.tsx
- src/components/ui/input.tsx
- src/components/ui/card.tsx
- ... (N total)

📄 Pages:
- [app/ui-showcase/page.tsx] — Landing Page Demo
- [app/ui-components/page.tsx] — Component Library

📱 Landing Page Demo (/ui-showcase):
- Hero, Features, Use Cases, CTA, Footer
- Built with the real components above
- Link to Component Library in footer

🎨 Component Library (/ui-components):
- Color system, Typography
- All 8 core components in all variants/states
- Existing project components: [list from scan]
- Link back to Landing Page Demo

Existing Components:
- [N] components found and included in Component Library
- [Assessment summary: consistent / needs attention]

Preview:
- Landing Page: Visit /ui-showcase
- Component Library: Visit /ui-components

You can continue adjusting colors, border radius, spacing, etc.
When satisfied, use /ui-design-workflow spec to generate the spec document.
```

---

### Flow D: Adopt Existing UI — Detailed Steps

For projects that already have significant UI code but no spec document. The goal is to **extract and document** the existing design system, not to redesign it.

#### Step 1: Deep Scan

Go beyond the basic component scan — analyze the full design surface:

**Components**:
- Scan all component directories (`src/components/`, `src/ui/`, `components/`, etc.)
- For each component: name, path, props/variants, states, usage count across pages

**Design Tokens** (extract from code):
- **Colors**: Collect all color values from CSS/Tailwind config/CSS variables/inline styles. Group into categories (brand, text, background, border, feedback)
- **Typography**: Identify fonts used (font-family declarations, Google Fonts imports, Tailwind font config), font sizes, weights, line heights
- **Spacing**: Common padding/margin/gap values
- **Border radius**: All radius values in use
- **Shadows**: Box-shadow values
- **Animations/transitions**: Transition durations, easing functions, keyframe animations

**Patterns**:
- Layout patterns (grid systems, container widths, breakpoints)
- Component composition patterns (how components are nested/combined)
- State management patterns for UI (modals, toasts, theme)

#### Step 2: Present Extraction Results

Use `AskUserQuestion` to present findings and confirm:

```
🔍 Existing UI Analysis Complete:

Components: [N] found
- [List top components with path and variant count]

Design Tokens Extracted:
🎨 Colors: [N] unique values → grouped into [N] semantic categories
🔤 Fonts: [Font names found]
📐 Spacing: [Base unit detected, e.g., "4px grid" or "inconsistent"]
📏 Border Radius: [Values found]
🌗 Theme: [Single / Light-dark / detected theme approach]

Consistency Assessment:
✅ Consistent: [aspects that are uniform]
⚠️ Inconsistent: [aspects with drift — e.g., "3 different border-radius values used randomly"]
❌ Issues: [severe problems, if any]
```

Then ask via `AskUserQuestion`:
- "Does this analysis look accurate?" → "Yes, proceed" / "Let me correct some things"

#### Step 3: Gap Analysis

Identify what's missing or inconsistent:

```
📋 Gap Analysis:

Missing from a complete design system:
- [ ] [e.g., "No centralized CSS variables — colors are hardcoded across 12 files"]
- [ ] [e.g., "No loading states (spinner/skeleton) found"]
- [ ] [e.g., "No toast/notification component"]

Inconsistencies to resolve:
- [ ] [e.g., "Border radius uses both 4px and 8px — recommend standardizing"]
- [ ] [e.g., "Two different button implementations in different pages"]

Recommendations:
1. [Priority fixes]
2. [Nice-to-have improvements]
```

Ask via `AskUserQuestion`:
- "How would you like to handle the gaps?" → "Generate spec as-is, fix later" / "Fix critical gaps now, then generate spec" / "Let me decide per item"

#### Step 4: Generate Spec

Based on extracted data, generate the spec document (`doc/ui-design-spec.md`):
- Design tokens come from **actual code**, not invented
- Component Registry reflects **actual components**, not templates
- Inconsistencies are documented in the spec's changelog as "known issues"
- If user chose to fix gaps, create missing components/tokens first

#### Step 5: Generate Showcase (Optional)

Ask via `AskUserQuestion`:
- "Would you like a showcase page for existing components?" → "Yes, create showcase" / "No, spec is enough"

If yes, create a showcase page that **imports existing components** (does NOT create new ones) and displays them in all variants/states.

#### Step 6: Update Agent Config

Same as other flows — detect CLAUDE.md/AGENTS.md and write spec reference.

#### Output Completion Prompt

```
✅ Existing UI adopted:

Extraction Summary:
📦 Components registered: [N]
🎨 Design tokens extracted: [colors: N, fonts: N, spacing: N, radius: N]
⚠️ Known inconsistencies: [N] (documented in spec changelog)
🔧 Gaps fixed: [N] / Gaps deferred: [N]

Files created/updated:
- doc/ui-design-spec.md (spec + Component Registry)
- [CLAUDE.md / AGENTS.md] (spec reference added)
- [app/ui-showcase/page.tsx] (if showcase was requested)

Next steps:
- Use /ui-design-workflow implement to build features using the spec
- Use /ui-design-workflow iterate to fix deferred inconsistencies
- Use /ui-design-workflow check to audit new code against the spec
```

---

## spec Mode

### Input

Confirmed Demo code (component files + showcase page)

### Output

1. **Spec Document**: `doc/ui-design-spec.md` (includes Component Registry)
2. **Project Integration**: Update CLAUDE.md

### Spec Document Structure

```markdown
# [Project Name] UI Design Spec

## 1. Design Philosophy
- Aesthetic direction and tone
- Memorable element
- Design rationale

## 2. Component Solution
- Solution type (Custom / Library name)
- Library version (if applicable)
- Theme configuration method and file path
- Usage rules

## 3. Color System

## 4. Typography System

## 5. Spacing & Border Radius

## 6. Shadows & Animations

## 7. Component Registry ← Lists components with paths, NOT code examples
- Registry table (component → path → variants → states)
- Library component mapping (if applicable)

## 8. Atmosphere & Visual Details

## 9. Don'ts List

## 10. Responsive Design

## 11. Accessibility

## 12. Changelog
```

Detailed template available at [assets/spec-template.md](../assets/spec-template.md).

### How Spec Generates the Component Registry

1. Scan all component files created during the demo phase
2. For each component, record:
   - Component name
   - File path
   - Available variants (from props/types)
   - Supported states
   - Brief notes (icon support, composability, etc.)
3. For existing project components found during scan, add them to the registry too
4. For component library solutions, add the library mapping table

### Agent Config File Update

Write the spec reference into the project's agent configuration file(s) so that any AI agent automatically reads the spec during development.

**Detection logic**:
1. Check the project root for `CLAUDE.md` and `AGENTS.md`
2. If both exist → append to both
3. If only one exists → append to that one
4. If neither exists → create `CLAUDE.md`

Append the following content:
```markdown
## UI Design Spec

This project follows the design spec defined in `doc/ui-design-spec.md`.

When developing UI-related features, you must:
1. Read the UI Design Spec first
2. Check the Component Registry — reuse existing components, do not duplicate
3. Use the design tokens (colors, spacing, typography) defined in the spec
4. For new components: follow the spec's design tokens, then add the component to the registry via `iterate`
```

---

## implement Mode

### Key Flow

```
1. Check whether the project has a UI spec
   ↓
2. If yes, read the spec document first
   ↓
3. Check the Component Registry for existing components that can be reused
   ↓
4. For components that exist in the registry:
   - Read the component's source file to understand its API
   - Import and use it — do NOT create a new version
   ↓
5. For new components needed:
   - Create the component file following the spec's design tokens
   - Use the same patterns as existing components in the registry
   ↓
6. Implement the user's requested feature
   ↓
7. If a new reusable component was created:
   - Notify the user that it should be added to the registry via `iterate`
```

### Mandatory Rules

- **Read the spec before writing code**
- **Check the Component Registry before creating any UI component**
- Use the design tokens (CSS variables) defined in the spec
- Use the border radius and spacing defined in the spec
- When creating new components, follow the same patterns as existing registry components
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
1. Whether colors use spec-defined CSS variables (not hardcoded values)
2. Whether spacing conforms to the spec's grid system
3. Whether existing registry components are reused (not duplicated)
4. Whether new components follow the spec's design tokens

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

#### Component Reuse Violations
- `src/pages/Home.tsx:23` hand-writes a Button instead of importing from `@/components/ui/button`
- `src/features/Auth.tsx:45` creates an inline card style instead of using `@/components/ui/card`

#### Color Violations
- `src/components/Header.tsx:15` uses `#333`, should use `var(--foreground)` or `text-foreground`

#### Spacing Violations
- `src/pages/Home.tsx:42` padding uses `13px`, should be `12px` (3*4)

#### Library Violations (if applicable)
- `src/components/Card.tsx:8` directly overrides component className, should customize through variants

### Recommendations
1. Import existing components from the registry instead of recreating them
2. Replace hardcoded color values with CSS variables
3. Check that spacing values are multiples of 4px

### Summary
- Files checked: X
- Violations found: Y
- Component reuse rate: Z% (components from registry vs. hand-written)
- Severity: Low / Medium / High
```

---

## iterate Mode

### Trigger Scenarios

- A new reusable component was created during `implement` and needs to be registered
- A missing component is discovered in the registry
- A design token needs to be added or modified
- **Switching component solutions** (e.g., from custom to a component library)

### Flow

```
1. Confirm the content to add/modify
   ↓
2. If adding a new component to the registry:
   - Verify the component file exists and is well-structured
   - Add it to the Component Registry in the spec
   - Add it to the showcase page
   ↓
3. If modifying design tokens:
   - Update the spec document
   - Update the CSS variables file
   - Check if existing components need adjustments
   ↓
4. If switching component solutions:
   - List the components that need to be migrated
   - Update the Component Registry
   ↓
5. Update the spec document
   ↓
6. Update the Demo showcase page (if needed)
   ↓
7. Synchronize updates to related implementation code (if needed)
```

### Output

```
✅ Spec updated

Changes:
- [Added/Modified/Migrated] Component Name: Details

Files updated:
- doc/ui-design-spec.md (Component Registry updated)
- src/components/ui/[component].tsx (if component file created/modified)
- app/ui-showcase/page.tsx (if showcase updated)
```
