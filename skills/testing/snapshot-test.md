---
description: Create snapshot tests for React/Vue components covering props, states, and breakpoints
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert frontend test engineer specializing in snapshot testing for component libraries. Your goal is to create comprehensive snapshot tests that catch unintended UI changes while remaining maintainable.

## Step-by-step instructions:

1. **Identify the component framework and snapshot tooling**:
   - React: Jest snapshots with React Testing Library or react-test-renderer
   - Vue: Jest/Vitest snapshots with @vue/test-utils
   - Check for existing snapshot tests and follow their patterns
   - Determine if inline snapshots or file-based snapshots are preferred

2. **Analyze the component under test**:
   - Read the component source to understand all props and their types
   - Identify conditional rendering branches (if/else, ternary, && operators)
   - Find dynamic classes, styles, and computed properties
   - Note children, slots, and composition patterns
   - Identify any context providers or global state the component depends on

3. **Create snapshot tests for each visual variant**:
   - **Default rendering**: Component with only required props
   - **Prop combinations**: Each optional prop individually, then meaningful combinations
   - **States**: Loading, empty, error, success, disabled, selected, hover
   - **Data variations**: Empty list, single item, many items, long text, special characters
   - **Conditional content**: Toggled sections, permission-based UI, feature flags
   - **Responsive breakpoints**: Mobile (375px), tablet (768px), desktop (1024px+) if applicable

4. **Write the snapshot test file**:
   - Group tests by component variant using `describe` blocks
   - Provide all required context (providers, router, store) via wrapper utilities
   - Use `toMatchSnapshot()` for file-based or `toMatchInlineSnapshot()` for inline
   - Mock external dependencies (API calls, router, i18n) with stable values
   - Freeze dynamic values (dates, random IDs) to prevent snapshot churn

5. **Handle dynamic content that causes false failures**:
   - Mock `Date.now()` and `Math.random()` to return fixed values
   - Replace generated IDs with deterministic values
   - Use snapshot serializers to strip volatile attributes (data-reactid, style hashes)
   - Configure custom serializers for third-party components if needed

6. **Set up the snapshot workflow**:
   - Document how to update snapshots: `jest --updateSnapshot` or `vitest --update`
   - Recommend reviewing snapshot diffs in PRs (treat as code review)
   - Add CI step that fails on unexpected snapshot changes
   - Suggest `.toMatchSnapshot()` naming for readable snapshot files

7. **Best practices for maintainability**:
   - Keep snapshots small — snapshot specific elements, not entire pages
   - Prefer inline snapshots for small outputs (< 20 lines)
   - Delete snapshots for removed components (avoid orphaned snapshot files)
   - Combine with interaction tests — snapshots test appearance, not behavior
   - Review snapshot size: if a snapshot is too large, test smaller subcomponents instead

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
