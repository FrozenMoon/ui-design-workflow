# 组件库模板

Demo 模式 Tab 2（组件库）的模板结构。

## 必须包含的组件区域

### 1. 颜色系统
- 主色调（Primary, Secondary, Background）
- 文本颜色层级（Heading, Body, Muted）
- 品牌强调色（Positive/Negative，用于业务对比）
- 系统反馈色（Success, Error, Warning, Info）

### 2. 排版系统
- Display / H1 / H2 / H3 / Body / Small / Caption
- 字重变体
- 行高示例

### 3. 按钮
- 风格：Primary, Secondary, Ghost, Outline
- 尺寸：Small, Medium, Large
- 状态：Normal, Hover, Active, Disabled
- 带图标变体

### 4. 表单组件
- Input（文本输入）
- Textarea（多行文本）
- Select（下拉选择）
- Checkbox（复选框）- 自定义样式
- Radio（单选框）- 自定义样式
- Switch（开关）
- 状态：Normal, Focus, Error, Disabled

### 5. 反馈组件
- Toast（轻提示）- Success, Error 变体
- Alert（警告提示）- Success, Error, Warning, Info
- Modal（模态框）

### 6. 卡片
- 基础卡片（边框）
- 阴影卡片
- 可交互卡片

### 7. 加载状态
- Spinner（加载圈）
- Skeleton（骨架屏）
- Progress Bar（进度条）

## 组件展示原则

每个组件应展示：
1. 所有变体（风格、尺寸）
2. 所有状态（正常、悬停、禁用等）
3. 可交互示例（如 Modal 的打开按钮）

## 代码结构示例

```tsx
<section className="component-section">
  <h2>3. 按钮</h2>

  <div className="subsection">
    <h3>风格变体</h3>
    <div className="examples">
      <button className="primary">Primary</button>
      <button className="secondary">Secondary</button>
      <button className="ghost">Ghost</button>
      <button className="outline">Outline</button>
    </div>
  </div>

  <div className="subsection">
    <h3>尺寸</h3>
    <div className="examples">
      <button className="small">Small</button>
      <button className="medium">Medium</button>
      <button className="large">Large</button>
    </div>
  </div>

  <div className="subsection">
    <h3>状态</h3>
    <div className="examples">
      <button>Normal</button>
      <button className="hover">Hover</button>
      <button disabled>Disabled</button>
    </div>
  </div>
</section>
```

## 自定义表单控件

Checkbox 和 Radio 应使用自定义样式，隐藏原生控件：

```tsx
// Checkbox 示例
<label className="flex items-center gap-3 cursor-pointer">
  <div className="relative w-5 h-5">
    <input type="checkbox" className="peer sr-only" />
    <div className="absolute inset-0 bg-zinc-100 rounded-lg
                    peer-checked:bg-zinc-900 transition-all" />
    <Check className="absolute inset-0 w-3.5 h-3.5 m-auto text-white
                      opacity-0 peer-checked:opacity-100" />
  </div>
  <span>选项文本</span>
</label>

// Radio 示例
<label className="flex items-center gap-3 cursor-pointer">
  <div className="relative w-5 h-5">
    <input type="radio" className="peer sr-only" />
    <div className="absolute inset-0 bg-zinc-100 rounded-full
                    peer-checked:bg-zinc-900 transition-all" />
    <div className="absolute inset-0 w-2 h-2 m-auto bg-white rounded-full
                    opacity-0 peer-checked:opacity-100" />
  </div>
  <span>选项文本</span>
</label>
```
