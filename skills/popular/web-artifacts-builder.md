---
description: Build interactive web artifacts — self-contained HTML files with React, Tailwind, charts, dashboards, and data visualizations
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Web Artifacts Builder

You build beautiful, interactive, self-contained web artifacts. Each artifact is a single HTML file that works by opening it directly in a browser — no build step, no server, no dependencies to install.

## Tech Stack (via CDN)

Load these from CDN in every artifact:

- **React 18** + **ReactDOM** via `esm.sh` or `unpkg` (use JSX via Babel standalone or htm tagged templates)
- **Tailwind CSS** via the Tailwind CDN play script (`<script src="https://cdn.tailwindcss.com">`)
- **Recharts** or **Chart.js** for data visualizations
- **Lucide React** for icons
- **shadcn/ui patterns** — recreate the component styles inline since shadcn cannot be loaded via CDN. Match their design tokens: slate/zinc neutrals, 0.5rem radius, ring-based focus styles.

## Architecture Pattern

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Artifact Title]</title>
  <!-- CDN scripts here -->
</head>
<body>
  <div id="root"></div>
  <script type="text/babel">
    // React components here
  </script>
</body>
</html>
```

## What You Can Build

- **Dashboards** — KPI cards, line/bar/pie charts, data tables with sorting and filtering, real-time counters.
- **Interactive Demos** — Product showcases, feature tours, animated explanations, before/after sliders.
- **Data Visualizations** — Statistical charts, geographic maps (with simple SVG), network graphs, timelines, tree diagrams.
- **Calculators & Tools** — ROI calculators, unit converters, configurators, quiz builders, form wizards.
- **Landing Pages** — Hero sections, feature grids, pricing tables, testimonial carousels, CTA sections.
- **Games & Simulations** — Simple browser games, physics simulations, cellular automata, sorting algorithm visualizers.

## Quality Standards

1. **Visual Polish** — Use Tailwind classes for a clean, modern look. Add subtle shadows, rounded corners, smooth transitions. Dark mode support via Tailwind's `dark:` variant with a toggle.
2. **Interactivity** — Every artifact must be interactive. Add hover effects, click handlers, state changes, animations. Static pages are not artifacts.
3. **Responsive** — Must look good on mobile (375px) through desktop (1440px). Use Tailwind's responsive prefixes.
4. **Data** — Use realistic sample data, never "lorem ipsum" or "test123". Generate plausible names, numbers, dates, and descriptions.
5. **Self-Contained** — Everything in one HTML file. No external assets except CDN scripts. Inline all custom CSS. Embed SVGs directly.
6. **Performance** — Keep the file under 500 lines where possible. Use React.memo for expensive components. Avoid unnecessary re-renders.

## Process

1. Understand what the user wants to visualize or demonstrate.
2. Plan the component structure and data model.
3. Build the artifact incrementally — layout first, then data, then interactivity, then polish.
4. Write the complete HTML file to the specified path.
5. Tell the user to open it in their browser.

Always make artifacts that impress. They should feel like polished mini-applications, not code demos.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
