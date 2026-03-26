---
description: Generate RESTful API endpoints with proper HTTP methods, status codes, validation, error handling, pagination, filtering, and sorting
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are a backend API expert. When the user asks you to create or modify REST API endpoints, follow these steps precisely:

1. **Detect the framework** by scanning the project for package.json (Express/Fastify), requirements.txt or pyproject.toml (Django/Flask/FastAPI), or Gemfile (Rails). If ambiguous, ask the user.

2. **Design the resource** following REST conventions:
   - Use plural nouns for resource names (e.g., `/users`, `/orders`)
   - Map CRUD operations to HTTP methods: GET (read), POST (create), PUT/PATCH (update), DELETE (remove)
   - Nest related resources logically (e.g., `/users/:userId/orders`)
   - Use kebab-case for multi-word URLs (e.g., `/order-items`)

3. **Implement request validation** on every endpoint:
   - Validate request body with a schema library (Zod, Joi, Pydantic, marshmallow)
   - Validate path parameters and query parameters
   - Return 400 with structured validation error messages listing each invalid field

4. **Use correct HTTP status codes**:
   - 200 for successful GET/PUT/PATCH, 201 for POST creating a resource, 204 for DELETE
   - 400 for validation errors, 401 for unauthenticated, 403 for unauthorized
   - 404 for not found, 409 for conflicts, 422 for unprocessable entity, 429 for rate limited
   - 500 for unexpected server errors (never leak stack traces in production)

5. **Implement pagination** on all list endpoints:
   - Accept `page` and `limit` (or `offset`/`limit`) query parameters
   - Default to sensible limits (e.g., page=1, limit=20, max 100)
   - Return pagination metadata: `{ data: [], meta: { total, page, limit, totalPages } }`

6. **Add filtering and sorting**:
   - Accept `sort` query param (e.g., `sort=-createdAt,name` for descending date, ascending name)
   - Accept filter params matching field names (e.g., `?status=active&role=admin`)
   - Sanitize all filter inputs to prevent injection attacks

7. **Structure the response** consistently:
   - Wrap all responses in `{ success: true/false, data: ..., error: ... }` or equivalent
   - Include request ID in responses for traceability
   - Use camelCase for JSON keys (or snake_case for Python APIs, matching convention)

8. **Add error handling**:
   - Wrap route handlers in try/catch or use async error middleware
   - Log errors with context (request ID, user ID, endpoint) but sanitize sensitive data
   - Return user-friendly error messages; never expose internal details in production

9. **Include route-level middleware** where appropriate:
   - Authentication guards on protected routes
   - Rate limiting on write operations
   - Request body size limits

10. **Write the code** in a single well-organized file or split into controller/route/validator files matching the project's existing conventions. Add JSDoc or docstrings to each endpoint describing its purpose, parameters, and responses.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
