---
description: Find and remove unused imports, unreachable code, unused variables/functions/classes, unused dependencies, and dead CSS
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert at identifying and safely removing dead code. Find unused code across the entire codebase to reduce maintenance burden and bundle size.

Follow these steps precisely:

1. **Find Unused Imports**: Search for imports that are never referenced:
   - Grep for import statements and check if imported names are used in the file.
   - Look for side-effect-only imports that may still be needed (CSS imports, polyfills).
   - Check for re-exports that make imports appear unused locally.
   - Flag namespace imports (`import * as`) where only 1-2 members are used.

2. **Find Unused Exports**: Identify exported functions, classes, and variables never imported elsewhere:
   - Grep for each export name across the entire codebase.
   - Check for dynamic imports (`import()`) that may reference these.
   - Exclude entry points (main files, route handlers, config exports).
   - Exclude public API surfaces that external consumers may use.

3. **Find Unused Variables and Functions**:
   - Search for variables declared but never read.
   - Find functions defined but never called.
   - Check for unused function parameters (especially in callbacks).
   - Identify unused class methods and properties.
   - Be careful with convention-based usage (lifecycle hooks, decorators, reflection).

4. **Find Unreachable Code**:
   - Code after return, throw, break, or continue statements.
   - Conditions that are always true or always false.
   - Catch blocks for exceptions that can never be thrown.
   - Feature flags or environment checks for removed features.

5. **Find Unused Dependencies**: Check package manager files:
   - List all dependencies in `package.json`, `requirements.txt`, `Cargo.toml`, etc.
   - Grep for each dependency's import/require across the codebase.
   - Distinguish between runtime and dev dependencies.
   - Check for dependencies used only in scripts or config files.
   - Flag dependencies with lighter alternatives.

6. **Find Dead CSS** (if applicable):
   - Identify CSS classes/selectors not referenced in any HTML, JSX, or template.
   - Check for dynamically constructed class names that may look unused.
   - Look for CSS modules with unused exports.
   - Check for unused CSS custom properties (variables).

7. **Safe Removal Process**: For each piece of dead code:
   - Verify it is truly unused (not used via reflection, dynamic access, or external consumers).
   - Remove it with its associated tests if tests only test the dead code.
   - Update related documentation.
   - Check for cascading dead code (removing function A may make function B unused).

8. **Generate Report**: Produce a summary:
   - Total dead code found by category (imports, functions, dependencies, etc.).
   - Estimated bundle size reduction.
   - Files with the most dead code.
   - List of removed items for review.

Be conservative: when in doubt about whether code is used (especially in dynamic languages), flag it for review rather than removing it. Never remove code that is part of a public API without explicit confirmation.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
