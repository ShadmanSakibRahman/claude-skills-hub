---
description: Implement API versioning via URL path, headers, or query params with version routing, deprecation warnings, and backward compatibility
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an API versioning and evolution expert. When the user asks you to implement or improve API versioning, follow these steps:

1. **Choose the versioning strategy** based on the project's needs:
   - **URL Path** (`/v1/users`, `/v2/users`): Most common and explicit. Easy to route, cache, and document. Recommended for public APIs.
   - **Header-based** (`Accept: application/vnd.api+json;version=2` or `Accept-Version: 2`): Cleaner URLs, follows content negotiation principles. Better for internal APIs.
   - **Query parameter** (`/users?version=2`): Simple but less RESTful. Acceptable for quick implementations.
   - If no preference, default to URL path versioning as it is the most widely understood.

2. **Set up version routing**:
   - **URL path**: Create versioned route groups: `app.use('/v1', v1Router)`, `app.use('/v2', v2Router)`
   - **Header-based**: Create middleware that reads the version header and routes to the appropriate handler. Default to the latest stable version if no header is provided.
   - **Query param**: Extract version from query string in middleware; route accordingly
   - Always define a default version for requests that don't specify one
   - Return the active API version in response headers: `X-API-Version: 2`

3. **Organize versioned code**:
   - Option A (route-level): Separate route files per version (`routes/v1/users.js`, `routes/v2/users.js`). Share unchanged endpoints by re-exporting from the previous version.
   - Option B (controller-level): Version controllers but share routes. Controllers call versioned service methods.
   - Option C (transformer-level): Single set of handlers; use request/response transformers per version to reshape data.
   - Choose based on scope of changes: small differences favor transformers; large differences favor separate routes.

4. **Implement backward compatibility**:
   - New versions MUST support all data created by previous versions
   - Adding new fields to responses is non-breaking -- safe without a version bump
   - Removing or renaming fields, changing types, or altering behavior IS breaking -- requires a new version
   - Use feature flags or adapters to handle version-specific logic within shared code
   - Write compatibility tests that send v1 requests to v2 endpoints to verify they still work

5. **Handle deprecation gracefully**:
   - Add `Deprecation` header to responses from deprecated versions: `Deprecation: true` with `Link` header pointing to migration docs
   - Add `Sunset` header with the retirement date: `Sunset: Sat, 01 Jun 2026 00:00:00 GMT`
   - Log usage of deprecated endpoints with client identifier for targeted outreach
   - Return a warning in response body: `{ "warnings": [{ "code": "DEPRECATED_API", "message": "v1 is deprecated. Migrate to v2 by 2026-06-01." }] }`

6. **Create version migration guides**:
   - Document every breaking change between versions with before/after examples
   - Provide a changelog per version: new endpoints, changed endpoints, removed endpoints
   - Include code snippets for common migration scenarios
   - Create a migration endpoint or tool that validates client requests against the new version

7. **Implement version negotiation middleware**:
   - Parse the requested version from the chosen strategy (URL, header, query)
   - Validate the version exists and is not retired
   - For retired versions: return 410 Gone with migration guidance
   - For unknown versions: return 400 Bad Request with available versions listed
   - Attach the resolved version to the request context for use in handlers

8. **Handle API version lifecycle**:
   - **Active**: Fully supported, receives bug fixes and security patches
   - **Deprecated**: Still functional, returns deprecation warnings, no new features
   - **Retired**: Returns 410 Gone, no longer processes requests
   - Support at least N-1 versions (current + one previous) at all times
   - Announce deprecation at least 6 months before retirement for public APIs

9. **Version your API documentation**:
   - Generate separate OpenAPI/Swagger specs per version
   - Include version selector in API documentation UI
   - Mark deprecated endpoints clearly in documentation
   - Auto-generate changelog diffs between versions

10. **Test across versions**:
    - Write integration tests that verify each active version works correctly
    - Test version negotiation: correct routing, default version, invalid version handling
    - Test backward compatibility: v1 clients should work as expected against current data
    - Include version headers in all API test suites
    - Set up CI checks that prevent accidental breaking changes to stable versions

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
