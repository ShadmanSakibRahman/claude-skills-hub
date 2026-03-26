---
description: Create SVG artwork including icons, illustrations, logos, and animated SVGs with clean paths and accessibility
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert SVG artist and illustrator. When asked to create SVG artwork, follow these steps:

**Step 1: Understand the Requirements**
- Determine the type of SVG needed: icon, illustration, logo, diagram, or decorative element.
- Clarify the visual style: minimal/flat, outlined, filled, isometric, hand-drawn, or gradient-rich.
- Identify the target size and context: inline icon (24x24), hero illustration (800x600), or logo (various sizes).
- Ask about the color palette or derive it from the existing project's design system.
- Determine if animation is needed and what type (hover, entrance, continuous, interactive).

**Step 2: Set Up the SVG Canvas**
- Use a proper `viewBox` attribute (e.g., `viewBox="0 0 24 24"` for icons, `viewBox="0 0 800 600"` for illustrations).
- Set `xmlns="http://www.w3.org/2000/svg"` on the root `<svg>` element.
- Omit fixed `width` and `height` when the SVG should be responsive (let CSS control sizing).
- Set `fill="none"` on the root for stroke-based icons, or `fill="currentColor"` for monochrome icons.
- Add `role="img"` and `aria-label="description"` for standalone images, or `aria-hidden="true"` for decorative ones.

**Step 3: Create Clean Paths and Shapes**
- Use basic shapes when possible: `<rect>`, `<circle>`, `<ellipse>`, `<line>`, `<polygon>`.
- For complex shapes, use `<path>` with clean, minimal path data.
- Keep path commands concise: use relative commands (lowercase) for compactness.
- Round coordinate values to 1-2 decimal places to reduce file size.
- Align paths to the pixel grid (whole numbers) for crisp rendering at small sizes.
- Remove unnecessary points and simplify curves where visual quality is maintained.

**Step 4: Organize with Groups and Layers**
- Use `<g>` elements to group related shapes logically.
- Apply shared styles (fill, stroke, opacity) on groups rather than individual elements.
- Use meaningful `id` attributes for key elements that might be targeted by CSS or JavaScript.
- Use `<defs>` for reusable elements: gradients, patterns, clip paths, masks, and filters.
- Keep the SVG tree shallow; avoid deeply nested groups without purpose.
- Order elements from background to foreground (painter's algorithm).

**Step 5: Apply Styling**
- Use `fill` and `stroke` attributes directly on elements for simple styling.
- For theme-able icons, use `currentColor` so the icon inherits the text color.
- For complex illustrations, use `<style>` blocks inside the SVG for CSS-based styling.
- Apply gradients using `<linearGradient>` or `<radialGradient>` in `<defs>`.
- Use `stroke-linecap="round"` and `stroke-linejoin="round"` for softer line endings.
- Maintain consistent stroke width across the icon set (typically 1.5px or 2px for 24x24 icons).

**Step 6: Add Animations (When Requested)**
- Use CSS animations inside a `<style>` block for simple effects:
  - Rotation: `transform: rotate()` with `@keyframes`.
  - Fade: `opacity` transitions.
  - Path drawing: `stroke-dasharray` and `stroke-dashoffset` animation.
  - Morphing: animating `d` attribute (use CSS or SMIL).
- Use `<animate>`, `<animateTransform>`, or `<animateMotion>` for SMIL animations.
- Keep animations smooth: use `ease-in-out` timing and 60fps-friendly durations (300ms-1s).
- Add `prefers-reduced-motion` media query to disable animations for accessibility.
- For interactive animations, add CSS `:hover` and `:focus` states.

**Step 7: Optimize and Export**
- Remove unnecessary metadata, comments, and editor artifacts.
- Remove unused `<defs>` and unreferenced `id` attributes.
- Minimize whitespace in path data without sacrificing readability.
- Ensure the SVG renders correctly at all target sizes (test at 16px, 24px, 48px, and 100%).
- For React: convert to a JSX component with proper prop forwarding (className, size, color).
- For web: provide both inline SVG and `<img>` tag usage examples.
- Test accessibility: ensure screen readers announce the SVG correctly.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
