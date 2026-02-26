# UI Design Workflow Skill

**通用 UI 设计工作流 Skill** for Claude Code - 从组件库 Demo 到规范文档到实际实现的完整流程管理。

适用于任何需要建立和维护 UI 设计规范的前端项目（不使用 shadcn/ui 等 UI 库的项目）。

## 安装

将此仓库克隆到项目的 `.claude/skills/` 目录：

```bash
git clone https://github.com/FrozenMoon/ui-design-workflow.git YOUR_PROJECT/.claude/skills/ui-design-workflow
```

或全局安装（所有项目可用）：

```bash
git clone https://github.com/FrozenMoon/ui-design-workflow.git ~/.claude/skills/ui-design-workflow
```

---

## 🎯 Skill 解决的问题

| 传统方式的问题 | Skill 的解决方案 |
|--------------|---------------|
| ❌ 手动维护 UI 规范，容易遗漏 | ✅ 自动强制读取和应用规范 |
| ❌ AI 可能忘记规范细节 | ✅ 每次开发都强制加载规范 |
| ❌ 没有规范检查机制 | ✅ `check` 命令自动检查违规 |
| ❌ 规范和代码实现脱节 | ✅ `iterate` 模式同步更新 |
| ❌ 团队成员不知道规范存在 | ✅ `spec` 阶段自动项目集成 |
| ❌ UI 风格不一致 | ✅ 完整工作流保证一致性 |
| ❌ 仅看组件库不够直观 | ✅ 提供成品展示（官网 Demo） |

---

## 📦 功能概览

### 5 个核心命令

| 命令 | 功能 | 使用场景 |
|------|------|---------|
| `demo` | 生成 UI 展示（成品 + 组件库） | 项目初期，确定 UI 风格 |
| `spec` | 生成规范文档 + 项目集成 | Demo 确定后，形成规范 |
| `implement` | 按规范实现功能 | 日常开发（最常用） |
| `check` | 检查规范遵守情况 | PR 前检查，定期审查 |
| `iterate` | 迭代更新规范 | 发现规范缺失时 |

---

## 🚀 快速开始

### 新项目从零开始

```bash
# 第 1 步：生成 UI 展示页面（成品 + 组件库）
/ui-design-workflow demo 为我的项目设计简约现代的 UI

# （与 AI 迭代改进 Demo，直到满意）
# 查看：Tab 1 看整体风格，Tab 2 看组件细节

# 第 2 步：生成规范文档 + 自动项目集成
/ui-design-workflow spec

# 第 3 步：日常开发，按规范实现功能
/ui-design-workflow implement 实现用户登录页面

# 第 4 步：PR 前检查规范
/ui-design-workflow check src/pages/Login.tsx

# 第 5 步：规范缺失时更新
/ui-design-workflow iterate 需要添加骨架屏加载效果
```

### 已有规范文档的老项目

如果你的项目已经有 UI 规范文档（如 `doc/UI设计规范.md`），但没有 UI Demo：

```bash
# 基于现有规范生成 Demo（可视化规范）
/ui-design-workflow demo --from-spec

# 然后正常使用 implement 和 check
/ui-design-workflow implement 实现新功能
/ui-design-workflow check src/pages/
```

---

## 📖 详细使用说明

### 命令 1: `demo` - 生成 UI 展示页面（成品 + 组件库）

**目标**：生成一个完整的 UI 展示页面，包含两个 Tab：
- **Tab 1: 成品展示** - 完整官网 Demo，展示实际应用效果
- **Tab 2: 组件库** - 所有组件的各种状态

**为什么包含成品展示？**
- 仅看组件库不够直观，用户看不到实际使用效果
- 成品展示（官网）让用户一眼看到整体风格
- 组件库提供细节和各种状态

**Tab 1: 成品展示（官网 Demo）**
- Hero Section（标题 + CTA 按钮）
- Features Section（核心特性）
- Use Cases Section（使用场景）
- CTA Section（行动号召）
- Footer（页脚）

**Tab 2: 组件库**
- ✅ 颜色系统和排版
- ✅ 按钮（4 种风格 × 3 种尺寸 × 4 种状态）
- ✅ 表单组件（Input, Select, Checkbox, Radio, Switch）
- ✅ 反馈组件（Toast, Alert, Modal, Popover, Tooltip）
- ✅ 卡片、导航、数据展示
- ✅ 滚动条、Loading、Progress 等

**技术栈**：
- 默认：React + TypeScript + Tailwind CSS
- 支持：Vue, Svelte, CSS Modules, UnoCSS 等

**示例**：
```bash
# 默认技术栈
/ui-design-workflow demo 为电商平台设计清新简洁的 UI

# 指定技术栈
/ui-design-workflow demo 使用 Vue 3 + UnoCSS 设计管理后台 UI

# 基于现有规范生成（老项目补 Demo）
/ui-design-workflow demo --from-spec
```

