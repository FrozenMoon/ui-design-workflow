# UI Design Workflow Skill

[English](README.md) | [中文](README.zh-CN.md)

> AI 写一个页面可以很精美，但真正的挑战是：当你的产品有几十个页面时，如何让每一个页面都保持同样的审美水准和视觉一致性？
>
> 没有规范约束的 AI 会在每次对话中「重新发明」UI 风格——颜色偏移、间距混乱、组件长相各异。页面越多，混乱越明显。
>
> **这个 Skill 解决的就是这个问题。**

从 UI Demo 到设计规范到日常开发，完整管控你的产品视觉一致性。

适用于任何前端项目，支持自定义组件和组件库（shadcn/ui, Ant Design, Element Plus 等）。
自动分析项目技术栈，推荐最合适的组件方案。

支持 Claude Code、Codex、Cursor、Cline、Gemini CLI 等 40+ AI 编程工具。

**实际案例**：[Input Translator](https://www.inputtranslator.com/) — 完全使用本 Skill 开发。

## 安装

### 推荐：npx skills（支持多 Agent）

```bash
npx skills add FrozenMoon/ui-design-workflow
```

交互式引导选择安装到哪些 Agent（Claude Code、Codex、Cursor 等），一次安装，多个工具同时生效。

### 手动安装：git clone

安装到当前项目：

```bash
git clone https://github.com/FrozenMoon/ui-design-workflow.git YOUR_PROJECT/.claude/skills/ui-design-workflow
```

全局安装（所有项目可用）：

```bash
git clone https://github.com/FrozenMoon/ui-design-workflow.git ~/.claude/skills/ui-design-workflow
```

---

## 5 个核心命令

| 命令 | 功能 | 使用场景 |
|------|------|---------|
| `demo` | 分析项目 + 生成 UI 展示 | 项目初期，确定风格和组件方案 |
| `spec` | 生成规范文档 + 项目集成 | Demo 确定后，形成规范 |
| `implement` | 按规范实现功能 | 日常开发（最常用） |
| `check` | 检查规范遵守情况 | PR 前检查，定期审查 |
| `iterate` | 迭代更新规范 | 发现规范缺失时 |

---

## 快速开始

### 新项目

```bash
# 第 1 步：生成 UI 展示页面
/ui-design-workflow demo 为我的项目设计简约现代的 UI

# 第 2 步：生成规范文档
/ui-design-workflow spec

# 第 3 步：日常开发
/ui-design-workflow implement 实现用户登录页面

# 第 4 步：PR 前检查
/ui-design-workflow check src/pages/Login.tsx

# 第 5 步：规范缺失时更新
/ui-design-workflow iterate 需要添加骨架屏加载效果
```

### 指定组件库

```bash
/ui-design-workflow demo 使用 shadcn/ui 设计后台管理系统
/ui-design-workflow demo 使用 Ant Design 设计企业管理平台
/ui-design-workflow demo 使用自定义组件设计品牌官网
```

### 已有规范的老项目

```bash
/ui-design-workflow demo --from-spec
```

---

## 支持的技术栈

React、Vue 3、Svelte、纯 HTML + CSS 等。默认：React + TypeScript + Tailwind CSS。

**组件库**：shadcn/ui、Ant Design、Element Plus、Chakra UI，或任何你指定的库。未指定时 Skill 会自动分析并推荐。

---

## 常见问题

**已有规范但没有 Demo？**
执行 `/ui-design-workflow demo --from-spec`。

**支持哪些组件库？**
任何组件库。在 `demo` 命令中指定：`/ui-design-workflow demo 使用 Mantine UI 设计应用`。

**项目已经在用 Ant Design？**
先执行 `spec`，会自动检测并记录。之后 `implement` 会自动使用 Ant Design。

**中途从自定义切换到组件库？**
`/ui-design-workflow iterate 将组件方案从自定义切换到 shadcn/ui`

---

## License

MIT

---

## 贡献

欢迎提交 Issue 和 Pull Request！

---

**Skill 版本**：2.0
**最后更新**：2026-03-06
**作者**：RedCat
