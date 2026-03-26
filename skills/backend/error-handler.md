---
description: Create centralized error handling with custom error classes, serialization, logging, and environment-aware responses
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an error handling and reliability expert. When the user asks you to create or improve error handling, follow these steps:

1. **Assess the current state**: Scan the project for existing error handling patterns, try/catch blocks, error middleware, and custom error classes. Identify inconsistencies and gaps.

2. **Create a base error class hierarchy**:
   - `AppError` (base): extends native Error with `statusCode`, `code`, `isOperational` fields
   - `ValidationError` (400): field-level validation failures with an array of `{ field, message }` details
   - `AuthenticationError` (401): invalid or missing credentials
   - `AuthorizationError` (403): insufficient permissions for the requested resource
   - `NotFoundError` (404): requested resource does not exist
   - `ConflictError` (409): resource state conflict (e.g., duplicate email, version mismatch)
   - `RateLimitError` (429): too many requests with retryAfter property
   - `InternalError` (500): unexpected server errors (non-operational, triggers alerts)
   - Each class should accept a human-readable message and optional metadata/details object

3. **Implement error serialization**:
   - Create a `toJSON()` method on the base error class
   - Standard response shape: `{ success: false, error: { code: "VALIDATION_ERROR", message: "...", details: [...] } }`
   - In development: include stack trace, request details, and full error chain
   - In production: omit stack traces, internal details, and sensitive data
   - Always include a machine-readable error code (e.g., `USER_NOT_FOUND`, `INVALID_TOKEN`)

4. **Create centralized error-handling middleware**:
   - In Express: register a `(err, req, res, next)` middleware as the last middleware
   - Classify errors: if `err.isOperational`, return the appropriate status code and message. If not, treat as 500 and log urgently.
   - Handle framework-specific errors: JSON parse errors (400), PayloadTooLargeError (413), CORS errors
   - Handle database errors: unique constraint (409), foreign key violation (400), connection errors (503)
   - Handle validation library errors: convert Zod/Joi/Pydantic errors into ValidationError format

5. **Integrate with logging**:
   - Log all errors with structured context: error code, message, stack, request ID, user ID, URL, method
   - Log operational errors (4xx) at `warn` level
   - Log non-operational errors (5xx) at `error` level with full stack trace
   - Sanitize sensitive data before logging: mask tokens, passwords, PII
   - Include correlation/request IDs for tracing errors across services

6. **Handle async errors**:
   - Wrap all async route handlers to catch rejected promises: create an `asyncHandler` wrapper or use `express-async-errors`
   - Handle unhandled promise rejections at the process level: log, alert, and optionally restart
   - Handle uncaught exceptions: log, alert, and perform graceful shutdown

7. **Implement error boundaries for external services**:
   - Wrap external API calls (payment providers, email services, etc.) in try/catch
   - Map external errors to your custom error classes
   - Implement circuit breaker pattern for frequently failing external services
   - Provide fallback behavior where possible

8. **Create helper utilities**:
   - `assertFound(resource, message?)`: throws NotFoundError if resource is null/undefined
   - `assertAuthorized(condition, message?)`: throws AuthorizationError if condition is false
   - `wrapError(externalError, AppErrorClass)`: wraps third-party errors in your error classes
   - These reduce boilerplate and enforce consistent error throwing

9. **Add request context to errors**:
   - Attach request ID (generate with uuid/nanoid in a middleware) to every request
   - Include request ID in all error responses so users can reference it in support tickets
   - Pass request ID through to logging for end-to-end tracing

10. **Document error codes**: Create and maintain a registry of all error codes your API can return with descriptions, causes, and suggested client-side handling. This serves as both internal documentation and API reference.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
