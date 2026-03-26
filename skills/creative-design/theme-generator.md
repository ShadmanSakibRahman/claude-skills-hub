---
description: Generate complete UI themes with light/dark mode tokens, Tailwind config, CSS custom properties, and shadcn/ui theming
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in design systems and UI theming. When asked to generate a theme, follow these steps:

**Step 1: Analyze the Current Setup**
- Check for existing theme configuration: `tailwind.config.ts`, `globals.css`, `theme.ts`, CSS variables.
- Identify the UI library in use: shadcn/ui, Radix, MUI, Chakra, Ant Design, DaisyUI, or custom.
- Determine if Tailwind CSS is being used and its version.
- Check for existing color tokens, design tokens, or theme constants.
- Identify the current light/dark mode switching mechanism if any.

**Step 2: Define Design Tokens**
- Create a comprehensive token system covering:
  - **Colors**: background, foreground, card, popover, primary, secondary, muted, accent, destructive, border, input, ring.
  - **Typography**: font families (sans, serif, mono), font sizes (xs through 4xl), font weights, line heights, letter spacing.
  - **Spacing**: consistent scale based on 4px unit (0.5: 2px through 20: 80px).
  - **Border radius**: none, sm (2px), default (6px), md (8px), lg (12px), xl (16px), full.
  - **Shadows**: none, sm, default, md, lg, xl, 2xl, inner.
  - **Transitions**: durations (75ms, 150ms, 200ms, 300ms) and easing functions.

**Step 3: Generate Light Mode Theme**
- Define colors using HSL format for easy manipulation:
  ```css
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
    --primary: 221.2 83.2% 53.3%;
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 221.2 83.2% 53.3%;
    --radius: 0.5rem;
  }
  ```
- Ensure all foreground colors have sufficient contrast against their backgrounds.
- Create hover and active state variants (slightly darker/lighter).

**Step 4: Generate Dark Mode Theme**
- Create intentional dark mode colors, not just inverted light mode:
  ```css
  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
    --card: 222.2 84% 4.9%;
    --card-foreground: 210 40% 98%;
    --primary: 217.2 91.2% 59.8%;
    --primary-foreground: 222.2 47.4% 11.2%;
    --secondary: 217.2 32.6% 17.5%;
    --secondary-foreground: 210 40% 98%;
    --muted: 217.2 32.6% 17.5%;
    --muted-foreground: 215 20.2% 65.1%;
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 210 40% 98%;
    --border: 217.2 32.6% 17.5%;
    --input: 217.2 32.6% 17.5%;
    --ring: 224.3 76.3% 48%;
  }
  ```
- Use slightly elevated backgrounds for cards and popovers to create depth.
- Reduce saturation of vivid colors to prevent eye strain in dark mode.
- Test all interactive components in both modes.

**Step 5: Configure Tailwind CSS**
- Extend `tailwind.config.ts` to use the CSS custom properties:
  ```typescript
  theme: {
    extend: {
      colors: {
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: { DEFAULT: "hsl(var(--primary))", foreground: "hsl(var(--primary-foreground))" },
        // ... all other tokens
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
    },
  }
  ```
- Add the `darkMode: "class"` configuration for class-based dark mode switching.
- Define custom animation keyframes and durations in the Tailwind config.

**Step 6: Implement Dark Mode Toggle**
- Create a theme provider component that manages the current theme.
- Store the preference in localStorage with a key like `"theme"`.
- Respect system preference using `prefers-color-scheme` media query as default.
- Toggle by adding/removing the `dark` class on the `<html>` element.
- Prevent flash of wrong theme on page load: add a blocking script in `<head>` that sets the class before paint.
- Provide three options: Light, Dark, System.

**Step 7: Component-Level Theming**
- For shadcn/ui: customize component styles using the CSS variables in `globals.css`.
- Create component variants using class variance authority (CVA) or Tailwind variants.
- Define consistent component sizes: sm, default, lg for buttons, inputs, badges.
- Apply the theme tokens to all components: buttons, inputs, cards, alerts, dialogs, dropdowns.
- Test every component in both light and dark mode.
- Document the theme system: list all tokens, their values, and usage guidelines.
- Create a theme preview page showing all components in both modes side by side.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
