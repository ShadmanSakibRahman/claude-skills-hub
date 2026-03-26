---
description: Convert vanilla CSS or SCSS files to Tailwind CSS utility classes
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in CSS and Tailwind CSS. When this skill is invoked, do the following:

1. Ask the user which CSS/SCSS file(s) to convert, or identify them from context.
2. Read the target CSS/SCSS file completely and analyze every rule.
3. Check the project's Tailwind configuration:
   - Read `tailwind.config.js` or `tailwind.config.ts` for custom theme values, plugins, and presets
   - Check for existing custom utilities or components defined via `@layer`
   - Note the configured breakpoints, colors, and spacing scale
4. For each CSS rule, perform the conversion:
   - Map standard properties to their Tailwind utility equivalents (e.g., `display: flex` -> `flex`, `margin-top: 1rem` -> `mt-4`)
   - Convert media queries to responsive prefixes (`sm:`, `md:`, `lg:`, `xl:`, `2xl:`)
   - Convert pseudo-classes to variant prefixes (`hover:`, `focus:`, `active:`, `first:`, `last:`, `disabled:`)
   - Convert pseudo-elements where Tailwind supports them (`before:`, `after:` with `content-['']`)
   - Handle combinators and nested selectors by restructuring component markup if needed
   - Use arbitrary value syntax `[value]` for custom values not in the default scale (e.g., `w-[137px]`, `bg-[#1a2b3c]`)
   - Map CSS custom properties to Tailwind theme references where possible
5. Handle complex scenarios:
   - Convert CSS Grid layouts to Tailwind grid utilities (`grid`, `grid-cols-3`, `col-span-2`, etc.)
   - Convert Flexbox layouts preserving all flex properties
   - Convert animations and transitions to Tailwind equivalents or use arbitrary values
   - Convert SCSS variables to Tailwind theme values or CSS custom properties
   - Convert SCSS mixins to Tailwind `@apply` directives or utility compositions
   - Convert SCSS nesting to flat Tailwind class structures
6. Update the component file(s) that reference the CSS:
   - Replace `className` or `class` attributes with the converted Tailwind classes
   - Remove the CSS/SCSS import if the file is fully converted
   - Use `clsx` or `cn` utility for conditional classes if the project has one
7. For values that have no Tailwind equivalent, either:
   - Add them to `tailwind.config.js` under `theme.extend` if they are reused
   - Use arbitrary value syntax for one-off values
8. Verify no styles are lost by listing any unconverted rules and flagging them.
9. Clean up: delete the original CSS file only if the user confirms, otherwise leave it with a comment noting it has been converted.

Best practices to follow:
- Prefer Tailwind's design tokens over arbitrary values for consistency
- Group related utilities logically (layout, spacing, typography, colors, effects)
- Use `@apply` sparingly and only in global styles or component libraries
- Preserve dark mode styles using the `dark:` variant
- Keep class strings readable; use multi-line formatting for long class lists
- Document any custom theme extensions added during conversion

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
