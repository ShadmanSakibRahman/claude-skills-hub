---
description: Reduce cyclomatic complexity by refactoring nested conditionals, long functions, and complex boolean expressions using proven patterns
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in code simplification and complexity reduction. Identify overly complex code and refactor it into clear, maintainable structures.

Follow these steps precisely:

1. **Measure Complexity**: Identify high-complexity code:
   - Find functions with deep nesting (3+ levels of if/for/while).
   - Find long functions (30+ lines of logic).
   - Find complex boolean expressions (3+ conditions combined with AND/OR).
   - Find switch/case statements with many branches (5+).
   - Find functions with many parameters (4+).
   - Rank findings by severity for prioritized refactoring.

2. **Apply Early Returns / Guard Clauses**: Flatten nested conditionals:
   - Convert `if (condition) { ...long block... }` to `if (!condition) return;` at the top.
   - Handle error cases and edge cases first, then proceed with the happy path.
   - Each guard clause should handle one specific condition.
   - This reduces nesting by one level per guard clause applied.

3. **Decompose Complex Conditionals**: Break down boolean expressions:
   - Extract complex conditions into well-named boolean variables or functions.
   - `if (user.age >= 18 && user.verified && !user.banned)` becomes `if (isEligibleUser(user))`.
   - Name by business intent, not implementation: `isEligible` not `isOldEnoughAndVerifiedAndNotBanned`.

4. **Extract Methods**: Break long functions into focused sub-functions:
   - Each function should do one thing at one level of abstraction.
   - Name extracted functions by their purpose (what, not how).
   - Keep extracted functions near their caller or in a logical module.
   - Pass only the data each function needs (not entire objects if only one field is used).

5. **Replace Conditionals with Data Structures**:
   - Convert switch/if-else chains to lookup objects/maps: `const handlers = { 'admin': handleAdmin, 'user': handleUser }`.
   - Use strategy pattern for complex behavioral branching.
   - Use polymorphism when different types need different behavior.
   - Use configuration objects instead of parameter-based branching.

6. **Simplify Loops**:
   - Replace manual loops with higher-order functions (map, filter, reduce).
   - Extract loop bodies into named functions.
   - Use early continue/break instead of nested conditions inside loops.
   - Consider splitting loops that do multiple unrelated things.

7. **Reduce Function Parameters**:
   - Group related parameters into an options/config object.
   - Use builder pattern for complex construction.
   - Apply partial application or currying where appropriate.
   - Consider whether many parameters indicate the function does too much.

8. **Validate Results**: After refactoring:
   - Confirm behavior is preserved (tests pass).
   - Verify nesting depth decreased.
   - Check that each function fits on one screen (~25 lines).
   - Ensure the code reads like a narrative from top to bottom.

Focus on the highest-complexity functions first. Aim for a maximum cyclomatic complexity of 10 per function. Make incremental changes, verifying after each step.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
