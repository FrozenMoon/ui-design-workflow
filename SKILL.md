---
name: ui-design-workflow
description: >
  MUST use when implementing UI components or frontend pages in this project.
  Triggers: 实现页面, 开发UI, 写组件, 前端开发, button, form, modal, toast,
  card, input, 样式, 界面, designing UI, implement page, create component.
  Before writing any UI code, load this skill to read the project's design spec.
---

# UI Design Workflow

管理 UI 设计工作流：Demo → 规范 → 实现 → 检查 → 迭代。

## 命令速查

| 命令 | 用途 | 触发场景 |
|------|------|---------|
| `demo` | 生成 UI 展示页面 | 项目初期确定风格 |
| `spec` | 生成规范文档 | Demo 确认后 |
| `implement` | 按规范实现功能 | 日常开发 |
| `check` | 检查规范遵守 | PR 前检查 |
| `iterate` | 迭代更新规范 | 发现规范缺失 |

---

## 命令详情

### demo - 生成 UI 展示页面

**输入**: 用户描述的 UI 风格需求（如"简约现代"、"科技感"）

**输出**: 单页面包含两个 Tab：
- **Tab 1: 成品展示** - 完整官网 Demo
- **Tab 2: 组件库** - 所有组件的各种状态

**流程**:
1. 与用户确认：主题模式（单一/明暗切换）、风格偏好
2. 设计颜色系统、排版、组件样式
3. 生成 UI 展示页面
4. 与用户迭代调整

**输出位置**:
- Next.js: `app/ui-showcase/page.tsx`
- Vite: `src/pages/UIShowcase.tsx`

**详细模板**: 见 [templates/website.md](templates/website.md) 和 [templates/components.md](templates/components.md)

---

### spec - 生成规范文档

**前提**: 已有确认的 Demo

**输出**:
1. 规范文档: `doc/UI设计规范.md`
2. 项目集成: 更新 CLAUDE.md 引用规范

**流程**:
1. 读取 Demo 代码，提取设计决策
2. 生成结构化规范文档
3. 更新 CLAUDE.md 添加规范引用

---

### implement - 按规范实现功能

**前提**: 项目已有 UI 规范

**流程**:
1. **必须**先读取项目的 UI 规范文档
2. 按规范实现用户请求的功能
3. 确保颜色、间距、组件样式符合规范

**关键**: 实现前必须加载规范，不要凭记忆实现。

---

### check - 检查规范遵守

**输入**: 要检查的文件或目录

**流程**:
1. 读取项目 UI 规范
2. 扫描指定代码
3. 输出违规报告

**输出格式**:
```
## 检查结果

### 违规项
- [文件:行号] 问题描述

### 建议修复
- 具体修复建议
```

---

### iterate - 迭代更新规范

**触发场景**: 发现规范缺失或需要新增组件

**流程**:
1. 与用户确认需要补充的内容
2. 更新规范文档
3. 更新 Demo 展示页面
4. 同步更新相关实现代码

---

## 设计原则（通用）

### 颜色系统
- **主色调**: Primary, Secondary, Background
- **文本色**: Heading, Body, Muted（多层级）
- **品牌强调色**: 用于业务场景的正面/负面对比
- **系统反馈色**: Success, Error, Warning, Info

### 排版
- 标题使用 Serif 字体，正文使用 Sans-serif
- 建立清晰的字号层级（Display → H1 → H2 → Body → Small）

### 组件样式
- 统一的圆角体系（如 xl, 2xl, 3xl, full）
- 统一的间距规律（4px 倍数）
- 一致的过渡动画

### 响应式
- Mobile-first 设计
- 关键断点：sm(640px), md(768px), lg(1024px)

---

## 文件结构

```
ui-design-workflow/
├── SKILL.md              # 本文件（概览）
├── README.md             # 用户文档
├── templates/
│   ├── website.md        # 官网模板结构
│   └── components.md     # 组件库模板
└── references/
    └── modes.md          # 各模式详细说明
```

---

## 快速决策

**用户说"设计 UI"** → 用 `demo`
**用户说"生成规范"** → 用 `spec`
**用户说"实现某功能"** → 用 `implement`（先读规范）
**用户说"检查代码"** → 用 `check`
**用户说"新增组件规范"** → 用 `iterate`
