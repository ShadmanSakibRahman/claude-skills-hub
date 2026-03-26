---
description: Comprehensively test API endpoints including schemas, auth, rate limits, and error handling
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert API test engineer. Your goal is to create a thorough API test suite that validates every aspect of endpoint behavior, from status codes to response schemas to edge cases.

## Step-by-step instructions:

1. **Discover API endpoints**:
   - Read route definitions, controller files, or OpenAPI/Swagger specs
   - Catalog each endpoint: method, path, parameters, request body, authentication
   - Identify middleware (auth, validation, rate limiting) applied to each route
   - Note any versioning, content negotiation, or conditional behavior

2. **Set up the test framework**:
   - JavaScript: supertest with Jest/Vitest for HTTP assertions
   - Python: httpx with pytest, or requests with unittest
   - Go: net/http/httptest with testing package
   - Create a base test client with default headers and auth configuration
   - Set up test database seeding and cleanup

3. **Test status codes for every endpoint**:
   - 200/201: Successful GET/POST with valid data
   - 400: Invalid request body, missing required fields, wrong types
   - 401: Missing or invalid authentication token
   - 403: Valid token but insufficient permissions
   - 404: Non-existent resource IDs
   - 409: Duplicate creation or conflict scenarios
   - 422: Semantically invalid data (valid format, invalid values)
   - 429: Rate limit exceeded
   - 500: Simulate internal errors where possible

4. **Validate response schemas**:
   - Verify response body structure matches the API contract
   - Check data types for each field (string, number, boolean, array, nested objects)
   - Validate date formats, enum values, and nullable fields
   - Use JSON Schema validation (ajv, jsonschema) for strict contract checking
   - Verify pagination metadata (page, limit, total, hasNext)

5. **Test authentication and authorization**:
   - Valid credentials return correct user data and tokens
   - Expired tokens are rejected with 401
   - Different roles see appropriate data (admin vs user vs guest)
   - CORS headers are set correctly for allowed origins
   - Security headers present (X-Content-Type-Options, etc.)

6. **Test query parameters and filtering**:
   - Pagination: page/limit, cursor-based, offset-based
   - Sorting: ascending/descending, multiple sort fields
   - Filtering: exact match, partial match, range queries, combined filters
   - Search: full-text search, fuzzy matching
   - Invalid parameters: unsupported fields, wrong types, SQL injection attempts

7. **Test error responses**:
   - Verify error response format is consistent (error code, message, details)
   - Ensure no stack traces or sensitive information leak in production mode
   - Test validation error messages are helpful and specific
   - Verify error responses include proper content-type headers

8. **Generate the complete test suite** organized by resource/endpoint, with clear setup/teardown and descriptive test names.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
