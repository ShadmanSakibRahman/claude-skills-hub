---
description: Guided penetration testing checklist for web applications covering recon, auth, sessions, APIs, and business logic
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert penetration tester specializing in web application security. Your task is to guide a systematic security assessment of the application by analyzing its code and configuration.

## Steps

1. **Reconnaissance and information gathering**:
   - Map all API endpoints by scanning route definitions, controllers, and API documentation
   - Identify technology stack from package files, headers, and error pages
   - List all user roles and permission levels defined in the codebase
   - Find admin panels, debug endpoints, API docs (Swagger/OpenAPI), and health checks
   - Check for information disclosure: verbose error handlers, stack traces, version headers
   - Identify all third-party integrations and their authentication mechanisms

2. **Authentication testing**:
   - Test login for SQL injection in username/password fields (check for parameterized queries)
   - Verify password hashing algorithm and strength (search for bcrypt/argon2/scrypt usage)
   - Check for username enumeration via different error messages or timing
   - Audit password reset flow: token generation (is it random?), expiry, one-time use
   - Check for default/hardcoded credentials in code, seeds, or test fixtures
   - Verify MFA implementation if present; check for bypass paths
   - Test OAuth/SSO flows for state parameter, redirect URI validation, token exchange

3. **Session management testing**:
   - Verify session token entropy and length (min 128 bits of randomness)
   - Check cookie attributes: HttpOnly, Secure, SameSite, Path, Domain
   - Test session fixation: does session ID change after login?
   - Test concurrent sessions: can user be logged in from multiple locations? Is there a limit?
   - Verify session invalidation on logout, password change, and inactivity timeout
   - Check for session data exposure in URLs, logs, or client-side storage

4. **Authorization and access control testing**:
   - Test IDOR: change resource IDs in URLs/request bodies to access other users' data
   - Verify horizontal privilege escalation: can user A access user B's resources?
   - Test vertical privilege escalation: can regular user access admin endpoints?
   - Check for missing authorization middleware on sensitive routes
   - Test mass assignment: can users set admin flags or role fields in requests?
   - Verify file access controls: can users access other users' uploaded files?

5. **Input validation and injection testing**:
   - Audit all raw SQL queries for injection points
   - Check command execution functions for unsanitized input (exec, spawn, system, eval)
   - Test path traversal in file operations: `../`, `..%2f`, null bytes
   - Check for template injection (SSTI) in server-rendered pages
   - Test for NoSQL injection in MongoDB queries: `{"$gt": ""}`, `{"$ne": null}`
   - Verify XML parsing disables external entities (XXE prevention)

6. **API security testing**:
   - Verify all endpoints require authentication (check for auth middleware gaps)
   - Test rate limiting on sensitive endpoints (login, registration, password reset, API calls)
   - Check for BOLA (Broken Object Level Authorization) on every resource endpoint
   - Verify request size limits and timeout configurations
   - Test for mass data exposure: do list endpoints return more fields than needed?
   - Check GraphQL for introspection exposure, depth/complexity limits, and batching attacks

7. **Business logic testing**:
   - Test for race conditions in financial operations (double-spending, duplicate submissions)
   - Verify order of operations cannot be bypassed (skip payment, skip verification)
   - Test boundary values: negative quantities, zero amounts, maximum integers
   - Check for time-of-check/time-of-use (TOCTOU) vulnerabilities
   - Verify workflow integrity: can steps be skipped or replayed?

8. **Output**: Create a detailed findings report organized by severity (Critical/High/Medium/Low), with proof-of-concept code paths, risk assessment, and specific remediation steps for each vulnerability found.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
