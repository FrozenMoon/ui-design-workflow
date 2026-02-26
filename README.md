# UI Design Workflow Skill

**通用 UI 设计工作流 Skill** - 为 Claude Code 打造的 UI 设计全流程管理工具。

从组件库 Demo 到设计规范到实际实现的完整流程管理，适用于任何前端项目。

## 功能特点

- **Demo 生成**：生成包含成品展示和组件库的 UI 展示页面
- **规范生成**：从 Demo 自动提取设计规范文档
- **规范实现**：按规范实现 UI 功能，强制加载规范防止遗漏
- **规范检查**：自动检测代码是否违反 UI 规范
- **规范迭代**：发现规范缺失时，同步更新规范和代码

## 安装方式

### 方式一：通过 URL 安装（推荐）

在 Claude Code 中运行：

```bash
/install-skill https://github.com/FrozenMoon/ui-design-workflow
```

### 方式二：手动安装到项目

将 `skills/ui-design-workflow` 目录复制到你的项目的 `.claude/skills/` 目录下：

```bash
# 克隆仓库
git clone https://github.com/FrozenMoon/ui-design-workflow.git

# 复制到项目
cp -r ui-design-workflow/skills/ui-design-workflow YOUR_PROJECT/.claude/skills/
```

### 方式三：全局安装

将 skill 安装到个人 Claude 目录，所有项目都可使用：

```bash
# 复制到全局 skills 目录
cp -r ui-design-workflow/skills/ui-design-workflow ~/.claude/skills/
```

## 快速开始

### 新项目从零开始

```bash
# 1. 生成 UI 展示页面（成品 + 组件库）
/ui-design-workflow demo 为我的项目设计简约现代的 UI

# 2. 确认后生成规范文档
/ui-design-workflow spec

# 3. 日常开发
/ui-design-workflow implement 实现用户登录页面

# 4. PR 前检查
/ui-design-workflow check src/pages/Login.tsx
```

### 已有规范的老项目

```bash
# 基于现有规范生成 Demo
/ui-design-workflow demo --from-spec

# 然后正常使用
/ui-design-workflow implement 实现新功能
```

## 命令速查

| 命令 | 用途 | 触发场景 |
|------|------| ---------|
| `demo` | 生成 UI 展示页面 | 项目初期确定风格 |
| `spec` | 生成规范文档 | Demo 确认后 |
| `implement` | 按规范实现功能 | 日常开发 |
| `check` | 检查规范遵守 | PR 前检查 |
| `iterate` | 迭代更新规范 | 发现规范缺失 |

## 技术栈支持

**默认**：React + TypeScript + Tailwind CSS

**支持**：
- Vue 3 + Composition API
- Svelte
- CSS Modules
- UnoCSS
- 纯 HTML + CSS

在 `demo` 命令中指定技术栈：
```bash
/ui-design-workflow demo 使用 Vue 3 + UnoCSS 设计后台管理系统
```

## 自动触发

当你在对话中提到以下关键词时，Claude 会自动加载此 skill：

- 中文：实现页面、开发UI、写组件、前端开发、样式、界面
- 英文：designing UI、implement page、create component
- 组件名：button、form、modal、toast、card、input

## 文件结构

```
ui-design-workflow/
├── plugin.json                          # 插件配置
├── README.md                            # 本文件
├── LICENSE                              # MIT 协议
└── skills/
    └── ui-design-workflow/
        ├── SKILL.md                     # 主 Skill 文件
        ├── README.md                    # 详细使用说明
        ├── templates/
        │   ├── website.md               # 官网模板
        │   ├── components.md            # 组件库模板
        │   ├── spec-template.md         # 规范文档模板
        │   └── design-principles.md     # 设计原则
        └── references/
            └── modes.md                 # 各模式详细说明
```

## 完整工作流

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

## 贡献

欢迎提交 Issue 和 Pull Request！

## 协议

MIT License