**输出**：
- Next.js: `app/ui-showcase/page.tsx`
- Vite: `src/pages/UIShowcase.tsx`
- HTML: `examples/ui-showcase.html`

**页面结构**：
一个页面，包含两个 Tab：
- 默认显示 Tab 1（成品展示），让用户先看到整体效果
- Tab 2（组件库）提供组件详细状态

---

### 命令 2: `spec` - 生成规范文档 + 自动项目集成

**目标**：将确定的 Demo 总结为项目的 UI 设计规范

**自动完成的工作**：
1. 读取和分析 Demo 代码
2. 提取设计 Token（颜色、排版、间距、圆角等）
3. 生成结构化规范文档（`doc/UI设计规范.md`）
4. **自动检测 AI 工具并完成项目集成**：
   - Cursor/Windsurf → 创建 `.cursor/rules/ui-design.mdc`
   - Claude Code → 创建/更新 `CLAUDE.md`
   - 通用项目 → 在 `README.md` 中添加说明

**示例**：
```bash
# 一键生成规范 + 项目集成
/ui-design-workflow spec
```

**输出**：
```
✅ UI 设计规范已完成！

生成的文件：
1. ✅ UI 设计规范文档：doc/UI设计规范.md
2. ✅ 项目集成已完成（Cursor）
   - 已创建：.cursor/rules/ui-design.mdc

AI 现在会自动知道使用 skill 来开发 UI。
```

---

### 命令 3: `implement` - 按规范实现功能

**目标**：日常开发，严格按规范实现 UI

**执行流程**：
1. **强制加载规范**（Pre-flight Check）
2. 分析用户需求
3. 按规范生成代码
4. 输出完成报告

**示例**：
```bash
# 实现页面
/ui-design-workflow implement 实现用户设置页面

# 实现组件
/ui-design-workflow implement 实现一个可折叠的侧边栏

# 实现功能模块
/ui-design-workflow implement 实现商品卡片列表，包含图片、标题、价格和购买按钮
```

**约束**：
- 🚨 必须先有规范文档，否则拒绝执行
- 🚨 每次都强制读取规范完整内容
- ✅ 自动遵守颜色、间距、圆角等规范
- ✅ 不添加注释标注规范章节

---

### 命令 4: `check` - 检查规范遵守情况

**目标**：自动检测代码是否违反 UI 规范

**检查项**：
- 颜色使用（是否使用规范外的颜色）
- 间距和圆角（是否符合规范定义）
- 布局属性（是否使用了不推荐的写法）
- 组件样式（是否符合规范）
- 动效（是否缺少过渡效果）

**示例**：
```bash
# 检查单个文件
/ui-design-workflow check src/pages/Login.tsx

# 检查整个目录
/ui-design-workflow check src/pages/

# 检查并自动修复
/ui-design-workflow check src/components/Button.tsx --fix
```

**输出示例**：
```
========================================
UI 规范检查报告
========================================

文件：src/pages/Login.tsx
规范：doc/UI设计规范.md

✅ 通过项: 15
⚠️  警告项: 3
❌ 违规项: 2

详细问题：
❌ 第 42 行：使用了禁用的颜色类
   发现：bg-blue-500
   建议：使用规范定义的 bg-primary

⚠️  第 73 行：圆角可能不符合规范
   发现：rounded-lg
   建议：卡片应使用 rounded-2xl

通过率: 75%
```

---

### 命令 5: `iterate` - 迭代更新规范

**目标**：当实现新功能时发现规范缺失，先更新规范再实现

**执行流程**：
1. 识别新需求
2. 与用户讨论设计决策
3. 更新规范文档
4. 可选：立即按新规范实现功能

**示例**：
```bash
# 添加新组件规范
/ui-design-workflow iterate 需要添加 Tooltip 组件的规范

# 添加新的视觉效果
/ui-design-workflow iterate 需要为加载状态添加骨架屏规范

# 扩展颜色系统
/ui-design-workflow iterate 需要为深色模式添加颜色变量
```

---

## 🎨 技术栈支持

### 默认技术栈
- **框架**：React
- **语言**：TypeScript
- **样式**：Tailwind CSS
- **构建工具**：Vite / Next.js

### 支持的技术栈
- Vue 3 + Composition API + Tailwind CSS
- Svelte + Tailwind CSS
- React + CSS Modules
- Vue + UnoCSS
- 纯 HTML + CSS

### 如何指定技术栈
在调用 `demo` 命令时说明：
```bash
/ui-design-workflow demo 使用 Vue 3 + UnoCSS 设计后台管理系统
/ui-design-workflow demo 使用 Svelte + Tailwind 设计落地页
```

---

## 📂 文件结构

