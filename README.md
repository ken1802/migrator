# AI Migrator — Pipeline Dashboard

Interactive demo dashboard showing the AI Migrator pipeline for Niteco sales pitches. Visualizes the end-to-end process of migrating web pages into a CMS blueprint using Vision / Graph / DOM Enrichment / Migration phases.

## What's in this folder

```
ai-migrator-deploy/
├── index.html     # Single-file dashboard (HTML + CSS + JS inline)
├── vercel.json    # Vercel static-site config
└── README.md      # This file
```

Everything is self-contained in `index.html`. No build step, no dependencies, no backend.

## Deploy to Vercel

### Option 1 — Vercel CLI (fastest)

```bash
# Install CLI once
npm i -g vercel

# From inside this folder
cd ai-migrator-deploy
vercel

# Follow prompts. For production deploy:
vercel --prod
```

### Option 2 — Vercel dashboard (no CLI)

1. Zip this folder or push it to a GitHub repo
2. Go to https://vercel.com/new
3. Import the repo (or drag-drop the folder)
4. Framework preset: **Other** (it's plain static HTML)
5. Build command: leave empty
6. Output directory: leave empty (Vercel serves the root)
7. Click **Deploy**

That's it. Vercel will detect `index.html` and serve it as-is with the headers from `vercel.json`.

## Local preview

Just open `index.html` in a browser — it works offline. Or run a quick static server:

```bash
# Python 3
python3 -m http.server 8080

# Node (npx)
npx serve .
```

Then visit `http://localhost:8080`.

## Features

- **4 routing modes** based on Configuration toggles:
  - Live site only → Vision → DOM Enrichment → Migration
  - Live + Figma → adds Figma crawling to Vision phase
  - + Optimizely GraphID → swaps DOM Enrichment for Vision × Graph fast-path
- **Horizontal carousel** — one slide per active phase, auto-advances as pipeline runs
- **Extracted Blocks panel** — populated with 13 real blocks during Block Extraction step
- **System Output** — 2×2 grid showing Source / Blocks / Blueprint / Delivered as they complete
- **Floating toolbar** with Start/Stop/Reset and progress bar
- Full **WCAG AA compliance** on all text/background combinations
- `prefers-reduced-motion` respected — animations disabled for users who opt out

## Browser support

Tested target: recent Chrome, Safari, Firefox, Edge. Uses:
- CSS Grid / Flexbox
- CSS custom properties
- `backdrop-filter` (progressive enhancement — still renders without)
- Standard ES2020+ JS (no transpilation needed for evergreen browsers)

## Customization

All Niteco brand tokens live in `:root` at the top of the `<style>` block:

```css
--bg-primary: #262524;     /* Niteco Black */
--accent: #FFD400;         /* Niteco Yellow */
--font-heading: 'Gilroy', Arial, sans-serif;
```

Step data, timings, and block list are in `STEPS_ALL` + `BLOCKS` arrays near the top of the `<script>` block. Edit and redeploy.
