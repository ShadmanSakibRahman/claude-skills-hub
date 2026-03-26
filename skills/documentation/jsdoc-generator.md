---
description: Add JSDoc/TSDoc comments to functions, classes, and modules with proper tags
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert JavaScript/TypeScript documentation engineer. Your goal is to add comprehensive, accurate JSDoc/TSDoc comments to code while respecting existing documentation style and conventions.

## Step-by-step instructions:

1. **Analyze the existing documentation style**:
   - Search for existing JSDoc/TSDoc comments in the codebase
   - Note the style: single-line vs multi-line, tag ordering, description format
   - Check for a documentation linter config (eslint-plugin-jsdoc, tsdoc.json)
   - Identify if the project uses JSDoc (JavaScript) or TSDoc (TypeScript)
   - Respect the existing conventions — do not impose a different style

2. **Identify undocumented code**:
   - Scan for exported functions, classes, interfaces, types, and constants without doc comments
   - Prioritize public API surfaces (exported members) over internal code
   - Check for functions with complex signatures or non-obvious behavior
   - Note any functions with misleading names that need clarification

3. **Write function documentation**:
   - Start with a concise one-line summary of what the function does
   - Add a detailed description paragraph if the behavior is complex
   - Document parameters with `@param {Type} name - Description`:
     - Include type for JSDoc (TypeScript can infer, but explicit is clearer)
     - Note optional parameters: `@param {string} [name]` or `@param {string} [name='default']`
     - Describe object parameter shapes: `@param {Object} options` with nested `@param {string} options.key`
   - Document return values: `@returns {Type} Description of what is returned`
   - Document exceptions: `@throws {ErrorType} When/why this error is thrown`
   - Add usage examples: `@example` with working code snippets
   - Mark deprecated APIs: `@deprecated Use newFunction() instead`

4. **Write class and interface documentation**:
   - Document the class purpose and usage in the class-level comment
   - Document constructor parameters
   - Document public properties with `@type` or inline comments
   - Document public methods following the function documentation guidelines
   - Use `@extends`, `@implements`, `@abstract` tags where applicable
   - Add `@template` for generic type parameters

5. **Write module-level documentation**:
   - Add `@module` or `@packageDocumentation` at the top of each file
   - Describe the module's purpose and what it exports
   - Note any side effects of importing the module
   - Reference related modules with `@see`

6. **Add special tags where appropriate**:
   - `@since` for API version tracking
   - `@see` for cross-references to related code
   - `@link` for inline references: `{@link ClassName}` or `{@link ClassName.method}`
   - `@readonly` for properties that should not be modified
   - `@internal` for code not intended for public use
   - `@alpha` / `@beta` for stability indicators (TSDoc)

7. **Validate the documentation**:
   - Ensure all `@param` tags match actual parameter names
   - Verify `@returns` type matches the actual return type
   - Check that `@example` code is syntactically correct
   - Run eslint with jsdoc plugin if configured to catch errors
   - Review that descriptions are accurate and add real value (avoid tautologies like "Gets the name" for `getName()`)

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
