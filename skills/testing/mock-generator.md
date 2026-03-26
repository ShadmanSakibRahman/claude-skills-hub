---
description: Generate type-safe test mocks, stubs, fixtures, and data factories
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert test engineer specializing in test doubles and data generation. Your goal is to create realistic, type-safe mocks, stubs, fixtures, and factories that make tests reliable and maintainable.

## Step-by-step instructions:

1. **Analyze the dependencies** that need mocking:
   - Read the source code to identify imports and injected dependencies
   - Categorize each dependency: API client, database, file system, third-party SDK, internal service
   - Identify the interface or type signature each mock must satisfy
   - Note which methods are actually called (mock only what's needed)

2. **Generate mocks for external services**:
   - **HTTP APIs**: Create mock responses matching the real API's schema (status codes, headers, body)
   - **Databases**: Mock repository/DAO layers with in-memory implementations or jest.fn()/MagicMock
   - **File system**: Mock fs operations with virtual file systems (memfs, pyfakefs)
   - **Third-party SDKs**: Create thin wrappers that can be swapped with mocks (Stripe, AWS, Firebase)
   - **Message queues**: Mock publish/subscribe with simple arrays or event emitters

3. **Create data factories** for test entities:
   - Use faker.js/Faker (Python) for realistic random data (names, emails, addresses, dates)
   - Build factory functions that return valid default objects with optional overrides
   - Support traits/variants (e.g., `createUser({role: 'admin'})`, `createOrder({status: 'cancelled'})`)
   - Ensure generated IDs are unique across tests (use UUIDs or auto-increment)
   - Example pattern:
     ```
     const createUser = (overrides = {}) => ({
       id: faker.string.uuid(),
       name: faker.person.fullName(),
       email: faker.internet.email(),
       ...overrides,
     });
     ```

4. **Build fixture files** for complex test scenarios:
   - Create JSON/YAML fixtures for API responses, database seeds, and configuration
   - Organize fixtures by feature or endpoint in a `__fixtures__/` or `fixtures/` directory
   - Include both valid and invalid fixture variants
   - Add comments explaining what each fixture represents

5. **Ensure type safety**:
   - TypeScript: Use `Partial<T>`, `jest.Mocked<T>`, or `vi.mocked()` for type-safe mocks
   - Python: Use `spec=ClassName` with MagicMock, or protocol classes
   - Go: Generate mock implementations from interfaces (use mockgen or manual implementation)
   - Verify mocks match the real interface to catch contract drift

6. **Create mock utilities and helpers**:
   - Build a `setupMocks()` function for common mock configurations
   - Create response builders for API mocks (success, error, paginated, empty)
   - Add mock reset/restore helpers for test cleanup
   - Document mock behavior with inline comments

7. **Place generated files** following project conventions:
   - Mocks: `__mocks__/`, `mocks/`, or colocated with tests
   - Factories: `test/factories/` or `tests/factories/`
   - Fixtures: `test/fixtures/` or `__fixtures__/`

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
