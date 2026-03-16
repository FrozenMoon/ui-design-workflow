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

    /* Product preview area — the main visual showcase */
    .product-preview {
      /* Each option sets its own background, fonts, colors inline */
      padding: 2rem;
      min-height: 360px;
    }

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
    <div class="preview-card">
      <div class="card-label">
        <div class="letter">A</div>
        <div>
          <div class="name">[Style A Name]</div>
          <div class="desc">[One-sentence vibe description]</div>
        </div>
      </div>
      <div class="product-preview" style="
        background: [background color/gradient];
        font-family: '[Heading Font A]', serif;
      ">
        <!--
          Render a MINI VERSION of the user's actual product UI here.
          The content adapts to project type:

          Website → mini landing page (nav + hero headline + CTA + feature cards)
          Dashboard → mini app layout (sidebar + top bar + stat cards + table rows)
          E-commerce → mini product grid (product cards with prices + search bar)
          Blog → mini article list (featured post + article cards with titles)

          Use the real fonts, colors, border-radius, and atmosphere of this style.
          Show enough UI elements (buttons, cards, inputs, nav) to convey the feel.
          Use realistic placeholder content matching the product domain.
        -->
      </div>
    </div>

    <!-- Option B — same structure, different style + product preview -->
    <!-- Option C — same structure, different style + product preview -->

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

Each card renders a **mini version of the user's actual product**, not abstract design tokens:

| Element | What to show | How |
|---------|-------------|-----|
| **Product UI mockup** | A miniature of the real product interface | Adapt to project type (see below) |
| **Typography** | Actual fonts from Google Fonts applied to real UI elements | `<link>` to Google Fonts CDN, apply via `font-family` |
| **Color & atmosphere** | Background, text colors, accents visible through the UI | Applied naturally through the UI elements, not as separate swatches |
| **Components** | Buttons, cards, inputs, navigation rendered in this style | Show enough real UI pieces to convey the overall feel |
| **Border radius & spacing** | Visible on buttons, cards, inputs | Applied naturally — users see the shape language without labels |

**Do NOT show**: color hex codes, font name labels, border-radius values, or any other design parameters. Users should judge purely by visual impression.

### Product preview adapts to project type

| Project type | What to render in the preview |
|-------------|------------------------------|
| **Website / Landing Page** | Mini nav bar + hero headline + CTA button + 2-3 feature cards |
| **Web App / Dashboard** | Mini sidebar + top bar + stat cards + a few table rows |
| **E-commerce** | Mini search bar + product cards grid (image + price + button) |
| **Blog / Content** | Featured article hero + article list cards with titles + dates |
| **Portfolio** | Project thumbnail grid + project title overlays |

The preview should make the user think: *"This is roughly what my product will look like in style A vs B vs C."*

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
