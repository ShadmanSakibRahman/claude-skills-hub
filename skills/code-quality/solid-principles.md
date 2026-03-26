---
description: Refactor code to follow SOLID principles by identifying and fixing SRP, OCP, LSP, ISP, and DIP violations with concrete changes
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in object-oriented design and SOLID principles. Identify violations and provide concrete refactorings that improve code architecture.

Follow these steps precisely:

1. **Single Responsibility Principle (SRP)**: Find classes/modules that have multiple reasons to change:
   - Identify classes that mix concerns (e.g., business logic + data access + formatting).
   - Look for God classes with too many methods or dependencies.
   - Check for functions that both compute values and produce side effects.
   - **Fix**: Extract each responsibility into its own class/module. A class should have one job.
   - Example: Split `UserService` that handles auth, profile updates, and email sending into `AuthService`, `UserProfileService`, and `EmailService`.

2. **Open/Closed Principle (OCP)**: Find code that requires modification for extension:
   - Identify switch/if-else chains that grow when new types are added.
   - Look for functions with type-checking conditionals (`if (type === 'A') ... else if (type === 'B')`).
   - **Fix**: Use polymorphism, strategy pattern, or plugin architecture. New behavior should be addable without modifying existing code.
   - Example: Replace a payment processing switch statement with a `PaymentProcessor` interface and concrete implementations.

3. **Liskov Substitution Principle (LSP)**: Find subclass violations:
   - Subclasses that throw exceptions for inherited methods they don't support.
   - Subclasses that ignore or override parent behavior in incompatible ways.
   - Methods that check the concrete type of their parameters.
   - **Fix**: Redesign the hierarchy. Use composition over inheritance. Ensure subtypes are fully substitutable for their base types.
   - Example: If `ReadOnlyRepository` extends `Repository` but throws on `save()`, create separate `Readable` and `Writable` interfaces instead.

4. **Interface Segregation Principle (ISP)**: Find fat interfaces:
   - Interfaces or abstract classes with methods that some implementors don't need.
   - Classes forced to implement stub methods or throw `NotImplementedError`.
   - **Fix**: Split large interfaces into smaller, focused ones. Clients should depend only on methods they use.
   - Example: Split `IWorker` (with `work()`, `eat()`, `sleep()`) into `IWorkable`, `IFeedable`, and `IRestable`.

5. **Dependency Inversion Principle (DIP)**: Find high-level modules depending on low-level details:
   - Classes that directly instantiate their dependencies (`new DatabaseClient()` inside a service).
   - Import of concrete implementations in business logic layers.
   - Hard-coded infrastructure details (file paths, URLs, database drivers) in domain code.
   - **Fix**: Depend on abstractions (interfaces/abstract classes). Inject dependencies through constructors or factory functions.
   - Example: `OrderService` should receive an `IOrderRepository` interface, not import `PostgresOrderRepository` directly.

6. **Prioritize Fixes**: Rank violations by impact:
   - Critical: Violations causing bugs or preventing testing.
   - High: Violations making the code hard to extend or maintain.
   - Medium: Violations that increase coupling unnecessarily.
   - Low: Minor structural improvements.

7. **Implement Changes**: For each fix:
   - Show the current violation clearly.
   - Provide the refactored code with new interfaces, classes, or modules.
   - Update all affected files (callers, tests, dependency injection config).
   - Ensure tests still pass or write new tests for the refactored structure.

Apply SOLID pragmatically. Not every class needs an interface. Focus on boundaries where flexibility and testability matter most.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
