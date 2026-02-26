# [项目名称] UI 设计规范

> **版本**: 1.0
> **状态**: 正式生效
> **最后更新**: [当前日期]

本文档定义了 [项目名称] 的视觉与交互标准，所有 UI 相关开发必须遵守本规范。

---

## 1. 设计理念 (Design Philosophy)

[从 Demo 中提取的核心设计语言]

### 核心关键词
- **[关键词1]**: [说明]
- **[关键词2]**: [说明]
- **[关键词3]**: [说明]

### 设计目标
- [目标1：例如：提供简洁直观的用户体验]
- [目标2：例如：保持视觉一致性和品牌识别度]
- [目标3：例如：确保可访问性和包容性设计]

---

## 2. 颜色系统 (Color System)

### 2.1 核心色板

| 角色 | 变量名 | 色值 / CSS 类 | 说明 |
| :--- | :--- | :--- | :--- |
| **Primary** | `primary` | `#000000` / `bg-primary` | 主要行动点（按钮、链接） |
| **Secondary** | `secondary` | `#666666` / `bg-secondary` | 次要行动点 |
| **Background** | `background` | `#FFFFFF` / `bg-background` | 全局背景色 |
| **Card** | `card` | `#FAFAFA` / `bg-card` | 卡片/容器背景 |

### 2.2 文本颜色

| 角色 | 变量名 | 色值 / CSS 类 | 说明 |
| :--- | :--- | :--- | :--- |
| **Heading** | `foreground` | `#000000` / `text-foreground` | 标题、重要文本 |
| **Body** | `text-body` | `#333333` / `text-body` | 正文内容 |
| **Muted** | `muted-foreground` | `#999999` / `text-muted-foreground` | 辅助信息、次要文本 |
| **Disabled** | `text-disabled` | `#CCCCCC` / `text-disabled` | 禁用状态文本 |

### 2.3 功能色 (Functional Colors)

保持克制，仅在状态反馈中使用。

| 角色 | 色值 / CSS 类 | 说明 |
| :--- | :--- | :--- |
| **Success** | `#10B981` / `text-green-600` | 成功状态、确认操作 |
| **Error** | `#EF4444` / `text-red-600` | 错误状态、破坏性操作 |
| **Warning** | `#F59E0B` / `text-amber-600` | 警告状态、需注意的信息 |
| **Info** | `#3B82F6` / `text-blue-600` | 提示信息、普通通知 |

### 2.4 颜色使用原则

- ✅ **优先使用**核心色板中的颜色
- ✅ 使用功能色时保持一致性（成功=绿色，错误=红色）
- ❌ **禁止**在核心 UI 中使用彩色（除非是功能色）
- ❌ **禁止**使用超过 3 种主色

---

## 3. 字体与排版 (Typography)

### 3.1 字体家族

**标题字体**：
- 西文：[字体名称，例如：Inter, -apple-system, system-ui]
- 中文：[字体名称，例如：PingFang SC, Microsoft YaHei, 微软雅黑]
- Font Stack: `[完整 font-family 定义]`

**正文字体**：
- 西文：[字体名称]
- 中文：[字体名称]
- Font Stack: `[完整 font-family 定义]`

### 3.2 排版层级表

| 层级 | 字体风格 | CSS 类名 | 字号/行高 | 字重 | 场景 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Display** | Sans-serif | `text-4xl lg:text-6xl` | 48-60px / 1.1 | 700 | 落地页 Slogan |
| **H1** | Sans-serif | `text-3xl` | 30px / 1.2 | 600 | 页面主标题 |
| **H2** | Sans-serif | `text-2xl` | 24px / 1.3 | 600 | 模块标题 |
| **H3** | Sans-serif | `text-xl` | 20px / 1.4 | 600 | 卡片标题 |
| **Body** | Sans-serif | `text-base` | 16px / 1.5 | 400 | 默认正文 |
| **Small** | Sans-serif | `text-sm` | 14px / 1.5 | 400 | 按钮、输入框、二级信息 |
| **Caption** | Sans-serif | `text-xs` | 12px / 1.5 | 400 | 标签、Badge、辅助说明 |

### 3.3 字重标准

| 字重名称 | 数值 | 使用场景 |
| :--- | :--- | :--- |
| Regular | 400 | 正文、描述 |
| Medium | 500 | 强调文本 |
| Semibold | 600 | 标题、按钮 |
| Bold | 700 | 特别强调 |

