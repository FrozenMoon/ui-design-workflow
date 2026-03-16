# Style Preview Page Template

Generate a standalone HTML file (`style-preview.html` in project root) that lets users visually compare 3 style directions in their browser before committing to a design.

> **Why**: Text descriptions like "Editorial luxury" are too abstract. Users need to SEE fonts, colors, and layout rendered in real to make informed decisions.

## File Requirements

- **Pure static HTML** — no framework dependency, user opens the file directly in browser
- **Inline CSS** — everything in one file
- **Google Fonts CDN** — load the actual fonts so users see real typography
- **Responsive** — 3 columns on desktop, stack vertically on mobile
- **Temporary file** — deleted after user confirms a style direction (already in .gitignore)
- **No server needed** — user views the page, then tells their agent the choice in chat

## Page Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Style Preview — [Project Name]</title>

  <!-- Load all fonts used across the 3 options via Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=[Font1]&family=[Font2]&...&display=swap" rel="stylesheet">

  <style>
    /* Reset + base */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: system-ui, sans-serif;
      background: #0a0a0a;
      color: #fafafa;
      padding: 2rem;
    }

    /* Page header */
    .page-header {
      text-align: center;
      margin-bottom: 3rem;
    }
    .page-header h1 { font-size: 1.5rem; font-weight: 300; letter-spacing: 0.1em; }
    .page-header p { color: #888; margin-top: 0.5rem; }

    /* Preview grid */
    .preview-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 2rem;
      max-width: 1400px;
      margin: 0 auto;
    }
    @media (max-width: 1024px) {
      .preview-grid { grid-template-columns: 1fr; max-width: 600px; }
    }

    /* Each preview card */
    .preview-card {
      border: 2px solid #333;
      border-radius: 12px;
      overflow: hidden;
      background: #111;
      transition: border-color 0.2s, transform 0.2s;
    }
    .preview-card:hover {
      border-color: #555;
      transform: translateY(-2px);
    }

    /* Card header (option label) */
    .card-label {
      padding: 1rem 1.5rem;
      border-bottom: 1px solid #222;
      display: flex;
      align-items: center;
      gap: 0.75rem;
    }
    .card-label .letter {
      width: 2rem; height: 2rem;
      border-radius: 50%;
      background: #fff;
      color: #000;
      display: flex; align-items: center; justify-content: center;
      font-weight: 700;
      font-size: 0.875rem;
    }
    .card-label .name { font-weight: 600; }
    .card-label .desc { color: #888; font-size: 0.875rem; }

    /* Mini hero preview area */
    .hero-preview {
      /* Each option sets its own background, fonts, colors inline */
      padding: 3rem 2rem;
      min-height: 280px;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    /* Color palette strip */
    .color-strip {
      display: flex;
      height: 3rem;
    }
    .color-strip div {
      flex: 1;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.625rem;
      font-family: monospace;
      color: rgba(255,255,255,0.7);
    }

    /* Font info */
    .font-info {
      padding: 1rem 1.5rem;
      border-top: 1px solid #222;
      font-size: 0.75rem;
      color: #888;
    }
    .font-info span { color: #ccc; }

    /* Footer instructions */
    .instructions {
      text-align: center;
      margin-top: 3rem;
      margin-bottom: 2rem;
      padding: 2rem;
      border: 1px dashed #333;
      border-radius: 8px;
      color: #888;
    }
    .instructions strong { color: #fafafa; }
  </style>
</head>
<body>

  <div class="page-header">
    <h1>STYLE PREVIEW</h1>
    <p>[Project Name] — choose your aesthetic direction</p>
  </div>

  <div class="preview-grid">

    <!-- Option A -->
    <div class="preview-card" data-option="A">
      <div class="card-label">
        <div class="letter">A</div>
        <div>
          <div class="name">[Style A Name]</div>
          <div class="desc">[One-sentence vibe description]</div>
        </div>
      </div>
      <div class="hero-preview" style="
        background: [background color/gradient];
        font-family: '[Heading Font A]', serif;
      ">
        <h2 style="font-size: 2rem; margin-bottom: 0.5rem; color: [heading color];">
          [Sample headline using this style]
        </h2>
        <p style="font-family: '[Body Font A]', sans-serif; color: [body color]; margin-bottom: 1.5rem;">
          [One line of body text showing the font pairing]
        </p>
        <div>
          <span style="
            display: inline-block;
            padding: 0.75rem 2rem;
            background: [CTA color];
            color: [CTA text color];
            border-radius: [border-radius for this style];
            font-family: '[Body Font A]', sans-serif;
            font-weight: 600;
          ">Get Started</span>
        </div>
      </div>
      <div class="color-strip">
        <div style="background: [primary color]">[primary]</div>
        <div style="background: [accent color]">[accent]</div>
        <div style="background: [background color]">[bg]</div>
        <div style="background: [text color]">[text]</div>
      </div>
      <div class="font-info">
        Heading: <span>[Heading Font A]</span> &nbsp;|&nbsp; Body: <span>[Body Font A]</span> &nbsp;|&nbsp; Radius: <span>[value]</span>
      </div>
    </div>

    <!-- Option B — same structure, different style -->
    <!-- Option C — same structure, different style -->

  </div>

  <div class="instructions">
    <p><strong>Tell your agent which style you prefer:</strong></p>
    <p style="margin-top: 0.5rem;">
      Reply <strong>A</strong>, <strong>B</strong>, or <strong>C</strong> &nbsp;|&nbsp;
      Say <strong>"new batch"</strong> to regenerate 3 new options &nbsp;|&nbsp;
      Or <strong>describe</strong> your own style direction
    </p>
  </div>

</body>
</html>
```

## What Each Preview Card Must Show

Each card renders a **real visual preview**, not just text descriptions:

| Element | What to render | How |
|---------|---------------|-----|
| **Typography** | Actual fonts from Google Fonts | `<link>` to Google Fonts CDN, apply via `font-family` |
| **Color palette** | 4 color blocks (primary, accent, background, text) | Colored `<div>` strip at bottom of card |
| **Mini Hero** | Headline + body text + CTA button | Rendered in the actual fonts and colors of this style |
| **Atmosphere** | Background treatment (gradient, texture, etc.) | Applied as CSS background on the hero area |
| **Border radius** | Shown on the CTA button and card edges | Applied via `border-radius` |
| **Font info** | Font names + border-radius value | Text line below the color strip |

## Rules for Generating Options

1. **3 diverse directions** — don't offer 3 variants of the same style. E.g., not "Minimal A / Minimal B / Minimal C" but "Editorial / Brutalist / Luxury"
2. **Real Google Fonts** — pick actual fonts from Google Fonts that match the style. NEVER use Inter, Roboto, Arial, or Helvetica as primary heading fonts.
3. **Coherent palettes** — each option's colors, fonts, and atmosphere must feel like a unified direction, not random
4. **Context-aware** — options should make sense for the project type (e.g., don't suggest "playful toy-like" for a B2B analytics dashboard)
5. **Sample text** — use the actual project name/product in the hero preview headline if available

## Agent Flow

```
1. Agent generates `style-preview.html` with 3 options in the project root
2. Agent tells user to open the file in their browser:
   "Open style-preview.html in your browser to compare the 3 style options,
    then tell me: A, B, or C / 'new batch' for 3 new options / describe your own direction"
3. User replies in chat with their choice
4. Agent handles the response:
   - "A" / "B" / "C" → Proceed with that style direction
   - "new batch" / "换一批" → Regenerate style-preview.html with 3 new options, tell user to refresh
   - User describes a custom direction → Proceed with that direction
5. After style is confirmed, delete style-preview.html
```

## Theme Mode Question

After the user picks a style, ask about theme mode separately (this is a functional choice, not a visual one):
- Single theme (light)
- Single theme (dark)
- Light + Dark toggle

This can be asked via text or interactive UI — it doesn't need a visual preview.
