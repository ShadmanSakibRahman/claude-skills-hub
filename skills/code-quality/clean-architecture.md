---
description: Restructure code following clean architecture with entities, use cases, interface adapters, and proper dependency boundaries
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in clean architecture and software system design. Restructure codebases to enforce clear boundaries, dependency rules, and separation of concerns.

Follow these steps precisely:

1. **Assess Current Architecture**: Analyze the codebase structure:
   - Map out the current directory structure and module organization.
   - Identify where business logic, data access, UI, and infrastructure code live.
   - Find dependency violations (business logic importing framework-specific code).
   - Check for circular dependencies between modules.
   - Document the current architecture with a simple diagram.

2. **Define the Layer Structure**: Plan the clean architecture layers:
   - **Entities (Domain)**: Core business objects, value objects, domain events, business rules. Zero external dependencies.
   - **Use Cases (Application)**: Application-specific business logic, orchestration. Depends only on entities. Defines interfaces for outer layers.
   - **Interface Adapters (Adapters)**: Controllers, presenters, gateways, repositories. Converts data between use case format and external format.
   - **Frameworks & Drivers (Infrastructure)**: Database, web framework, external APIs, file system. The outermost layer.

3. **Enforce the Dependency Rule**: Inner layers must never know about outer layers:
   - Entities do not import from use cases, adapters, or infrastructure.
   - Use cases do not import from adapters or infrastructure (they define interfaces that adapters implement).
   - Adapters do not import from infrastructure (they define ports that infrastructure implements).
   - All dependencies point inward. Use dependency injection to invert control.

4. **Extract Entities**: Create the domain layer:
   - Identify core business objects and extract them into entity classes/types.
   - Move business rules and validations into entity methods.
   - Define value objects for concepts with equality by value (Money, Email, Address).
   - Define domain events for significant state changes.
   - This layer should be testable with zero mocking.

5. **Extract Use Cases**: Create the application layer:
   - Identify distinct operations (CreateOrder, AuthenticateUser, GenerateReport).
   - Each use case is a single class/function with one public method (execute/handle).
   - Define input/output DTOs (Data Transfer Objects) for each use case.
   - Define repository and service interfaces (ports) that use cases depend on.
   - Use cases orchestrate entities and call port interfaces.

6. **Create Adapters**: Implement the interface adapter layer:
   - **Controllers**: Receive HTTP/CLI/event input, convert to use case input DTO, call use case, convert output to response format.
   - **Repositories**: Implement repository interfaces defined by use cases. Handle ORM/SQL details.
   - **Presenters/Serializers**: Format use case output for the delivery mechanism (JSON, HTML, CLI).
   - **Gateways**: Implement external service interfaces (email, payment, storage).

7. **Configure Dependency Injection**: Wire everything together at the composition root:
   - Create a single place where concrete implementations are bound to interfaces.
   - Use constructor injection for all dependencies.
   - Framework DI container or manual wiring, depending on project needs.

8. **Restructure Directories**: Organize files by architectural layer:
   ```
   src/
     domain/         (entities, value objects, domain events)
     application/    (use cases, ports/interfaces, DTOs)
     adapters/       (controllers, repositories, presenters)
     infrastructure/ (database, framework config, external services)
   ```
   Or organize by feature, with layers within each feature.

9. **Validate Boundaries**: After restructuring:
   - Verify no dependency rule violations (inner layers importing from outer).
   - Run tests to confirm behavior is preserved.
   - Check that domain and use case layers can be tested without any infrastructure.

Apply clean architecture incrementally. Start with the most critical domain area. Not every project needs full clean architecture -- apply the right level of separation for the project's complexity.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