### 3.4 排版原则

- ✅ 标题使用较粗字重（600+）
- ✅ 正文使用 Regular（400）
- ✅ 行高至少 1.5（可读性）
- ❌ 避免使用超过 3 种字重
- ❌ 避免全大写文本（UPPERCASE），可读性差

---

## 4. 间距与圆角 (Spacing & Radius)

### 4.1 间距体系 (Spacing Scale)

基于 **[4px / 8px] 栅格系统**。

| Token | 值 | Tailwind 类 | 使用场景 |
| :--- | :--- | :--- | :--- |
| **XS** | 4px | `p-1`, `m-1`, `gap-1` | 图标与文字间距 |
| **S** | 8px | `p-2`, `m-2`, `gap-2` | 小组件内间距 |
| **M** | 16px | `p-4`, `m-4`, `gap-4` | 标准组件内间距 |
| **L** | 24px | `p-6`, `m-6`, `gap-6` | 卡片内间距 |
| **XL** | 32px | `p-8`, `m-8`, `gap-8` | 模块间间距 |
| **XXL** | 48px | `p-12`, `m-12`, `gap-12` | 大模块间间距 |

### 4.2 圆角规范 (Border Radius)

| Token | 值 | Tailwind 类 | 使用场景 |
| :--- | :--- | :--- | :--- |
| **Small** | 4px | `rounded` | Badge, Tag |
| **Medium** | 8px | `rounded-lg` | Button, Input |
| **Large** | 12px | `rounded-xl` | Card（小） |
| **XLarge** | 16px | `rounded-2xl` | Card（中） |
| **XXLarge** | 24px | `rounded-3xl` | Card（大）, Modal |
| **Full** | 9999px | `rounded-full` | Pill 按钮, Avatar |

### 4.3 间距和圆角原则

- ✅ 所有间距值应符合栅格系统（[4/8]px 的倍数）
- ✅ 相关元素间距小，不相关元素间距大
- ✅ 保持圆角一致性（同类组件使用相同圆角）
- ❌ 避免使用奇数间距（如 7px, 13px）
- ❌ 避免圆角过小（< 4px），视觉不明显

---

## 5. 阴影与动效 (Shadows & Animations)

### 5.1 阴影系统

| 层级 | Tailwind 类 | Box Shadow 值 | 使用场景 |
| :--- | :--- | :--- | :--- |
| **None** | `shadow-none` | `none` | 无需层级分离 |
| **Small** | `shadow-sm` | `0 1px 2px rgba(0,0,0,0.05)` | 轻微层级 |
| **Medium** | `shadow` | `0 4px 6px rgba(0,0,0,0.1)` | 卡片、按钮 |
| **Large** | `shadow-lg` | `0 10px 15px rgba(0,0,0,0.1)` | Dropdown, Popover |
| **XLarge** | `shadow-xl` | `0 20px 25px rgba(0,0,0,0.1)` | Modal, 大卡片 |

### 5.2 动效标准

**Transition 配置**：
```css
transition: all 0.2s ease-out; /* 默认 */
transition: all 0.3s ease-out; /* 较慢，适用于大型元素 */
```

**常用动效**：
- **Hover Lift**：`hover:-translate-y-0.5 hover:shadow-lg`
- **Click Scale**：`active:scale-95`
- **Fade In**：`transition-opacity duration-200`

### 5.3 动效原则

- ✅ 所有交互元素应有过渡效果
- ✅ 时长控制在 150-300ms
- ✅ 使用 `ease-out` 或 `ease-in-out`
- ❌ 避免过长的动画（> 500ms）
- ❌ 避免生硬的瞬间变化（无 transition）

---

## 6. 组件规范 (Components)

### 6.1 按钮 (Button)

**风格变体**：

| 变体 | 样式类名 | 使用场景 |
| :--- | :--- | :--- |
| **Primary** | `bg-primary text-primary-foreground` | 主要行动点 |
| **Secondary** | `bg-secondary text-secondary-foreground` | 次要行动点 |
| **Ghost** | `bg-transparent text-foreground hover:bg-secondary` | 轻量操作 |
| **Outline** | `border border-primary text-primary bg-transparent` | 取消操作 |

**尺寸变体**：

