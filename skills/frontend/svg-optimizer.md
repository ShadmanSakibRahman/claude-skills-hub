---
description: Optimize SVG files, convert to React components, and ensure accessibility
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in SVG optimization and integration. When this skill is invoked, do the following:

1. Ask the user which SVG file(s) to optimize, or identify them from context.
2. Read each SVG file completely and analyze its structure and complexity.
3. Check the project setup:
   - Determine if SVGs are used as inline components, `<img>` sources, or CSS backgrounds
   - Check for SVGR or similar SVG-to-component tooling in the build pipeline
   - Identify naming conventions for icon/illustration components
   - Look for an existing icon system or sprite sheet

4. Optimize the SVG markup:

   **Remove unnecessary metadata:**
   - Strip XML declarations (`<?xml ...?>`)
   - Remove editor metadata (`<metadata>`, Sketch/Figma/Illustrator comments)
   - Remove `xmlns:xlink` if no `xlink:href` attributes are used (modern browsers support `href` directly)
   - Remove default namespace declarations that duplicate the root `xmlns`
   - Strip `data-name` and other editor-generated attributes
   - Remove empty `<defs>` blocks, unused `<clipPath>`, `<mask>`, and `<filter>` definitions

   **Minify paths and shapes:**
   - Round coordinate values to 2 decimal places (or fewer if visual quality is preserved)
   - Convert absolute path commands to relative where it shortens the output
   - Remove redundant path commands (consecutive `L` commands that can be implicit)
   - Merge adjacent paths with the same fill/stroke into a single path
   - Convert simple `<path>` elements to simpler shapes where possible (`<rect>`, `<circle>`, `<line>`)
   - Remove unnecessary `transform` attributes by applying them directly to coordinates
   - Remove default attribute values (`fill-rule="nonzero"`, `stroke-miterlimit="4"`)

   **Optimize visual attributes:**
   - Convert named colors to shorter hex codes (`black` -> `#000`, `white` -> `#fff`)
   - Shorten 6-digit hex to 3-digit where possible (`#aabbcc` -> `#abc`)
   - Remove `fill="#000"` or `fill="black"` if it is the SVG default
   - Move repeated attributes to a parent `<g>` element to reduce duplication
   - Use `currentColor` for fills/strokes that should match the text color (enables CSS color inheritance)

   **Structural cleanup:**
   - Remove unnecessary wrapper `<g>` elements with no attributes
   - Flatten nested `<g>` elements where transforms can be combined
   - Add or correct the `viewBox` attribute if missing (essential for responsive scaling)
   - Remove hardcoded `width` and `height` from the root `<svg>` (let the consumer control sizing)
   - Ensure `xmlns="http://www.w3.org/2000/svg"` is present on the root element

5. Convert to React component (if the project uses React):
   - Create a functional component with TypeScript and `SVGProps<SVGSVGElement>` typing
   - Spread `...props` on the root `<svg>` element for consumer control of `className`, `style`, `width`, `height`
   - Add `width` and `height` props with sensible defaults matching the original viewBox
   - Replace `fill` and `stroke` hardcoded colors with `currentColor` or configurable props
   - Convert kebab-case SVG attributes to camelCase JSX (`stroke-width` -> `strokeWidth`, `fill-rule` -> `fillRule`, `clip-path` -> `clipPath`)
   - Convert `class` to `className`
   - Convert inline `style` strings to style objects
   - Remove `xmlns:xlink` and replace `xlink:href` with `href`
   - Name the component in PascalCase matching the file name (e.g., `arrow-left.svg` -> `ArrowLeftIcon`)

6. Ensure accessibility:
   - Add `<title>` element as the first child of `<svg>` with a descriptive label
   - Add `<desc>` element for complex illustrations that benefit from a longer description
   - Link `<title>` to the SVG with `aria-labelledby="title-id"` on the root element
   - For decorative SVGs: add `aria-hidden="true"` and `focusable="false"` and remove `<title>`/`<desc>`
   - Provide a prop to toggle between decorative and informative modes:
     ```tsx
     interface IconProps extends SVGProps<SVGSVGElement> {
       title?: string;  // If provided, icon is informative; if omitted, icon is decorative
     }
     ```
   - Add `role="img"` for informative SVGs

7. Set up icon system (if multiple SVGs are being processed):
   - Create an icon component that accepts a `name` prop and renders the corresponding SVG
   - Generate a barrel export file (`index.ts`) listing all icon components
   - Consider creating an SVG sprite sheet (`<symbol>` + `<use>`) for projects with many icons
   - Document available icons with their names and visual preview (as code comments)

8. Report the optimization results:
   - Show before/after file sizes for each SVG
   - List any visual changes that need manual verification
   - Flag SVGs that use features requiring special handling (filters, masks, animations, text)

Best practices to follow:
- Always preserve visual fidelity; compare before and after rendering
- Use `currentColor` as the default fill/stroke so icons adapt to their context
- Keep the `viewBox` intact; never remove it as it is essential for responsive SVG
- For animation, prefer CSS animations on SVG elements over SMIL (better browser support)
- Test SVGs at multiple sizes (16px, 24px, 48px) to ensure they remain crisp
- Prefer inline SVG components over `<img>` for icons that need to be styled dynamically

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
