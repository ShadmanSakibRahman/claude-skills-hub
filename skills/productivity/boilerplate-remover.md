---
description: Remove boilerplate by extracting utilities, higher-order functions, decorators, and applying DRY principles
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert at identifying and eliminating code repetition. When asked to reduce boilerplate, follow these steps:

**Step 1: Identify Repetitive Patterns**
- Scan the codebase for duplicated code blocks using structural similarity, not just exact matches.
- Look for common boilerplate categories:
  - Repeated API call patterns (fetch, error handling, loading states).
  - Similar CRUD operations across different resources.
  - Repeated form validation logic.
  - Duplicated component structures with slight variations.
  - Repeated try/catch blocks with the same error handling.
  - Copy-pasted configuration objects with minor differences.
- Count occurrences and note the locations of each repeated pattern.

**Step 2: Extract Shared Utilities**
- Create utility functions for repeated logic patterns.
- Place utilities in a shared directory (e.g., `lib/utils.ts`, `utils/helpers.ts`).
- Make utilities generic with parameters for the varying parts.
- Add proper TypeScript types and generics for type safety.
- Examples:
  - `formatCurrency(amount, locale, currency)` instead of inline `Intl.NumberFormat` calls.
  - `debounce(fn, ms)` instead of repeated setTimeout/clearTimeout patterns.
  - `groupBy(array, key)` instead of repeated reduce operations.
  - `fetcher<T>(url, options)` instead of repeated fetch-then-parse code.

**Step 3: Create Higher-Order Functions and Wrappers**
- For repeated function patterns, create higher-order functions that encapsulate the common logic.
- API handlers: create a `withAuth(handler)` wrapper that checks authentication.
- Error handling: create a `withErrorHandler(fn)` that wraps try/catch and logging.
- Validation: create a `withValidation(schema, handler)` that validates input before execution.
- Caching: create a `withCache(fn, ttl)` that memoizes results with time-to-live.
- Ensure the HOF preserves the original function's type signature.

**Step 4: Leverage Framework Patterns**
- **React**: Extract repeated logic into custom hooks (`useForm`, `useFetch`, `useDebounce`, `useLocalStorage`).
- **Vue**: Extract into composables (`useAuth`, `useTable`, `usePagination`).
- **Express/Fastify**: Extract into middleware (auth, validation, logging, rate limiting).
- **Django/Rails**: Use mixins, decorators, and class-based view inheritance.
- Identify where the framework already provides abstractions being reimplemented.

**Step 5: Create Reusable Components**
- For repeated UI patterns, extract into parameterized components.
- Create a component library for common elements: Button, Input, Card, Modal, Table, Form.
- Use composition patterns: slots/children, render props, or compound components.
- Make components configurable via props with sensible defaults.
- Extract repeated layout patterns into layout components.
- Use variants (via props or class variants) instead of creating near-duplicate components.

**Step 6: Apply Configuration-Driven Patterns**
- Replace repeated similar code with data-driven approaches.
- Define form fields as configuration arrays rendered by a generic form component.
- Define table columns as configuration objects rendered by a generic table component.
- Define routes as configuration arrays processed by a route generator.
- Define validation rules as declarative schemas (zod, yup) instead of imperative checks.
- Use factories that generate specific instances from a template.

**Step 7: Refactor and Verify**
- Replace each instance of the repeated code with the new abstraction.
- Ensure all existing tests still pass after the refactoring.
- Verify no functionality was lost in the extraction.
- Check that the new abstractions are properly exported and documented.
- Remove unused imports and dead code left behind by the refactoring.
- Confirm that the codebase is smaller, more readable, and easier to modify.
- Add a brief JSDoc comment to each new utility explaining its purpose and usage.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
