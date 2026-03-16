# Style Preview Page Template

Generate a standalone HTML file (`style-preview.html` in project root) that lets users visually compare 3 style directions in their browser before committing to a design.

> **Why**: Text descriptions like "Editorial luxury" are too abstract. Users need to SEE fonts, colors, and layout rendered in real to make informed decisions.

## File Requirements

- **Pure static HTML** — no framework dependency, served by a lightweight Node.js server
- **Inline CSS** — everything in one file
- **Google Fonts CDN** — load the actual fonts so users see real typography
- **Responsive** — 3 columns on desktop, stack vertically on mobile
- **Temporary file** — deleted after user confirms a style direction (already in .gitignore)
- **Agent communication** — user clicks "Confirm Selection" → POST to local server → agent auto-detects

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
      cursor: pointer;
      transition: border-color 0.2s, box-shadow 0.2s, transform 0.2s;
    }
    .preview-card:hover {
      border-color: #555;
      transform: translateY(-2px);
    }
    .preview-card.selected {
      border-color: #fff;
      box-shadow: 0 0 0 1px #fff, 0 8px 32px rgba(255,255,255,0.1);
    }
    .preview-card.selected .card-label .letter {
      background: #22c55e;
      color: #fff;
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

    /* Selection status bar (sticky bottom) */
    .status-bar {
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      background: #111;
      border-top: 1px solid #333;
      padding: 1rem 2rem;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 1rem;
      z-index: 100;
      transition: background 0.2s;
    }
    .status-bar.has-selection {
      background: #0a1a0a;
      border-top-color: #22c55e;
    }
    .status-text {
      color: #888;
      font-size: 0.9rem;
    }
    .status-bar.has-selection .status-text {
      color: #fafafa;
    }
    .status-selection {
      color: #22c55e;
      font-weight: 700;
      font-size: 1.1rem;
    }
    .copy-btn {
      display: none;
      padding: 0.5rem 1.25rem;
      background: #22c55e;
      color: #000;
      border: none;
      border-radius: 6px;
      font-weight: 600;
      font-size: 0.875rem;
      cursor: pointer;
      transition: background 0.15s;
    }
    .copy-btn:hover { background: #16a34a; }
    .copy-btn.copied {
      background: #666;
      color: #fff;
    }
    .status-bar.has-selection .copy-btn { display: inline-block; }

    /* Footer instructions */
    .instructions {
      text-align: center;
      margin-top: 3rem;
      margin-bottom: 5rem; /* space for sticky status bar */
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
    <p><strong>Click a card above to select, then tell your agent:</strong></p>
    <p style="margin-top: 0.5rem;">
      Reply <strong>A</strong>, <strong>B</strong>, or <strong>C</strong> &nbsp;|&nbsp;
      Say <strong>"new batch"</strong> to regenerate 3 new options &nbsp;|&nbsp;
      Or <strong>describe</strong> your own style direction
    </p>
  </div>

  <!-- Sticky status bar at bottom -->
  <div class="status-bar" id="statusBar">
    <span class="status-text" id="statusText">Click a style card to select</span>
    <button class="copy-btn" id="confirmBtn">Confirm Selection</button>
  </div>

  <script>
    // Card selection interaction
    const cards = document.querySelectorAll('.preview-card');
    const statusBar = document.getElementById('statusBar');
    const statusText = document.getElementById('statusText');
    const confirmBtn = document.getElementById('confirmBtn');
    let selected = null;
    let selectedName = '';

    cards.forEach(card => {
      card.addEventListener('click', () => {
        cards.forEach(c => c.classList.remove('selected'));
        card.classList.add('selected');
        selected = card.getAttribute('data-option');
        selectedName = card.querySelector('.name').textContent;
        statusBar.classList.add('has-selection');
        confirmBtn.textContent = 'Confirm Selection';
        confirmBtn.classList.remove('copied');
        statusText.innerHTML =
          'Selected: <span class="status-selection">' + selected + ' — ' + selectedName + '</span>';
      });
    });

    // Confirm selection — POST to local server, agent picks it up automatically
    confirmBtn.addEventListener('click', async () => {
      if (!selected) return;
      confirmBtn.textContent = 'Sending...';
      try {
        const res = await fetch('/choose', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ choice: selected, name: selectedName })
        });
        if (res.ok) {
          confirmBtn.textContent = '✓ Agent notified!';
          confirmBtn.classList.add('copied');
          statusText.innerHTML =
            '<span class="status-selection">✓ ' + selected + ' — ' + selectedName + '</span>' +
            ' &nbsp;·&nbsp; Your agent is continuing...';
        }
      } catch (e) {
        confirmBtn.textContent = 'Error — tell agent: "' + selected + '"';
        confirmBtn.classList.add('copied');
      }
    });
  </script>

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

## Local Server for Agent Communication

The agent starts a lightweight Node.js server that serves the preview page and receives the user's selection via POST.

### Server Script

The agent runs this inline (no external file needed):

```bash
node -e "
const http = require('http');
const fs = require('fs');
const path = require('path');
const PORT = 19836;
const ROOT = process.cwd();

http.createServer((req, res) => {
  // Serve the preview page
  if (req.method === 'GET' && (req.url === '/' || req.url === '/index.html')) {
    const html = fs.readFileSync(path.join(ROOT, 'style-preview.html'), 'utf8');
    res.writeHead(200, { 'Content-Type': 'text/html; charset=utf-8' });
    res.end(html);
    return;
  }

  // Receive the user's choice
  if (req.method === 'POST' && req.url === '/choose') {
    let body = '';
    req.on('data', chunk => body += chunk);
    req.on('end', () => {
      fs.writeFileSync(path.join(ROOT, '.style-choice'), body);
      res.writeHead(200, { 'Content-Type': 'application/json' });
      res.end(JSON.stringify({ status: 'ok' }));
    });
    return;
  }

  res.writeHead(404);
  res.end('Not found');
}).listen(PORT, () => {
  console.log('Style preview server running at http://localhost:' + PORT);
});
"
```

### Agent Flow

```
1. Agent generates `style-preview.html` with 3 options
2. Agent starts the local server in background (port 19836)
3. Agent tells user: "Open http://localhost:19836 to preview and select a style"
4. Agent polls for `.style-choice` file (check every 2 seconds)
5. When `.style-choice` appears:
   - Read the choice: {"choice": "B", "name": "Editorial"}
   - Kill the server process
   - Delete `style-preview.html` and `.style-choice`
   - Proceed with the selected direction
6. If user says "new batch" / "换一批" in chat instead:
   - Regenerate `style-preview.html` with 3 new options
   - Tell user to refresh the browser
7. If user describes a custom direction in chat:
   - Kill the server, delete temp files
   - Proceed with the described direction
```

### Important Notes

- Port `19836` is used to avoid conflicts with common dev server ports (3000, 5173, 8080, etc.)
- The server MUST be killed after the user confirms (or after timeout)
- Both `style-preview.html` and `.style-choice` MUST be deleted after use
- If the server fails to start (port in use), fall back to asking the user to open `style-preview.html` directly and reply with their choice in chat

## Theme Mode Question

After the user picks a style, ask about theme mode separately (this is a functional choice, not a visual one):
- Single theme (light)
- Single theme (dark)
- Light + Dark toggle

This can be asked via text or interactive UI — it doesn't need a visual preview.
