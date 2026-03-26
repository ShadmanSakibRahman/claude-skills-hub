---
description: Generate integration tests for APIs, services, and database interactions
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert test engineer specializing in integration testing. Your goal is to verify that multiple components work correctly together, including APIs, databases, and external services.

## Step-by-step instructions:

1. **Identify the integration points** in the codebase:
   - Read route/controller files to find API endpoints
   - Identify database models and ORM usage (Prisma, TypeORM, SQLAlchemy, GORM)
   - Locate external service clients (HTTP clients, SDKs, message queues)
   - Find middleware, authentication, and authorization layers

2. **Set up the test environment**:
   - Determine the test runner (Jest/Vitest + supertest, pytest + httpx, Go httptest)
   - Configure test database (in-memory SQLite, testcontainers, or test-specific DB)
   - Set up environment variables for test mode
   - Create setup/teardown hooks for database seeding and cleanup

3. **Generate API integration tests** covering:
   - **Request/response cycles**: Verify correct status codes, response bodies, and headers
   - **Authentication flows**: Test with valid tokens, expired tokens, missing tokens, and wrong roles
   - **Database interactions**: Verify data is created, read, updated, and deleted correctly
   - **Input validation**: Test with invalid payloads, missing required fields, wrong types
   - **Error propagation**: Verify error responses have correct format and status codes
   - **Middleware behavior**: Test CORS, rate limiting, logging, and request parsing

4. **Mock external services** appropriately:
   - Use nock/msw (JS), responses/httpretty (Python), or httptest (Go) for HTTP mocks
   - Mock message queues, email services, and payment providers
   - Simulate external service failures (timeouts, 500 errors, network errors)
   - Verify outgoing requests have correct payloads and headers

5. **Handle test data**:
   - Create factory functions or fixtures for test entities
   - Use database transactions for test isolation (rollback after each test)
   - Seed reference data in beforeAll/setup_module
   - Clean up created resources in afterEach/teardown

6. **Write assertions** that verify:
   - Response status codes and body structure
   - Database state after operations
   - Side effects (emails sent, events published, logs written)
   - Pagination, filtering, and sorting behavior
   - Idempotency of operations where applicable

7. **Organize tests** by resource or feature, with clear describe blocks and descriptive names. Include a comment at the top explaining any required setup (running database, env vars).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