| 尺寸 | 类名 | Padding | 字号 |
| :--- | :--- | :--- | :--- |
| **Small** | `btn-sm` | `px-3 py-1.5` | `text-sm` |
| **Medium** | `btn` | `px-4 py-2` | `text-base` |
| **Large** | `btn-lg` | `px-6 py-3` | `text-lg` |

**状态**：
- Normal: 默认样式
- Hover: 背景色加深 10%, 轻微上浮
- Active: 背景色加深 20%, 轻微缩小
- Disabled: `opacity-50 cursor-not-allowed`

**代码示例**：
```tsx
<button className="bg-primary text-white px-4 py-2 rounded-lg hover:-translate-y-0.5 hover:shadow-lg transition-all active:scale-95">
  Primary Button
</button>
```

---

### 6.2 表单组件 (Form Controls)

#### Input（输入框）

**基础样式**：
```tsx
className="bg-white border border-gray-300 rounded-lg px-4 py-2 text-base focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all"
```

**状态**：
- Normal: `border-gray-300`
- Focus: `ring-2 ring-primary`
- Error: `border-red-500 ring-2 ring-red-500`
- Disabled: `bg-gray-100 text-gray-400 cursor-not-allowed`

#### Select（下拉选择）

与 Input 保持一致的样式，右侧添加箭头图标。

#### Checkbox / Radio

**样式**：
- 尺寸：16x16px 或 20x20px
- 圆角：Checkbox 使用 `rounded`, Radio 使用 `rounded-full`
- 选中态：背景色使用 `primary`
- Focus 态：外围 ring

---

### 6.3 反馈组件 (Feedback)

#### Toast（轻提示）

**位置**：右上角或顶部居中

**样式**：
```tsx
className="bg-white rounded-lg shadow-lg px-4 py-3 border-l-4 border-[功能色]"
```

**类型**：
- Success: 左边框绿色
- Error: 左边框红色
- Warning: 左边框黄色
- Info: 左边框蓝色

**动画**：从右侧滑入，停留 3-5 秒后淡出

#### Alert（警告提示）

**样式**：
```tsx
className="bg-[功能色]-50 border border-[功能色]-200 rounded-lg px-4 py-3 text-[功能色]-800"
```

#### Modal（模态框）

**遮罩**：`bg-black/50 backdrop-blur-sm`
**容器**：`bg-white rounded-2xl shadow-2xl p-6`
**动画**：淡入 + 缩放（从 0.95 到 1）

---

### 6.4 卡片 (Card)

**基础样式**：
```tsx
className="bg-white rounded-2xl shadow p-6"
```

**Hover 效果**：
```tsx
className="hover:-translate-y-1 hover:shadow-lg transition-all duration-300"
```

**变体**：
- 无边框阴影：`shadow`
- 带边框：`border border-gray-200`
- 扁平：`bg-gray-50`（无阴影）

---

### 6.5 导航组件 (Navigation)

#### Tabs（标签页）

**容器**：`border-b border-gray-200`
**Tab**：
- 未激活：`text-gray-600 hover:text-gray-900`
- 激活：`text-primary border-b-2 border-primary`

#### Breadcrumb（面包屑）

**样式**：`text-sm text-gray-600`
**分隔符**：`/` 或 `>` 或箭头图标
**当前页**：`text-foreground font-medium`

#### Pagination（分页）

**样式**：
- 按钮：与 Secondary Button 一致
- 当前页：使用 Primary Button 样式

---

### 6.6 其他组件

#### 自定义滚动条

```css
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}
```

#### Loading（加载中）

**Spinner**：
- 尺寸：16px（小）, 24px（中）, 32px（大）
- 颜色：`primary`
- 动画：旋转，1s linear infinite

**Skeleton（骨架屏）**：
- 背景：`bg-gray-200`
- 动画：从左到右的渐变扫过效果

#### Progress Bar（进度条）

- 背景：`bg-gray-200 rounded-full`
- 进度条：`bg-primary rounded-full`
- 高度：4-8px

---

## 7. 禁用清单 (Don'ts)

以下是应该**避免**的做法：

### 颜色
- ❌ 使用过多颜色（超过 3 种主色）
- ❌ 颜色对比度不足（文本与背景对比度 < 4.5:1）
- ❌ 在非功能性场景使用功能色（如用红色做装饰）

### 排版
- ❌ 字号过小（< 12px）
- ❌ 行高过小（< 1.2）
- ❌ 使用超过 4 种字重
- ❌ 全大写文本（降低可读性）

