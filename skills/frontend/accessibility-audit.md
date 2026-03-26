---
description: Perform a comprehensive WCAG 2.1 AA accessibility audit with prioritized fixes
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in web accessibility and WCAG 2.1 guidelines. When this skill is invoked, do the following:

1. Ask the user which files, components, or pages to audit, or identify them from context.
2. Read all target files thoroughly, including templates, components, and associated styles.
3. Perform a systematic audit against WCAG 2.1 AA success criteria, checking each category:

   **Images and Media (WCAG 1.1.1, 1.2.x):**
   - Every `<img>` must have meaningful `alt` text (or `alt=""` for decorative images)
   - `<svg>` elements need `role="img"` with `<title>` and optional `<desc>`, or `aria-hidden="true"` if decorative
   - Video/audio content needs captions and transcripts
   - Icon-only buttons must have `aria-label` or visually hidden text

   **Semantic HTML (WCAG 1.3.1, 1.3.2):**
   - Proper heading hierarchy (h1-h6) without skipping levels
   - Use `<nav>`, `<main>`, `<aside>`, `<header>`, `<footer>`, `<section>`, `<article>` landmarks
   - Lists use `<ul>`, `<ol>`, `<dl>` appropriately
   - Tables use `<thead>`, `<th scope>`, `<caption>` for data tables
   - Reading order in the DOM matches visual order

   **Color and Contrast (WCAG 1.4.3, 1.4.11):**
   - Text contrast ratio meets 4.5:1 for normal text, 3:1 for large text
   - UI component boundaries meet 3:1 contrast against adjacent colors
   - Information is not conveyed by color alone (add icons, patterns, or text)
   - Check both light and dark mode if applicable

   **Keyboard Navigation (WCAG 2.1.1, 2.1.2, 2.4.3, 2.4.7):**
   - All interactive elements are reachable via Tab key
   - No keyboard traps (user can always Tab away)
   - Logical tab order follows visual layout
   - Visible focus indicators on all focusable elements (check for `outline: none` without replacement)
   - Custom components implement expected keyboard patterns (Enter/Space for buttons, arrows for menus)
   - Skip link exists to bypass repetitive navigation

   **Forms (WCAG 1.3.5, 3.3.1, 3.3.2, 4.1.2):**
   - Every input has a visible `<label>` linked via `htmlFor`/`id`
   - Required fields are indicated beyond just color (asterisk, text, `aria-required`)
   - Error messages are associated with fields via `aria-describedby`
   - Autocomplete attributes are present for common fields (name, email, address)
   - Form validation errors are announced to screen readers

   **ARIA Usage (WCAG 4.1.2):**
   - ARIA roles, states, and properties are used correctly (no misuse of `role`)
   - `aria-live` regions for dynamic content updates (toasts, loading states, errors)
   - Modal dialogs use `role="dialog"`, `aria-modal="true"`, and focus trap
   - Expandable sections use `aria-expanded`
   - No redundant ARIA (e.g., `role="button"` on a `<button>`)

   **Focus Management (WCAG 2.4.3):**
   - Focus moves to modals when opened and returns when closed
   - Focus is managed after route changes in SPAs
   - `tabindex` usage is appropriate (-1 for programmatic focus, 0 for natural order, never positive values)

4. Generate a prioritized report with three sections:
   - **Critical** (blocks users entirely): missing alt text on informational images, keyboard traps, no focus indicators, missing form labels
   - **Major** (significant barriers): poor contrast, missing landmarks, no skip links, improper heading hierarchy
   - **Minor** (improvements): redundant ARIA, missing autocomplete, decorative images without empty alt

5. For each issue found, provide:
   - The file path and line number
   - The specific WCAG criterion violated
   - A concrete code fix (not just a description)
6. Offer to apply all fixes automatically, or let the user choose which to apply.

Best practices to follow:
- Test with the mindset of a keyboard-only user, screen reader user, and low-vision user
- Prefer native HTML semantics over ARIA (first rule of ARIA: do not use ARIA if native HTML works)
- Verify that dynamic content changes are announced appropriately
- Check that focus is never lost after interactions (deleting items, closing dialogs, navigation)

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
