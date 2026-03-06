# Website Template Structure

Template structure for Demo mode Tab 1 (Final Preview).

## Page Structure

```
1. Navigation (Navbar)
   - Logo + Product name
   - Navigation links
   - CTA button (optional)

2. Hero Section
   - Main heading: Product name + core value proposition
   - Subheading: One-line description of what the product is
   - CTA button
   - Optional: Product screenshot or demo animation placeholder

3. Why Needed Section
   - Compare traditional approach vs. this product
   - Side-by-side comparison cards

4. Features Section (Core Features)
   - Alternating left-right layout (text + illustration)
   - 3-4 features, each including:
     - Title
     - Description
     - Accompanying image/animation on the opposite side

5. Use Cases Section
   - 3-4 use case cards
   - Each: Icon + Title + Brief description

6. CTA Section (Call to Action)
   - Heading: Encourage users to take action
   - CTA button

7. Footer
   - Multi-column link layout
   - Copyright information
```

## Content Strategy

Adjust the copy style based on project type:

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
- Maintain clear visual hierarchy; avoid information overload