```
.claude/skills/ui-design-workflow/
├── SKILL.md                           # 主 Skill 文件（核心逻辑）
├── README.md                          # 本文件（使用说明）
└── assets/
    ├── design-principles.md           # UI 设计基本原则（demo 阶段参考）
    └── spec-template.md               # 规范文档模板（spec 阶段使用）
```

---

## 🔄 完整工作流图

```
项目初期                    Demo 确定                日常开发
   ↓                          ↓                        ↓
 demo ──(迭代)──→ demo ──→  spec  ──────→  implement ← iterate
   ↓                          ↓                        ↑
产出组件库展示            生成规范文档              发现规范缺失
                        + 自动项目集成                ↓
                                                  更新规范
                                                      │
                                                      ↓
                                                    check
                                                      ↓
                                              定期检查/PR前检查
```

---

## 💡 最佳实践

### 项目初期
1. 先与产品/设计团队对齐整体风格方向
2. 使用 `demo` 命令生成组件库展示
3. 与团队一起 Review Demo，迭代改进
4. 确定后立即执行 `spec` 生成规范

### 日常开发
1. **所有 UI 开发都通过 `implement` 命令**
2. 不要绕过 skill 直接修改 UI（除非紧急情况）
3. PR 前使用 `check` 命令检查

### 规范维护
1. 每季度 Review 一次规范文档
2. 发现规范缺失立即使用 `iterate` 更新
3. 保持规范的版本号和更新日志

### 团队协作
1. 在项目 README 中说明 UI 规范的存在
2. 新成员入职时介绍 skill 的使用
3. 建立规范 Review 机制

---

## 🔧 项目集成（自动完成）

在执行 `spec` 命令时，Skill 会自动检测项目使用的 AI 工具并完成集成：

### Cursor / Windsurf
自动创建 `.cursor/rules/ui-design.mdc`：
```markdown
---
description: UI 设计规范 - UI 相关开发必须遵守
globs: ["src/**/*", "app/**/*"]
alwaysApply: true
---

开发 UI 时必须使用 `/ui-design-workflow implement`
```

### Claude Code
自动创建/更新 `CLAUDE.md`：
```markdown
## UI 开发规范

开发 UI 时必须使用 `/ui-design-workflow implement`
```

### 通用项目
在 `README.md` 中添加 UI 规范说明。

---

## ❓ 常见问题

### Q1: 老项目已有 UI 规范，但没有 Demo，怎么办？

使用 `demo --from-spec` 基于现有规范生成 Demo：
```bash
/ui-design-workflow demo --from-spec
```

这样可以：
- 将规范可视化
- 发现规范中的缺失
- 为新团队成员提供参考

### Q2: 可以不使用 skill，直接手动开发 UI 吗？

可以，但不推荐。如果确实需要：
1. 手动阅读并严格遵守 `doc/UI设计规范.md`
2. 完成后使用 `check` 命令检查
3. 修复所有违规项

### Q3: 规范文档可以放在其他位置吗？

可以。Skill 会自动检测以下位置：
- `doc/UI设计规范.md`（优先）
- `doc/shared/UI设计规范.md`
- `docs/ui-design-spec.md`
- `docs/design-system.md`

### Q4: 技术栈不支持怎么办？

在调用 `demo` 时说明你的技术栈，AI 会尝试生成对应的代码。例如：
```bash
/ui-design-workflow demo 使用 Angular + SCSS
```

### Q5: 多人协作时如何保持规范一致？

1. 所有 UI 开发都通过 skill（项目集成会提示 AI）
2. PR Review 时使用 `check` 命令
3. 定期团队 Review 规范文档

### Q6: 规范文档太长，AI 会遗漏吗？

不会。`implement` 模式会**强制读取规范完整内容**并注入上下文，确保不会遗漏。

---

## 📊 对比：使用 Skill vs 不使用

| 对比项 | 不使用 Skill | 使用 Skill |
|--------|------------|-----------|
| **规范建立** | 手动编写，费时费力 | Demo → Spec 自动生成 |
| **规范遵守** | 依赖开发者记忆 | 自动强制加载规范 |
| **规范检查** | 人工 Review | 自动 check 命令 |
| **规范更新** | 手动更新文档 | iterate 模式同步 |
| **团队协作** | 需要培训和文档 | 项目集成自动提示 |
| **一致性** | 容易出现差异 | 强制保证一致 |

---

## 🌟 为什么选择这个 Skill？

1. ✅ **节省时间**：自动生成规范文档，无需手动编写
2. ✅ **保证质量**：强制规范检查，防止违规代码
3. ✅ **易于维护**：规范和代码实现同步迭代
4. ✅ **团队协作**：自动项目集成，无需额外培训
5. ✅ **通用性强**：适用于任何前端项目和技术栈

---

## 📝 License

MIT

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

---

**Skill 版本**：1.0
**最后更新**：2026-02-25
**作者**：[你的名字]
