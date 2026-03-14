# Website Template Structure

Template structure for Demo mode Tab 1 (Final Preview).

> **Before using this template**: Read [references/frontend-aesthetics.md](../references/frontend-aesthetics.md). This template defines the *content sections* — the **visual execution** must follow the aesthetics guide. Do NOT produce a generic page with centered containers and equal columns.

## Page Sections

The following sections are the building blocks. **Arrange, combine, and style them creatively** based on the chosen aesthetic direction.

```
1. Navigation (Navbar)
   - Logo + Product name
   - Navigation links
   - CTA button (optional)
   - Consider: sticky, transparent, minimal, or unconventional placements

2. Hero Section
   - Main heading: Product name + core value proposition
   - Subheading: One-line description
   - CTA button
   - Optional: Product screenshot, demo animation, or atmospheric visual
   - LAYOUT IDEAS: asymmetric split, full-bleed background, overlapping elements,
     diagonal composition, dramatic whitespace, text as visual element

3. Why Needed Section (optional)
   - Compare traditional approach vs. this product
   - Side-by-side or before/after presentation
   - Can be replaced with a metrics/stats section for variety

4. Features Section (Core Features)
   - 3-4 features, each with title + description + visual
   - LAYOUT IDEAS: bento grid, staggered cards, scrolling showcase,
     overlapping image-text, tabbed display, timeline — NOT just alternating left-right

5. Use Cases / Testimonials Section
   - 3-4 use cases or testimonials
   - LAYOUT IDEAS: masonry grid, carousel, quote with large typography,
     full-width story blocks — NOT just identical cards in a row

6. CTA Section (Call to Action)
   - Heading: Encourage action
   - CTA button
   - Consider: atmospheric background, gradient, pattern, or unique visual treatment

7. Footer
   - Multi-column link layout
   - Copyright information
```

## Creative Execution Reminders

- **Typography**: Use the distinctive fonts chosen during design thinking. Headlines should be visually striking — consider oversized display text, varied weights, or decorative treatments.
- **Color**: Apply the dominant + accent palette. Background sections should vary — not all the same white or gray.
- **Motion**: Add orchestrated page load animations (staggered reveals). Scroll-triggered animations for sections entering viewport. Interesting hover states.
- **Backgrounds**: No plain solid backgrounds for every section. Use gradients, textures, patterns, or color shifts between sections to create visual rhythm.
- **Layout**: Vary density and spacing between sections. Not every section should have the same padding and centered layout.

## Content Strategy

Adjust copy style based on project type:

| Project Type | Copy Style |
|-------------|------------|
| B2B tool | Emphasize efficiency, professionalism, ROI |
| C2C application | Emphasize ease of use, experience, emotion |
| Developer tool | Emphasize technical details, easy integration |
| Content website | Emphasize content quality, reading experience |

## Example Code Structure

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

## Important Notes

- Hero heading should not exceed 10 words
- Each Feature description should not exceed 2 lines
- CTA button copy should be action-oriented ("Get Started" rather than "Learn More")
- **Run the anti-AI-slop checklist** from the aesthetics guide before finalizing
