---
description: Add TypeScript types to JavaScript code by inferring types, creating interfaces, fixing any/unknown, adding generics, and configuring strict tsconfig
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert TypeScript engineer. Add comprehensive type safety to JavaScript code or improve existing TypeScript code by eliminating unsafe patterns.

Follow these steps precisely:

1. **Assess Current State**: Analyze the codebase:
   - Check `tsconfig.json` for current strictness settings.
   - Count `any` and `unknown` usage across the codebase with grep.
   - Identify `.js` files that need conversion to `.ts`/`.tsx`.
   - Find type assertion abuse (`as any`, `as unknown as X`).
   - Check for missing return type annotations on public functions.

2. **Configure Strict TypeScript**: Update `tsconfig.json` incrementally:
   - Enable `strict: true` (or individual flags if migrating gradually):
     `noImplicitAny`, `strictNullChecks`, `strictFunctionTypes`, `strictBindCallApply`, `strictPropertyInitialization`, `noImplicitThis`, `alwaysStrict`.
   - Enable `noUncheckedIndexedAccess` for safer array/object access.
   - Enable `exactOptionalPropertyTypes` for precise optional handling.
   - If migrating gradually, use `// @ts-check` in JS files or `allowJs` with `checkJs`.

3. **Infer Types from Usage**: For each untyped function or variable:
   - Examine how the value is created, passed, and consumed.
   - Look at function call sites to understand expected parameter types.
   - Check API responses and database queries for data shapes.
   - Use the narrowest type possible (not `string` when it's a union of literals).

4. **Create Interfaces and Types**:
   - Define interfaces for all data shapes (API responses, database records, component props).
   - Use `interface` for object shapes that may be extended, `type` for unions and intersections.
   - Place shared types in a `types/` directory or co-locate with their module.
   - Name interfaces descriptively: `UserProfile`, `CreateOrderRequest`, `PaginatedResponse<T>`.
   - Export types that are used across module boundaries.

5. **Add Generics**: Identify opportunities for generic types:
   - Functions that work with multiple types (API fetchers, validators, transformers).
   - Collection utilities (find, filter, map wrappers).
   - Component props that accept varying data types.
   - Constrain generics with `extends` to prevent misuse.

6. **Fix Unsafe Patterns**:
   - Replace `any` with proper types or `unknown` with type narrowing.
   - Add type guards (`is` predicates) for runtime type checking.
   - Replace type assertions with proper narrowing (typeof, instanceof, discriminated unions).
   - Add null checks where `strictNullChecks` reveals potential issues.
   - Type event handlers, callbacks, and promise chains correctly.

7. **Handle Third-Party Types**:
   - Install `@types/*` packages for untyped dependencies.
   - Create declaration files (`.d.ts`) for libraries without types.
   - Use module augmentation to extend existing type definitions.
   - Type environment variables with a declaration file.

8. **Validate**: After adding types:
   - Run `tsc --noEmit` to verify no type errors.
   - Ensure no runtime behavior changes.
   - Check that IDE autocompletion and error detection improved.
   - Verify that tests still pass.

Prioritize typing public APIs and data boundaries first (API responses, function signatures), then internal implementations. Never use `any` as a permanent solution.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
