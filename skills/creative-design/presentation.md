---
description: Create HTML slide presentations with Reveal.js including code highlighting, animations, speaker notes, and PDF export
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert at creating engaging technical presentations using HTML-based slide frameworks. When asked to create a presentation, follow these steps:

**Step 1: Choose the Framework and Setup**
- Default to **Reveal.js** (most popular, feature-rich HTML presentation framework).
- Alternatives: Slidev (Vue-based, Markdown), Marp (Markdown-to-slides), Shower, or Impress.js.
- Set up via CDN for quick start or npm for customization:
  - CDN: include reveal.js CSS and JS from unpkg or cdnjs.
  - npm: `npm install reveal.js` with a build step.
- Create the HTML file with the Reveal.js boilerplate structure.
- Configure Reveal.js options: transition style, slide number format, hash navigation.

**Step 2: Structure the Slide Deck**
- Plan the presentation flow:
  1. **Title slide**: Title, subtitle, author name, date, and branding.
  2. **Agenda/Overview**: Outline of topics to be covered.
  3. **Content slides**: One key idea per slide (the "billboard test").
  4. **Demo/Code slides**: Live code examples with syntax highlighting.
  5. **Summary/Takeaways**: Key points recap.
  6. **Q&A/Contact**: Final slide with contact info or discussion prompt.
- Use horizontal slides for main topics and vertical slides (nested `<section>`) for subtopics.
- Limit slides to 20-30 for a typical 30-minute presentation.

**Step 3: Design Clean Typography**
- Use a sans-serif font for headings (Inter, Montserrat, or Poppins).
- Use a readable font for body text (minimum 24px for legibility on projectors).
- Set heading sizes: h1 at 48-60px, h2 at 36-48px, h3 at 28-36px.
- Limit text per slide: 5-7 bullet points maximum, each one line long.
- Use consistent text alignment: left-aligned for content, centered for titles.
- Apply a high-contrast color scheme: dark text on light background or light text on dark.

**Step 4: Add Code Highlighting**
- Use Reveal.js plugin for syntax highlighting (built-in highlight.js or Prism.js).
- Configure the code theme to match the presentation's color scheme.
- Use `<pre><code>` blocks with the appropriate language class: `class="language-typescript"`.
- Enable line numbers for reference: `data-line-numbers`.
- Highlight specific lines for emphasis: `data-line-numbers="3-5|8"` (with step-through).
- Keep code snippets short (10-15 lines max) and focused on the key concept.
- Use a monospace font at 18-20px minimum for readability.

**Step 5: Add Animations and Transitions**
- Set a global transition: `slide`, `fade`, `convex`, `concave`, or `none`.
- Use fragment animations for progressive reveal:
  - `class="fragment"`: Fade in on advance.
  - `class="fragment highlight-red"`: Highlight text.
  - `class="fragment fade-out"`: Fade out previous element.
  - `data-fragment-index="0"`: Control order of fragment animations.
- Use `data-auto-animate` for smooth element transitions between slides.
- Add background transitions: `data-background-color`, `data-background-image`, `data-background-video`.
- Keep animations purposeful; avoid gratuitous effects that distract from content.

**Step 6: Add Speaker Notes and Interactive Features**
- Add speaker notes using `<aside class="notes">` inside each slide section.
- Notes are visible in the speaker view (press `S` to open).
- Include timing reminders in notes: "2 minutes for this section".
- Add interactive features:
  - Overview mode: press `Esc` or `O` for slide overview grid.
  - Zoom: `Alt+click` to zoom into an element.
  - Timer: enable the elapsed time display.
  - Laser pointer: enable the pointer plugin for emphasis.
- Configure keyboard shortcuts for custom navigation if needed.

**Step 7: Export and Distribute**
- Enable PDF export: add `?print-pdf` to the URL and use browser Print to PDF.
- Configure the print stylesheet for clean PDF output:
  - Remove navigation controls and progress bar.
  - Ensure slide backgrounds render in PDF.
  - Set page size to match slide dimensions (typically 960x700 or 1920x1080).
- Make the presentation responsive for viewing on different screen sizes.
- Host on GitHub Pages, Netlify, or Vercel for easy sharing via URL.
- Provide a standalone HTML file option (embed all CSS/JS) for offline viewing.
- Include a README with instructions for running, modifying, and exporting the presentation.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
