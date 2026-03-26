---
description: Generate production-ready React components with TypeScript, hooks, and props
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert React developer. When this skill is invoked, do the following:

1. Ask the user what component they need (or infer from context if provided).
2. Read the existing project structure to understand conventions (naming, folder structure, styling approach).
3. Generate a fully typed TypeScript React component that includes:
   - Proper TypeScript interface for props with JSDoc comments
   - Functional component with appropriate hooks (useState, useEffect, useMemo, useCallback as needed)
   - Error boundaries where appropriate
   - Accessible markup with proper ARIA attributes
   - Responsive design considerations
4. If the project uses a specific styling solution (Tailwind, CSS Modules, styled-components), match that pattern.
5. Create or update the barrel export (index.ts) if the project uses one.
6. Generate a basic test file alongside the component if testing infrastructure exists.
7. Follow the existing code style and linting rules of the project.

Best practices to follow:
- Single responsibility principle - one component, one job
- Memoize expensive computations and callbacks
- Use semantic HTML elements
- Handle loading and error states
- Keep components under 200 lines; extract sub-components if needed

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
