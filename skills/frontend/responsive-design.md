---
description: Analyze a component or page and make it fully responsive across mobile, tablet, and desktop
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in responsive web design. When this skill is invoked, do the following:

1. Ask the user which component or page to make responsive, or identify it from context.
2. Read the target file(s) and all related style files to understand the current layout.
3. Identify the project's styling approach (Tailwind, CSS Modules, styled-components, vanilla CSS) and work within that system.
4. Apply a mobile-first responsive strategy:
   - Start with the smallest viewport (320px) as the base styles
   - Layer on tablet styles (768px) as the first breakpoint
   - Add desktop styles (1280px) as the next breakpoint
   - Consider large desktop (1536px+) if the layout benefits from it
5. Convert fixed layouts to flexible ones:
   - Replace fixed widths with `max-width`, percentage, or viewport-relative units
   - Convert pixel-based grids to CSS Grid with `auto-fit`/`auto-fill` and `minmax()`
   - Use Flexbox `flex-wrap` for content that should reflow
   - Set appropriate `min-width: 0` on flex children to prevent overflow
   - Use `clamp()` for fluid sizing where appropriate (e.g., `clamp(1rem, 2.5vw, 2rem)`)
6. Implement fluid typography:
   - Use `clamp()` for font sizes that scale smoothly between breakpoints
   - Ensure line heights and letter spacing adjust proportionally
   - Keep body text between 16px-18px minimum for readability on mobile
   - Limit line length to 60-80 characters on wide screens using `max-width: 65ch`
7. Handle responsive images and media:
   - Add `max-width: 100%` and `height: auto` as baseline
   - Use `<picture>` with `<source>` for art direction across breakpoints
   - Add `srcset` and `sizes` attributes for resolution switching
   - Lazy load below-the-fold images with `loading="lazy"`
   - Use `aspect-ratio` to prevent layout shifts
8. Optimize touch interactions for mobile:
   - Ensure tap targets are at least 44x44px (WCAG 2.5.5)
   - Add adequate spacing between interactive elements
   - Replace hover-dependent interactions with click/tap alternatives
   - Use `@media (hover: hover)` to scope hover styles to devices that support them
9. Handle navigation responsively:
   - Implement hamburger menu or bottom navigation for mobile
   - Ensure the mobile menu is accessible (focus trap, escape to close, aria-expanded)
   - Consider sticky headers with reduced height on scroll for mobile
10. Test edge cases:
    - Verify no horizontal scrolling occurs at any viewport width
    - Check that text does not overflow containers
    - Ensure modals, dropdowns, and tooltips remain visible and usable
    - Verify tables either scroll horizontally, stack vertically, or use a responsive pattern
11. Add responsive utility styles if they do not already exist in the project:
    - Visually hidden class for screen-reader-only content
    - Container classes with responsive padding

Best practices to follow:
- Mobile-first: base styles for mobile, use `min-width` media queries to add complexity
- Avoid hiding content on mobile just to simplify; restructure instead
- Test with real device widths, not just the browser's responsive mode
- Use relative units (rem, em, %, vw, vh) over absolute units (px)
- Ensure interactive elements remain accessible at all sizes
- Preserve content hierarchy and reading order across breakpoints

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
