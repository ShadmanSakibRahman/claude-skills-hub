---
description: Audit and fix naming conventions across the codebase applying language-specific standards for clarity and consistency
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in clean code naming practices. Audit naming across the codebase and apply language-specific conventions for maximum clarity and consistency.

Follow these steps precisely:

1. **Identify Language Conventions**: Determine the correct naming style:
   - **JavaScript/TypeScript**: camelCase for variables/functions, PascalCase for classes/components/types, UPPER_SNAKE_CASE for constants, camelCase for file names (or kebab-case).
   - **Python**: snake_case for variables/functions/modules, PascalCase for classes, UPPER_SNAKE_CASE for constants.
   - **Rust**: snake_case for variables/functions/modules, PascalCase for types/traits, UPPER_SNAKE_CASE for constants.
   - **Go**: camelCase/PascalCase (exported vs unexported), no underscores.
   - **CSS**: kebab-case for class names, custom properties.

2. **Audit Variable Names**: Find and flag:
   - Single-letter names outside of loop counters or lambdas (`x`, `d`, `t`).
   - Abbreviated names that sacrifice clarity (`usr`, `mgr`, `btn`, `cfg`).
   - Names that describe implementation instead of purpose (`list1`, `data2`, `temp`).
   - Boolean variables not phrased as questions (`active` should be `isActive`).
   - Negated booleans that cause double-negative confusion (`isNotDisabled`).

3. **Audit Function Names**: Check that functions:
   - Start with a verb describing the action (`get`, `create`, `calculate`, `validate`).
   - Describe what they return, not how they work.
   - Avoid generic names (`process`, `handle`, `manage`, `do`) without specificity.
   - Event handlers follow convention (`onClick`, `handleSubmit`).
   - Async functions indicate their async nature if conventions require it.

4. **Audit Class and Type Names**: Verify:
   - Classes use PascalCase nouns describing the entity (`UserRepository`, `PaymentService`).
   - Interfaces are named by capability, not prefixed with `I` (prefer `Readable` over `IReadable`, unless project convention differs).
   - Enums use PascalCase with PascalCase members (or UPPER_SNAKE_CASE members per language convention).
   - Generic type parameters are descriptive when meaning is not obvious (`TItem` not just `T` when multiple generics exist).

5. **Audit File and Directory Names**: Check:
   - Files match the primary export they contain.
   - Consistent file naming style across the project.
   - Directory names clearly describe their contents.
   - Test files follow naming convention (`*.test.ts`, `*_test.go`, `test_*.py`).

6. **Fix Inconsistencies**: For each naming issue:
   - Rename the identifier to follow conventions.
   - Update ALL references across the entire codebase (imports, usages, tests, documentation).
   - Use the IDE-safe rename approach: search globally before and after to ensure nothing was missed.
   - Prioritize public API names over internal names.

7. **Domain Language**: Ensure the codebase uses consistent domain terminology:
   - Create a glossary of domain terms if one does not exist.
   - Use the same word for the same concept everywhere (don't mix `user`/`account`/`member` for the same entity).
   - Match the domain language used by stakeholders.

8. **Document Conventions**: If the project lacks a naming guide, suggest creating one covering all the patterns established during the audit.

Rename carefully. Use grep to verify all references are updated. Be especially cautious with dynamically accessed names (string-based property access, reflection, serialization).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
