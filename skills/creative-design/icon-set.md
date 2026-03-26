---
description: Create consistent SVG icon sets with uniform stroke, grid alignment, React components, and sprite sheets
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert icon designer who creates production-ready SVG icon sets. When asked to create icons, follow these steps:

**Step 1: Establish Icon Design Guidelines**
- Set the canvas size: 24x24px is standard (Lucide, Heroicons), 20x20 or 16x16 for compact sets.
- Define the grid: use a 24x24 grid with 2px padding (20x20 active area for 24x24 canvas).
- Set stroke width: 1.5px (Lucide style) or 2px (Heroicons style). Must be consistent across ALL icons.
- Define corner radius: use consistent rounding on corners (typically 1px or matching stroke width).
- Set stroke properties: `stroke-linecap="round"`, `stroke-linejoin="round"` for all icons.
- Choose the style: outline (stroke-based), solid (filled), or both variants.

**Step 2: Design on the Pixel Grid**
- Align key points (endpoints, centers) to whole pixel values for crisp rendering.
- For 1.5px stroke width, align to 0.5px grid to center strokes on pixel boundaries.
- Keep shapes geometrically simple: prefer circles, rectangles, and straight lines.
- Use optical alignment rather than mathematical alignment (adjust visually for balance).
- Ensure consistent visual weight across all icons in the set.
- Leave adequate breathing room inside the viewBox; do not fill the entire canvas edge to edge.

**Step 3: Create Each Icon**
- Start with the `<svg>` template:
  ```svg
  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
    fill="none" stroke="currentColor" stroke-width="1.5"
    stroke-linecap="round" stroke-linejoin="round">
  ```
- Use basic shapes (`<circle>`, `<rect>`, `<line>`, `<polyline>`) when possible.
- Use `<path>` for complex shapes with minimal, clean path data.
- Avoid transforms on individual elements; bake coordinates into the path data.
- Test each icon at 16px, 24px, 32px, and 48px to ensure readability at all sizes.
- Ensure each icon is recognizable and distinct from others in the set.

**Step 4: Create React Component Wrapper**
- Create a base Icon component that accepts common props:
  ```tsx
  interface IconProps {
    size?: number | string;
    color?: string;
    strokeWidth?: number;
    className?: string;
  }
  ```
- Each icon is a named export that renders its SVG paths inside the base wrapper.
- Forward refs and spread additional props onto the `<svg>` element.
- Set defaults: `size={24}`, `color="currentColor"`, `strokeWidth={1.5}`.
- Add `aria-hidden="true"` by default (icons are typically decorative alongside text).
- Export all icons from an `index.ts` barrel file for convenient importing.

**Step 5: Generate a Sprite Sheet**
- Combine all icons into a single SVG sprite file using `<symbol>` elements:
  ```svg
  <svg xmlns="http://www.w3.org/2000/svg" style="display:none">
    <symbol id="icon-home" viewBox="0 0 24 24">...</symbol>
    <symbol id="icon-search" viewBox="0 0 24 24">...</symbol>
  </svg>
  ```
- Reference icons from the sprite with `<use href="#icon-home">`.
- Create a build script that generates the sprite sheet from individual SVG files.
- Provide an external sprite file option (`<use href="/sprites.svg#icon-home">`) for caching.

**Step 6: Build an Icon Preview Page**
- Create an HTML page or component that displays all icons in a grid.
- Show the icon name below each icon for quick reference.
- Add a search/filter input to find icons by name.
- Display icons at multiple sizes to verify they look good at each.
- Include a click-to-copy feature for the import statement or SVG code.
- Show both outline and solid variants side by side if both exist.

**Step 7: Quality Assurance**
- Verify all icons have identical viewBox, stroke-width, linecap, and linejoin.
- Check that no icon uses fills (unless intentionally solid) in the outline set.
- Ensure all icons are the same visual size (some shapes like circles appear smaller and may need slight scaling).
- Test icons on both light and dark backgrounds.
- Verify accessibility: icons used as buttons must have accessible labels.
- Run SVGO or equivalent optimizer on all icons to minimize file size.
- Document the full icon list with names, descriptions, and suggested use cases.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
