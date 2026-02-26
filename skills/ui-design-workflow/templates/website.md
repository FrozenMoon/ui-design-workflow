# 官网模板结构

Demo 模式 Tab 1（成品展示）的模板结构。

## 页面结构

```
1. Navigation（导航栏）
   - Logo + 产品名
   - 导航链接
   - CTA 按钮（可选）

2. Hero Section（英雄区）
   - 大标题：产品名 + 核心价值主张
   - 副标题：一句话说明产品是什么
   - CTA 按钮
   - 可选：产品截图或演示动画占位

3. Why Needed Section（为什么需要）
   - 对比传统方式 vs 本产品
   - 左右两列对比卡片

4. Features Section（核心特性）
   - 左右交替布局（文字 + 插图）
   - 3-4 个特性，每个包含：
     - 标题
     - 描述
     - 右侧配图/动画

5. Use Cases Section（使用场景）
   - 3-4 个场景卡片
   - 每个：图标 + 标题 + 简短描述

6. CTA Section（行动号召）
   - 标题：鼓励用户行动
   - CTA 按钮

7. Footer（页脚）
   - 多列链接布局
   - 版权信息
```

## 内容填充策略

根据项目类型调整文案风格：

| 项目类型 | 文案风格 |
|---------|---------|
| B2B 工具 | 强调效率、专业、ROI |
| C2C 应用 | 强调易用、体验、情感 |
| 开发者工具 | 强调技术细节、集成简单 |
| 内容网站 | 强调内容质量、阅读体验 |

## 示例代码结构

```tsx
export default function ProductDemo() {
  return (
    <>
      <Navigation />
      <HeroSection />
      <WhyNeededSection />
      <FeaturesSection />
      <UseCasesSection />
      <CTASection />
      <Footer />
    </>
  )
}
```

## 注意事项

- Hero 标题不超过 10 个字
- 每个 Feature 描述不超过 2 行
- CTA 按钮文案要有行动感（"立即开始"而非"了解更多"）
- 保持视觉层级清晰，避免信息过载
