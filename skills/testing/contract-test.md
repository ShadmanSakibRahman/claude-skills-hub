---
description: Create consumer-driven contract tests using Pact to verify API compatibility
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in consumer-driven contract testing. Your goal is to set up and maintain contract tests that ensure API providers and consumers remain compatible as they evolve independently.

## Step-by-step instructions:

1. **Assess the architecture and identify contracts**:
   - Map out service-to-service communication (REST, GraphQL, messaging)
   - Identify consumer services (frontends, downstream APIs) and provider services (backends, upstream APIs)
   - Determine which interactions are most critical and fragile
   - Choose the contract testing tool: Pact (most popular), Spring Cloud Contract, or custom schema validation

2. **Set up Pact (or chosen tool)**:
   - Install dependencies: `@pact-foundation/pact` (JS), `pact-python`, `pact-go`
   - Configure the Pact broker URL (or use Pactflow for hosted)
   - Set up provider and consumer names following a consistent naming convention
   - Configure logging and output directories for pact files

3. **Write consumer-side contract tests**:
   - Define the expected interactions from the consumer's perspective
   - For each API call the consumer makes, specify:
     - Request: method, path, headers, query parameters, body
     - Response: expected status code, headers, and body structure
   - Use matchers for flexible matching (type-based, regex, array length)
   - Do NOT hardcode exact values — use `like()`, `eachLike()`, `term()` matchers
   - Generate the pact file by running consumer tests

4. **Write provider-side verification tests**:
   - Load the pact file(s) from the broker or local directory
   - Set up provider states (e.g., "a user with ID 123 exists") with state handlers
   - Configure the provider base URL and authentication
   - Run verification against the actual provider service
   - Handle provider states by seeding test data in setup hooks

5. **Define contracts for different scenarios**:
   - Happy path: Standard request/response for each endpoint
   - Error cases: 404 for missing resources, 400 for invalid input, 401 for unauthorized
   - Edge cases: Empty lists, paginated responses, nullable fields
   - Different consumer roles: Admin vs regular user responses

6. **Integrate into CI/CD pipeline**:
   - Consumer pipeline: Run consumer tests, publish pact to broker, trigger provider verification
   - Provider pipeline: Verify pacts from all consumers, publish verification results
   - Use "can I deploy" checks before deploying either consumer or provider
   - Set up webhooks to notify providers when new pacts are published

7. **Maintain contracts over time**:
   - Use pact broker tags or branches for environment tracking (dev, staging, prod)
   - Handle breaking changes by versioning contracts
   - Remove contracts for decommissioned consumers
   - Review pending pacts and work with consumer teams to resolve failures
   - Document contract ownership and escalation paths

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
