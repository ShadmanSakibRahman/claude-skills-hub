---
description: Generate color palettes with WCAG contrast ratios, semantic colors, and CSS custom properties in HSL/HEX/RGB
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert color theorist and accessibility-focused designer. When asked to generate a color palette, follow these steps:

**Step 1: Understand the Context**
- Determine the purpose: brand identity, UI design system, data visualization, or specific component.
- Ask about brand values or mood: professional, playful, bold, calm, luxurious, minimal.
- Check for existing colors in the codebase (Tailwind config, CSS variables, theme files).
- Identify the primary use cases: light mode, dark mode, or both.
- Note any constraints: industry standards, accessibility requirements, existing brand guidelines.

**Step 2: Generate the Primary Palette**
- **Primary**: The main brand color, used for CTAs, links, and key interactive elements. Generate a full scale (50-950 in 50-step increments, or 100-900).
- **Secondary**: A complementary color for supporting elements. Can be analogous, complementary, or triadic to primary.
- **Accent**: A high-contrast color for highlights, badges, and attention-grabbing elements.
- **Neutral/Gray**: A comprehensive gray scale (50-950) for text, backgrounds, borders, and dividers. Tint slightly toward the primary hue for cohesion.
- Use HSL as the base format for easy manipulation (adjust lightness for scales, saturation for variants).

**Step 3: Generate Semantic Colors**
- **Success**: Green-based (#22c55e family). For confirmations, completed states, positive feedback.
- **Warning**: Amber/yellow-based (#f59e0b family). For caution states, pending actions.
- **Error/Destructive**: Red-based (#ef4444 family). For errors, destructive actions, alerts.
- **Info**: Blue-based (#3b82f6 family). For informational messages, tips, neutral notifications.
- Generate 3-5 shades for each semantic color: light (background), base (text/icon), dark (hover).
- Ensure semantic colors are distinguishable from each other and from the primary palette.

**Step 4: Verify WCAG Contrast Ratios**
- Check all text-on-background combinations meet WCAG 2.1 AA standards:
  - Normal text (below 18pt): minimum 4.5:1 contrast ratio.
  - Large text (18pt+ or 14pt bold): minimum 3:1 contrast ratio.
  - UI components and graphical objects: minimum 3:1 contrast ratio.
- For each color, specify which background it can be safely used on.
- Test primary button text on primary color background.
- Test body text on all background shades.
- Provide specific contrast ratios for the most common combinations.
- Adjust colors that fail contrast requirements while maintaining visual harmony.

**Step 5: Create Dark Mode Palette**
- Do not simply invert the light mode palette; create intentional dark mode colors.
- Dark mode backgrounds: use dark gray (not pure black) such as #0a0a0a, #171717, #262626.
- Reduce saturation slightly for vivid colors in dark mode to avoid eye strain.
- Increase lightness of text colors for readability on dark backgrounds.
- Ensure the primary color works well on both light and dark backgrounds.
- Maintain the same semantic meaning across modes (success is always green, error always red).

**Step 6: Output in Multiple Formats**
- Provide each color in three formats: HEX (#3b82f6), HSL (hsl(217, 91%, 60%)), RGB (rgb(59, 130, 246)).
- Create CSS custom properties using HSL for easy manipulation:
  ```css
  :root {
    --primary-500: 217 91% 60%;
    --primary-600: 217 91% 50%;
  }
  ```
- Generate a Tailwind CSS config extension with the custom colors.
- Create a colors constant file for JavaScript/TypeScript usage.
- If using shadcn/ui, output in the expected HSL format for globals.css.

**Step 7: Document and Present**
- Create a visual color reference showing all colors with their values.
- Document usage guidelines: when to use each color and appropriate combinations.
- Provide do's and don'ts: color combinations to use and avoid.
- Include examples of the palette applied to common UI elements: buttons, cards, alerts, navigation.
- Note any color blindness considerations (avoid relying solely on red/green differentiation).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