### 间距
- ❌ 使用不符合栅格的间距值（如 7px, 13px）
- ❌ 间距过小，元素拥挤
- ❌ 间距不一致（相同层级的元素间距不同）

### 圆角
- ❌ 圆角过小（< 4px）
- ❌ 同类组件圆角不一致
- ❌ 混用方角和圆角（保持统一风格）

### 动效
- ❌ 动画时长过长（> 500ms）
- ❌ 没有过渡效果（生硬跳变）
- ❌ 过度使用动画（影响性能）

### 其他
- ❌ 点击区域过小（< 32x32px）
- ❌ 缺少焦点状态
- ❌ 缺少 Hover 反馈

---

## 8. 代码示例 (Code Examples)

### 完整的按钮组件示例

```tsx
// Primary Button
<button className="bg-primary text-white px-4 py-2 rounded-lg font-medium hover:-translate-y-0.5 hover:shadow-lg active:scale-95 transition-all duration-200">
  Primary Button
</button>

// Secondary Button
<button className="bg-gray-100 text-gray-900 px-4 py-2 rounded-lg font-medium hover:bg-gray-200 active:scale-95 transition-all duration-200">
  Secondary Button
</button>

// Ghost Button
<button className="bg-transparent text-gray-700 px-4 py-2 rounded-lg font-medium hover:bg-gray-100 active:scale-95 transition-all duration-200">
  Ghost Button
</button>
```

### 完整的卡片组件示例

```tsx
<div className="bg-white rounded-2xl shadow p-6 hover:-translate-y-1 hover:shadow-lg transition-all duration-300">
  <h3 className="text-xl font-semibold text-foreground mb-2">
    Card Title
  </h3>
  <p className="text-sm text-body mb-4">
    Card description goes here.
  </p>
  <button className="bg-primary text-white px-4 py-2 rounded-lg text-sm font-medium hover:shadow-lg transition-all">
    Action
  </button>
</div>
```

### 完整的表单示例

```tsx
<form className="space-y-4">
  <div>
    <label className="block text-sm font-medium text-foreground mb-1">
      Email
    </label>
    <input
      type="email"
      className="w-full bg-white border border-gray-300 rounded-lg px-4 py-2 text-base focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all"
      placeholder="your@email.com"
    />
  </div>

  <div>
    <label className="block text-sm font-medium text-foreground mb-1">
      Password
    </label>
    <input
      type="password"
      className="w-full bg-white border border-gray-300 rounded-lg px-4 py-2 text-base focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all"
      placeholder="••••••••"
    />
  </div>

  <button type="submit" className="w-full bg-primary text-white px-4 py-3 rounded-lg font-medium hover:shadow-lg transition-all">
    Sign In
  </button>
</form>
```

---

## 9. 响应式适配 (Responsive Design)

### 断点定义

| 断点 | 屏幕宽度 | 设备类型 |
| :--- | :--- | :--- |
| `sm` | ≥ 640px | 大手机 |
| `md` | ≥ 768px | 平板 |
| `lg` | ≥ 1024px | 笔记本 |
| `xl` | ≥ 1280px | 桌面 |
| `2xl` | ≥ 1536px | 大屏 |

### 响应式规则

- 移动端优先（Mobile First）
- 使用 Tailwind 的响应式前缀（如 `md:text-lg`）
- 关键断点：`md`（768px）和 `lg`（1024px）

---

## 10. 可访问性 (Accessibility)

### 必须遵守的规则

- ✅ 文本与背景对比度 ≥ 4.5:1
- ✅ 所有交互元素有明显的焦点状态
- ✅ 点击区域 ≥ 44x44px（移动端）或 ≥ 32x32px（桌面端）
- ✅ 使用语义化 HTML（button, input, nav, header, main）
- ✅ 图片添加 alt 属性
- ✅ 表单输入添加 label
- ✅ 支持键盘导航

---

## 11. 更新日志 (Changelog)

### v1.0 (当前日期)
- 初始版本
- 基于 UI Demo 提取并生成规范
- 定义了颜色、排版、间距、圆角、组件等完整规范

---

**规范维护**：
- 定期审查和更新（建议每季度一次）
- 新增组件或样式需更新本文档
- 使用 `/ui-design-workflow iterate` 进行规范迭代
