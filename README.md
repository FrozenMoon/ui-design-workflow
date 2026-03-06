# UI Design Workflow Skill

[English](README.md) | [中文](README.zh-CN.md)

> AI can make a single page look stunning. But the real challenge is: when your product has dozens of pages, how do you keep every one of them at the same level of polish and visual consistency?
>
> Without spec constraints, AI "reinvents" the UI style in every conversation — colors drift, spacing breaks, components look different. The more pages you build, the worse it gets.
>
> **This skill solves that problem.**

End-to-end visual consistency for your product — from UI Demo to design spec to daily development.

Works with any frontend project. Supports both custom components and component libraries (shadcn/ui, Ant Design, Element Plus, etc.).
Auto-analyzes your tech stack and recommends the best component solution.

Compatible with Claude Code, Codex, Cursor, Cline, Gemini CLI, and 40+ AI coding tools.

## Installation

### Recommended: npx skills (multi-agent support)

```bash
npx skills add FrozenMoon/ui-design-workflow
```

Interactive setup to choose which agents to install to (Claude Code, Codex, Cursor, etc.). One install, all tools supported.

### Manual: git clone

Install to current project:

```bash
git clone https://github.com/FrozenMoon/ui-design-workflow.git YOUR_PROJECT/.claude/skills/ui-design-workflow
```

Global install (available to all projects):

```bash
git clone https://github.com/FrozenMoon/ui-design-workflow.git ~/.claude/skills/ui-design-workflow
```

---

## 5 Core Commands

| Command | Function | When to Use |
|---------|----------|-------------|
| `demo` | Analyze project + generate UI showcase | Early stage: establish style & component solution |
| `spec` | Generate spec document + project integration | After Demo is confirmed |
| `implement` | Build features per spec | Daily development (most used) |
| `check` | Audit spec compliance | Before PR, periodic review |
| `iterate` | Update the spec | When gaps are discovered |

---

## Quick Start

### New Project

```bash
# Step 1: Generate UI showcase page
/ui-design-workflow demo design a clean modern UI for my project

# Step 2: Generate spec document
/ui-design-workflow spec

# Step 3: Daily development
/ui-design-workflow implement build the user login page

# Step 4: Pre-PR check
/ui-design-workflow check src/pages/Login.tsx

# Step 5: Update spec when gaps are found
/ui-design-workflow iterate add skeleton loading spec
```

### Specify a Component Library

```bash
/ui-design-workflow demo use shadcn/ui to design an admin dashboard
/ui-design-workflow demo use Ant Design to design an enterprise platform
/ui-design-workflow demo use custom components to design a brand website
```

### Existing Project with Spec

```bash
/ui-design-workflow demo --from-spec
```

---

## Supported Tech Stacks

React, Vue 3, Svelte, Plain HTML + CSS, and more. Default: React + TypeScript + Tailwind CSS.

**Component Libraries**: shadcn/ui, Ant Design, Element Plus, Chakra UI, or any library you specify. Not specified? The skill auto-analyzes and recommends.

---

## FAQ

**Already have a spec but no Demo?**
Run `/ui-design-workflow demo --from-spec`.

**Which component libraries are supported?**
Any. Specify in the `demo` command: `/ui-design-workflow demo use Mantine UI to design an app`.

**Project already uses Ant Design?**
Run `spec` first — it auto-detects and records. Then `implement` uses it automatically.

**Switch from custom to a library mid-project?**
`/ui-design-workflow iterate switch component solution from custom to shadcn/ui`

---

## License

MIT

---

## Contributing

Issues and Pull Requests are welcome!

---

**Skill version**: 2.0
**Last updated**: 2026-03-06
**Author**: RedCat
