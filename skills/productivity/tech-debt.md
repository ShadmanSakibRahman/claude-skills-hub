---
description: Identify and prioritize technical debt including outdated deps, code smells, missing tests, and security issues
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in software quality and technical debt management. When asked to assess technical debt, follow these steps:

**Step 1: Dependency Health**
- Run `pnpm outdated` (or equivalent) to find outdated dependencies.
- Identify dependencies with major version gaps (e.g., React 17 when 19 is available).
- Run `pnpm audit` to find known security vulnerabilities.
- Check for deprecated packages by looking at their npm/PyPI pages or GitHub status.
- Identify abandoned packages (no commits in 2+ years, unresolved critical issues).
- Estimate upgrade effort for each: trivial, moderate, significant.

**Step 2: Code Smells and Anti-Patterns**
- Search for common code smells:
  - Files over 500 lines (likely need splitting).
  - Functions over 50 lines (too complex, need extraction).
  - Deeply nested callbacks or conditionals (4+ levels).
  - Duplicate code blocks (search for similar patterns across files).
  - `any` type usage in TypeScript (search for `: any`, `as any`).
  - Commented-out code blocks (should be removed, history is in git).
  - TODO/FIXME/HACK comments that indicate unfinished work.
  - Magic numbers and hardcoded strings that should be constants.
- Note each smell with its location, severity, and suggested fix.

**Step 3: Test Coverage Gaps**
- Check if a testing framework is configured and tests exist.
- Identify critical paths with no tests: auth flows, payment processing, data mutations.
- Look for test files that only have skipped or placeholder tests.
- Check for integration/E2E tests beyond unit tests.
- Assess test quality: do tests test behavior or just implementation details?
- Estimate the effort to reach adequate coverage for critical paths.

**Step 4: Deprecated APIs and Patterns**
- Search for framework-specific deprecated patterns:
  - React: class components, componentWillMount, findDOMNode, defaultProps on function components.
  - Next.js: pages directory patterns when app router is available, getServerSideProps when server components exist.
  - Vue: Options API when Composition API is preferred, filters (removed in Vue 3).
- Search for deprecated Node.js APIs: `url.parse` (use URL constructor), `querystring` (use URLSearchParams).
- Check for deprecated CSS properties or vendor prefixes no longer needed.
- Identify outdated build configurations or tooling.

**Step 5: Security Issues**
- Search for potential security vulnerabilities:
  - SQL injection: raw query strings with variable interpolation.
  - XSS: `dangerouslySetInnerHTML`, `v-html`, unescaped user input in templates.
  - Hardcoded secrets: API keys, passwords, tokens in source code.
  - Missing input validation on API endpoints.
  - Missing CSRF protection on state-changing endpoints.
  - Insecure cookie settings (missing HttpOnly, Secure, SameSite).
  - Missing rate limiting on authentication endpoints.
- Rate each finding by severity: critical, high, medium, low.

**Step 6: Performance Issues**
- Look for performance anti-patterns:
  - N+1 database queries in loops.
  - Missing database indexes on frequently queried columns.
  - Large bundle sizes from improper code splitting or tree shaking.
  - Unoptimized images served without compression or resizing.
  - Missing memoization on expensive computations.
  - Unnecessary re-renders from missing React.memo, useMemo, useCallback.
  - Synchronous file I/O or blocking operations in request handlers.

**Step 7: Create Prioritized Remediation Plan**
- Categorize all findings into priority tiers:
  - **P0 - Immediate**: Security vulnerabilities and critical bugs.
  - **P1 - This sprint**: Deprecated APIs that will break on next upgrade, blocking tech debt.
  - **P2 - This quarter**: Code quality improvements, test coverage, moderate upgrades.
  - **P3 - Backlog**: Nice-to-have cleanups, minor code smells, cosmetic issues.
- For each item, provide: description, location (file paths), estimated effort (hours/days), impact, and suggested approach.
- Group related items into actionable work items that can be tackled together.
- Suggest a sustainable pace: allocate 15-20% of each sprint to tech debt reduction.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
