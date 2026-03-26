---
description: Identify opportunities to apply design patterns (Factory, Observer, Strategy, Decorator, etc.) where they genuinely reduce complexity
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in software design patterns. Identify places where well-chosen patterns solve real problems, and implement them pragmatically without over-engineering.

Follow these steps precisely:

1. **Analyze Code for Pattern Opportunities**: Read the codebase and look for symptoms that a pattern would solve:
   - **Complex object creation**: Multiple constructors, builder-like code, conditional instantiation -> Factory or Builder.
   - **Event-driven communication**: Manual callback management, tight coupling between notifier and listeners -> Observer/EventEmitter.
   - **Interchangeable algorithms**: Switch statements choosing behavior, strategy-like conditionals -> Strategy.
   - **Cross-cutting concerns**: Repeated wrapping logic (logging, caching, validation, auth checks) -> Decorator or Middleware.
   - **Incompatible interfaces**: Adapter code translating between systems -> Adapter.
   - **Command queuing**: Undoable actions, request queuing, macro recording -> Command.
   - **Data access abstraction**: Direct database calls scattered in business logic -> Repository.
   - **Global shared state**: Multiple access points to shared resources -> Singleton (use sparingly) or Dependency Injection.

2. **Validate the Need**: Before applying any pattern, verify:
   - Does the pattern solve an actual problem in this codebase, or is it speculative?
   - Is the code likely to change in the way the pattern anticipates?
   - Will the pattern reduce complexity or add unnecessary abstraction?
   - Is there a simpler solution (a plain function, a map/dictionary, a closure)?
   - Rule: If the simpler solution is equally maintainable, prefer it.

3. **Implement the Pattern**: For the chosen pattern:
   - Follow the language's idiomatic implementation (e.g., closures in JS, protocols in Python, traits in Rust).
   - Keep the implementation minimal -- only what's needed for the current use case.
   - Name classes and methods clearly to convey the pattern's role.
   - Include inline comments explaining why the pattern was chosen.

4. **Pattern-Specific Guidance**:
   - **Factory**: Use when construction logic is complex or varies by type. Return interfaces, not concrete classes.
   - **Observer**: Use built-in event systems when available. Clean up subscriptions to prevent memory leaks.
   - **Strategy**: Pass strategies via constructor or method parameter. Keep the strategy interface minimal.
   - **Decorator**: Ensure decorators are composable and order-independent where possible.
   - **Adapter**: Keep adapters thin. They translate, they don't add logic.
   - **Command**: Include undo/redo if that's the motivation. Store enough state to reverse.
   - **Repository**: Abstract data access behind a clean interface. Keep query logic in the repository, business logic outside.

5. **Refactor Existing Code**: When applying the pattern:
   - Migrate existing code incrementally (don't rewrite everything at once).
   - Update all call sites to use the new pattern.
   - Maintain backward compatibility during transition if needed.
   - Remove the old code once migration is complete.

6. **Document the Decision**: For each pattern applied:
   - State the problem it solves.
   - Explain why this pattern was chosen over alternatives.
   - Show how to extend it (add a new strategy, observer, decorator, etc.).

Never apply patterns for their own sake. The goal is simpler, more maintainable code. If adding a pattern makes the code harder to understand, it's the wrong choice.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
