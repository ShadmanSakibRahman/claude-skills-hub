---
description: Implement dark mode with system detection, manual toggle, persistence, and proper contrast
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in implementing dark mode for web applications. When this skill is invoked, do the following:

1. Read the existing project to determine the current setup:
   - Identify the framework (React, Next.js, Vue, Svelte)
   - Check for existing theme/dark mode implementation to extend rather than replace
   - Determine the styling approach (Tailwind, CSS custom properties, CSS-in-JS, CSS Modules)
   - Check for an existing component library with built-in dark mode support
   - Look at current color usage patterns across the codebase

2. Set up the theme infrastructure based on the styling approach:

   **Tailwind CSS approach:**
   - Configure `darkMode: 'class'` in `tailwind.config.ts` (preferred over `media` for user control)
   - Add `dark:` variant classes to all color-related utilities throughout the project
   - Define semantic color tokens in the Tailwind config that swap values based on theme
   - Example: `bg-white dark:bg-gray-900`, `text-gray-900 dark:text-gray-100`

   **CSS Custom Properties approach:**
   - Define a complete set of CSS custom properties on `:root` for the light theme
   - Define dark theme overrides on `[data-theme="dark"]` or `.dark` class on `<html>`
   - Use semantic property names that describe purpose, not appearance:
     - `--color-bg-primary`, `--color-bg-secondary`, `--color-bg-tertiary`
     - `--color-text-primary`, `--color-text-secondary`, `--color-text-muted`
     - `--color-border`, `--color-ring`, `--color-shadow`
     - `--color-accent`, `--color-accent-hover`, `--color-accent-active`
   - Apply custom properties throughout all component styles

   **CSS-in-JS approach:**
   - Create a `lightTheme` and `darkTheme` object with identical keys but different values
   - Wrap the app with a `ThemeProvider` that switches between theme objects
   - Access theme values via the library's hook (`useTheme`, `styled` props)

3. Implement system preference detection:
   - Use `window.matchMedia('(prefers-color-scheme: dark)')` to detect OS-level preference
   - Listen for changes with `matchMedia.addEventListener('change', handler)` for real-time OS toggles
   - Use system preference as the default when no user preference is stored
   - For SSR/Next.js: prevent flash of incorrect theme with an inline script in `<head>` that runs before React hydrates:
     ```
     <script dangerouslySetInnerHTML={{ __html: `
       (function() {
         const stored = localStorage.getItem('theme');
         const preferred = window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
         document.documentElement.classList.add(stored || preferred);
       })();
     ` }} />
     ```

4. Implement manual toggle with persistence:
   - Create a `useTheme` hook or composable that provides:
     - `theme`: current theme value (`'light'`, `'dark'`, or `'system'`)
     - `resolvedTheme`: the actual applied theme after resolving `'system'`
     - `setTheme(theme)`: function to change theme
     - `toggleTheme()`: convenience function to cycle between themes
   - Persist user preference to `localStorage` under a consistent key (e.g., `'theme-preference'`)
   - Apply the theme by adding/removing a class or data attribute on `document.documentElement`
   - Support three modes: Light, Dark, and System (follows OS preference)

5. Create a theme toggle UI component:
   - Use an accessible button or segmented control with sun/moon/system icons
   - Add proper `aria-label` that describes the current state (e.g., "Switch to dark mode")
   - Include smooth icon transitions between states
   - Position consistently in the header/navbar

6. Apply smooth transitions between themes:
   - Add `transition: background-color 200ms ease, color 200ms ease, border-color 200ms ease` to transitioning elements
   - Alternatively, add a global transition class temporarily during theme switches and remove it after transition completes (prevents transitions on every page load)
   - Avoid transitioning `box-shadow` (use opacity on a pseudo-element instead for performance)

7. Ensure proper contrast ratios in both themes:
   - Verify text-to-background contrast meets WCAG AA (4.5:1 for normal text, 3:1 for large text)
   - Dark mode is NOT just inverted colors; design it intentionally:
     - Use slightly desaturated colors in dark mode (pure saturated colors are harsh on dark backgrounds)
     - Reduce elevation shadows; use subtle lighter borders instead in dark mode
     - Background surfaces should use dark grays (not pure black) for depth perception
     - Text should be off-white (not pure white) to reduce eye strain
   - Check that status colors (success green, error red, warning yellow) remain distinguishable in both modes
   - Verify that images, logos, and illustrations work in both themes (consider providing dark variants)

8. Handle edge cases:
   - Images: add a subtle background or border if images have transparent backgrounds
   - SVGs and icons: ensure they use `currentColor` so they adapt to the theme
   - Third-party embeds (maps, videos): wrap with appropriate backgrounds
   - Code blocks and syntax highlighting: provide both light and dark highlight themes
   - Form elements: ensure native browser inputs (date picker, select dropdown) are styled for both themes
   - Scrollbar styling: consider custom scrollbar colors for dark mode (`scrollbar-color` CSS property)

Best practices to follow:
- Never flash the wrong theme on page load (solve FOUC with the inline script approach)
- Test both themes on every page, not just the main page
- Use semantic color names, not literal ones (use `--bg-primary`, not `--white` / `--dark-gray`)
- Dark mode is not an afterthought; design both themes as first-class experiences
- Respect user autonomy: always allow manual override of system preference
- Test with actual users who prefer dark mode; contrast issues are common

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
