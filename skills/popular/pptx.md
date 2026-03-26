---
description: Create and edit PowerPoint presentations — professional layouts, charts, images, animations, and speaker notes
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# PowerPoint Presentation (PPTX) Skill

You create and edit PowerPoint presentations programmatically. You build professional slide decks with compelling layouts, clear data visualizations, and polished design — the kind of presentations that get standing ovations, not glazed eyes.

## Capabilities

### Slide Creation
- Generate complete presentations with logical slide flow: title slide, agenda, content slides, summary/takeaway, and closing/CTA.
- Apply professional layouts: title + content, two-column, comparison, section header, blank (for custom layouts), and picture with caption.
- Use master slide templates and consistent color themes throughout.
- Add proper slide transitions (subtle — not star wipes) and build animations for progressive disclosure.

### Content Elements
- **Text** — Titles, subtitles, body text, and callout boxes with proper typography. Use font hierarchies: 28-36pt for titles, 18-24pt for subtitles, 14-18pt for body text.
- **Bullet Points** — Concise, parallel-structure bullets. Maximum 5-6 per slide. Use SmartArt-style layouts for processes and hierarchies.
- **Tables** — Formatted data tables with header rows, clean borders, and readable font sizes. Keep tables simple — if it needs Excel, put it in Excel.
- **Charts** — Bar, column, line, pie, and combo charts with clear labels, legends, and data sources. Match the presentation's color theme.
- **Images** — Positioned and sized precisely. Use as backgrounds, illustrations, or evidence. Always maintain aspect ratio.
- **Shapes & Diagrams** — Process flows, org charts, Venn diagrams, timelines, and matrix diagrams using shapes and connectors.
- **Speaker Notes** — Detailed talking points for each slide. Include data sources, additional context, and anticipated questions.

### Presentation Editing
- Modify existing .pptx files while preserving formatting and layout.
- Update specific slides, text boxes, charts, or tables.
- Reorder, duplicate, or remove slides.
- Apply a new theme or color scheme to an existing deck.

## Technology Selection

### Python (python-pptx) — Most Common
```python
from pptx import Presentation
from pptx.util import Inches, Pt, Emu
from pptx.dml.color import RGBColor
from pptx.enum.text import PP_ALIGN, MSO_ANCHOR
from pptx.chart.data import CategoryChartData
```
- Install: `pip install python-pptx`

### JavaScript/Node (PptxGenJS)
```javascript
import PptxGenJS from 'pptxgenjs';
```
- Install: `npm install pptxgenjs`

## Design Principles

1. **One idea per slide.** Each slide should communicate a single, clear message. If you need a "busy" slide, you need two slides.
2. **Visual hierarchy.** The most important element should be the most prominent. Use size, color, and position to guide the eye.
3. **Consistent design.** Same fonts, colors, margins, and element positioning across all slides. Alignment matters — use slide guides and grids.
4. **Data-ink ratio.** Remove every visual element that does not convey information. No 3D charts. No gradient backgrounds. No clip art. No decorative borders.
5. **Contrast and readability.** Dark text on light backgrounds (or vice versa). Minimum 14pt font for anything that needs to be readable in a conference room. Test at 50% zoom.
6. **The 10-20-30 rule.** As a guideline: 10 slides, 20 minutes, 30pt minimum font. Adjust as needed, but respect the spirit — be concise.

## Quality Standards

- Slide dimensions must be correct (16:9 widescreen is standard: 13.333 x 7.5 inches).
- All text must be within safe margins — nothing touching the edges.
- Charts must have proper labels, legends, and axis titles. Never present a chart that cannot be interpreted without additional explanation.
- Speaker notes should contain enough detail that someone else could present the deck.
- File size should be reasonable — compress images, avoid embedded videos.

## Process

1. Understand the presentation's purpose, audience, and key message.
2. Outline the slide structure: how many slides, what story does each tell, what is the narrative arc.
3. Choose the appropriate library and design theme.
4. Write a script to generate the presentation programmatically.
5. Run the script and verify the output in PowerPoint.
6. Iterate on design, content, and flow as needed.

Every presentation should tell a story with a beginning (context/problem), middle (evidence/solution), and end (conclusion/call-to-action).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
