---
description: Create or extend a design system with tokens, reusable components, theming, and dark mode
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in design systems and component architecture. When this skill is invoked, do the following:

1. Ask the user what they need: a new design system from scratch, extending an existing one, or adding specific tokens/components. Infer from context if possible.
2. Read the existing project to understand the current state:
   - Check for existing design tokens, theme files, or CSS custom properties
   - Identify component library in use (Radix, Shadcn, Headless UI, Chakra, MUI)
   - Determine styling approach (Tailwind, CSS-in-JS, CSS Modules, vanilla CSS)
   - Look for existing theming or dark mode implementation
3. Define or extend design tokens as a structured, single source of truth:

   **Colors:**
   - Establish a semantic color scale: primary, secondary, accent, neutral, success, warning, error, info
   - Define each semantic color with shades (50-950) for flexibility
   - Create semantic aliases: `background`, `foreground`, `muted`, `card`, `border`, `input`, `ring`
   - Ensure all color pairings meet WCAG AA contrast ratios (4.5:1 for text, 3:1 for UI)

   **Typography:**
   - Define a type scale with consistent ratios (1.25 major third or 1.333 perfect fourth)
   - Set font families: `sans`, `serif`, `mono` with proper fallback stacks
   - Define font weights used in the system (regular, medium, semibold, bold)
   - Set line heights optimized for readability (1.5 for body, 1.2 for headings)

   **Spacing:**
   - Define a spacing scale based on a base unit (typically 4px or 0.25rem)
   - Include values: 0, 1, 2, 3, 4, 5, 6, 8, 10, 12, 16, 20, 24, 32, 40, 48, 64

   **Other tokens:**
   - Border radii: `none`, `sm`, `md`, `lg`, `xl`, `full`
   - Shadows: `sm`, `md`, `lg`, `xl`, `inner`, `none`
   - Transitions: durations (fast, normal, slow) and easing functions
   - Z-index scale: `base`, `dropdown`, `sticky`, `modal`, `popover`, `toast`, `tooltip`

4. Implement tokens in the appropriate format:
   - **Tailwind:** Extend `tailwind.config.ts` theme with token values
   - **CSS Custom Properties:** Create `:root` and `[data-theme="dark"]` rule sets
   - **CSS-in-JS:** Create a theme object exportable for ThemeProvider
   - **JSON/JS tokens:** Create a tokens file importable across platforms

5. Set up theming and dark mode:
   - Implement theme switching using `data-theme` attribute on `<html>` or a class-based approach
   - Detect system preference with `prefers-color-scheme` media query
   - Persist user preference to `localStorage`
   - Provide a toggle component with system/light/dark options
   - Ensure smooth transitions between themes (`transition: background-color 200ms, color 200ms`)
   - Define all color tokens as pairs (light value and dark value)

6. Create foundational reusable components:
   - **Button:** variants (primary, secondary, outline, ghost, link), sizes (sm, md, lg), loading/disabled states
   - **Input:** text, textarea, select with consistent styling, error states, labels
   - **Card:** with header, body, footer composition
   - **Badge:** informational labels with color variants
   - **Typography:** Heading (h1-h6) and Text components with size/weight props
   - Each component should accept a `className` prop for extension

7. Document the design system:
   - Add JSDoc comments to all token exports
   - Include usage examples as code comments in component files
   - List available variants, sizes, and states for each component

Best practices to follow:
- Tokens are the single source of truth; components consume tokens, never hardcode values
- Use CSS custom properties for runtime theming (they update without re-render)
- Compose complex components from primitive ones (a Dialog uses Button, Typography, and Card internally)
- Design for extension: consumers should be able to override styles without fighting specificity
- Version your design system tokens to track breaking changes
- Test all components in both light and dark themes before shipping

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
