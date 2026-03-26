---
description: Convert HTML templates to properly formatted JSX/TSX with React conventions
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in converting HTML to React JSX/TSX. When this skill is invoked, do the following:

1. Ask the user which HTML file(s) to convert, or identify them from context.
2. Read the HTML file(s) completely and analyze the structure.
3. Read the target React project to understand:
   - Whether the project uses TypeScript (TSX) or JavaScript (JSX)
   - The component naming convention and file structure
   - The styling approach (Tailwind, CSS Modules, styled-components)
   - Available UI component libraries that could replace raw HTML elements

4. Perform systematic HTML-to-JSX transformations:

   **Attribute renaming:**
   - `class` -> `className`
   - `for` -> `htmlFor`
   - `tabindex` -> `tabIndex`
   - `readonly` -> `readOnly`
   - `maxlength` -> `maxLength`
   - `cellpadding` -> `cellPadding`
   - `cellspacing` -> `cellSpacing`
   - `colspan` -> `colSpan`
   - `rowspan` -> `rowSpan`
   - `enctype` -> `encType`
   - `crossorigin` -> `crossOrigin`
   - `autocomplete` -> `autoComplete`
   - `autofocus` -> `autoFocus`
   - `novalidate` -> `noValidate`
   - All `data-*` and `aria-*` attributes remain unchanged (kebab-case is correct in JSX)

   **Style attribute conversion:**
   - Convert inline `style="color: red; font-size: 16px"` to `style={{ color: 'red', fontSize: '16px' }}`
   - Convert CSS property names from kebab-case to camelCase
   - Convert numeric values: keep as numbers without `px` suffix where JSX accepts numbers
   - Wrap string values in quotes, number values without quotes

   **Self-closing tags:**
   - Close all void elements: `<br>` -> `<br />`, `<img>` -> `<img />`, `<input>` -> `<input />`, `<hr>` -> `<hr />`
   - Also self-close: `<meta />`, `<link />`, `<area />`, `<col />`, `<embed />`, `<source />`, `<track />`, `<wbr />`

   **Event handlers:**
   - Convert inline handlers: `onclick="handleClick()"` -> `onClick={handleClick}`
   - Convert `onchange` -> `onChange`, `onsubmit` -> `onSubmit`, `onfocus` -> `onFocus`, etc.
   - Extract inline JavaScript from event handlers into component functions
   - Convert `addEventListener` patterns in `<script>` tags to React event props

   **Conditional rendering:**
   - Convert `style="display: none"` toggling to conditional rendering with `{condition && <Element />}`
   - Convert template `if/else` blocks to ternary expressions or early returns
   - Convert `hidden` attribute usage to conditional rendering

   **List rendering:**
   - Convert repeated HTML elements into `.map()` with proper `key` props
   - Identify unique identifiers for keys (IDs, slugs); avoid using array index for dynamic lists
   - Wrap the map call in a fragment `<>...</>` or parent element as needed

5. Extract components from the HTML:
   - Identify repeated patterns and extract them as reusable components
   - Identify logical sections (header, sidebar, card, list-item) as separate components
   - Pass dynamic content as props with proper TypeScript interfaces
   - Keep the component hierarchy shallow (2-3 levels maximum)

6. Handle embedded content:
   - Convert `<script>` tags: extract logic into `useEffect` hooks or component body
   - Convert `<script>` external references to proper imports
   - Convert `<style>` tags to the project's styling solution (CSS Module, Tailwind classes, etc.)
   - Convert `<link>` stylesheet references to CSS imports
   - Move `<meta>` tags to the appropriate head management (Next.js metadata, react-helmet)

7. Handle special HTML patterns:
   - Convert HTML comments `<!-- -->` to JSX comments `{/* */}`
   - Convert HTML entities (`&amp;`, `&lt;`, `&nbsp;`) to their character equivalents or use Unicode
   - Convert `<template>` elements to React fragments
   - Convert `<slot>` elements to `{children}` or named props
   - Remove `type="text/javascript"` and `type="text/css"` attributes (unnecessary)

8. Clean up and finalize:
   - Ensure all JSX is wrapped in a single root element (use fragments `<>...</>` to avoid extra DOM nodes)
   - Add proper imports for any hooks, components, or utilities used
   - Format the output with consistent indentation matching the project style
   - Verify the conversion is complete with no remaining raw HTML syntax

Best practices to follow:
- Preserve the original visual appearance and behavior exactly
- Use semantic React patterns (controlled inputs, event delegation)
- Extract magic strings and numbers into constants or props
- Add TypeScript types for all props, event handlers, and state
- Flag any HTML that relies on jQuery or vanilla JS DOM manipulation for manual review
- Preserve accessibility attributes throughout the conversion

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
