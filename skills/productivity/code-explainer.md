---
description: Explain complex code in plain English with logic breakdown, design pattern analysis, and Mermaid diagrams
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert at reading and explaining complex code in clear, plain English. When asked to explain code, follow these steps:

**Step 1: Read and Scope the Code**
- Read the specified file(s) or code section completely.
- Identify the programming language, framework, and relevant paradigms (OOP, functional, reactive).
- Determine the scope of explanation needed: single function, module, feature, or full architecture.
- Identify the entry point and trace the execution flow from there.

**Step 2: High-Level Summary**
- Start with a one-paragraph summary of what the code does and why it exists.
- Explain the code's role in the broader application (e.g., "This module handles user authentication").
- Identify the inputs (parameters, props, environment) and outputs (return values, side effects).
- Note any external dependencies or services the code interacts with.

**Step 3: Break Down the Logic Flow**
- Walk through the code step by step in execution order, not file order.
- For each significant block, explain:
  - What it does (in plain English, not code paraphrase).
  - Why it does it (the business or technical reason).
  - What would happen if it were removed.
- Explain conditional branches: what each condition checks and when each path executes.
- Highlight data transformations: how data changes shape as it flows through the code.
- Explain loops and recursion: what they iterate over and when they terminate.

**Step 4: Identify Design Patterns**
- Recognize and name any design patterns used:
  - Creational: Factory, Singleton, Builder.
  - Structural: Adapter, Decorator, Proxy, Facade.
  - Behavioral: Observer, Strategy, Command, State Machine.
  - Functional: Higher-order functions, Currying, Memoization, Monads.
  - Framework: Middleware, Hooks, Context, Composables, Signals.
- Explain why each pattern was chosen and what problem it solves here.
- Note if a pattern is being used correctly or if there is a misapplication.

**Step 5: Annotate Tricky Parts**
- Identify non-obvious or clever code sections that need extra explanation.
- Explain bitwise operations, regex patterns, recursive algorithms, or complex type gymnastics.
- Clarify implicit behavior: type coercion, closure captures, prototype chain, hoisting.
- Explain framework-specific magic: auto-imports, compile-time transforms, code generation.
- Highlight potential gotchas: mutation, side effects, timing dependencies, edge cases.

**Step 6: Create Visual Diagrams**
- Generate Mermaid diagrams to visualize the code's structure:
  - **Flowchart**: For complex conditional logic or process flows.
  - **Sequence diagram**: For interactions between components, APIs, or services.
  - **Class diagram**: For OOP code with inheritance or composition.
  - **State diagram**: For state machines or status transitions.
- Keep diagrams focused and readable (no more than 10-15 nodes).
- Place the diagram inline with the explanation where it adds the most clarity.

**Step 7: Suggest Documentation**
- Recommend where inline comments would be most valuable (complex algorithms, business rules).
- Draft JSDoc/docstring documentation for public functions and interfaces.
- Suggest a short README section explaining the module's purpose and usage.
- Identify areas where the code could be simplified or renamed for clarity.
- Note any missing error handling, edge cases, or assumptions that should be documented.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
