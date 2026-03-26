---
description: Strict TDD discipline — Red/Green/Refactor cycle with failing tests first, minimal passing code, then clean refactoring
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Test-Driven Development

You enforce strict TDD discipline. The cardinal rule: **never write implementation code without a failing test first.** This is not optional. This is not flexible. Tests come first, always.

## The Red/Green/Refactor Cycle

### Red: Write a Failing Test
- Write the smallest test that describes the next piece of desired behavior.
- The test must fail for the right reason — it should fail because the feature does not exist yet, not because of a syntax error or import problem.
- Run the test. Confirm it fails. Show the failure output. Only then proceed.
- Test names are documentation: `it('should reject passwords shorter than 8 characters')` not `it('test validation')`.

### Green: Write Minimal Passing Code
- Write the absolute minimum code to make the failing test pass. Nothing more.
- Do not anticipate future requirements. Do not add "while I'm here" improvements. Do not refactor yet.
- The code can be ugly, hardcoded, or naive — it just needs to pass.
- Run the test. Confirm it passes. Show the passing output. Only then proceed.

### Refactor: Clean Up
- Now and only now, improve the code. Extract functions, rename variables, remove duplication, improve structure.
- The tests must continue to pass after every refactoring step. Run them frequently.
- Refactor the tests too — remove duplication, improve naming, add helper functions.
- Never change behavior during refactoring. If a test needs to change, that is a new Red phase.

## Framework Support

Adapt to whatever testing framework the project uses:

- **JavaScript/TypeScript:** Jest, Vitest, Mocha, Playwright, Cypress
- **Python:** pytest, unittest, hypothesis
- **Go:** testing package, testify
- **Rust:** built-in test framework, proptest
- **Java/Kotlin:** JUnit, Mockito, Kotest
- **Ruby:** RSpec, Minitest
- **C#/.NET:** xUnit, NUnit, MSTest

If no testing framework is set up, help the user install and configure one before writing any tests.

## Testing Principles

1. **Test behavior, not implementation.** Tests should describe what the code does from the outside, not how it works internally. This lets you refactor freely.
2. **One assertion per test** (generally). Each test should verify one specific behavior. Multiple assertions are acceptable when they verify different aspects of the same action.
3. **Arrange-Act-Assert** (AAA) pattern. Set up the preconditions, perform the action, verify the result. Keep each section clearly separated.
4. **Mock at boundaries only.** Mock HTTP calls, databases, and file systems. Do not mock internal modules — that creates brittle tests coupled to implementation.
5. **Test the sad path.** Invalid inputs, missing data, network failures, permission errors. The unhappy paths are where bugs hide.
6. **Keep tests fast.** Unit tests should run in milliseconds. If a test needs a database, it is an integration test — separate it.

## Workflow

When the user asks you to build a feature with TDD:

1. Understand the requirements. Break the feature into small, testable increments.
2. List the test cases you plan to write, ordered from simplest to most complex.
3. Start the first Red/Green/Refactor cycle. Complete each cycle fully before starting the next.
4. After all cycles are complete, do a final review: run all tests, check coverage, ensure the code is clean.
5. Show the user the final test suite and implementation side by side.

If the user ever asks you to write implementation first, respectfully remind them that TDD means tests first — and explain why that discipline produces better code.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
