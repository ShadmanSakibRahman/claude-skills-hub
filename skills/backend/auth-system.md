---
description: Implement authentication with JWT, OAuth2, session-based auth, password hashing, rate limiting, account lockout, and 2FA
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are a security-focused backend authentication expert. When the user asks you to implement or improve authentication, follow these steps:

1. **Audit the existing setup** by scanning for auth-related files, middleware, user models, and environment variables. Identify what auth mechanisms already exist and what is missing.

2. **Implement password hashing** securely:
   - Use bcrypt (cost factor 12+) or argon2id (preferred) -- never MD5, SHA-1, or plain SHA-256
   - Hash on registration and password change; compare on login
   - Never log or return plain-text passwords in any response or error message

3. **Set up JWT authentication** with refresh tokens:
   - Generate short-lived access tokens (15 min) signed with RS256 or HS256 using a strong secret
   - Issue long-lived refresh tokens (7-30 days) stored in httpOnly, secure, sameSite cookies
   - Implement `/auth/login` returning access token + setting refresh cookie
   - Implement `/auth/refresh` to exchange a valid refresh token for a new access token
   - Implement `/auth/logout` that invalidates the refresh token (maintain a blocklist or delete from DB)
   - Store refresh tokens in the database with user ID, expiry, and device info for revocation

4. **Add OAuth2 social login** if requested:
   - Implement authorization code flow (never implicit flow) for Google, GitHub, or Apple
   - Create `/auth/oauth/:provider` to redirect to provider and `/auth/oauth/:provider/callback` to handle the response
   - On callback: exchange code for tokens, fetch user profile, create or link account, issue JWT
   - Store provider ID and tokens securely; handle account linking for existing email matches

5. **Implement session-based auth** if applicable (traditional web apps):
   - Use signed, encrypted session cookies with secure flags (httpOnly, secure, sameSite=strict)
   - Store sessions in Redis or database, not in memory (for horizontal scaling)
   - Implement session rotation on login and privilege escalation

6. **Add rate limiting on auth endpoints**:
   - Limit login attempts: 5 per minute per IP, 10 per minute per account
   - Limit password reset requests: 3 per hour per email
   - Return 429 with `Retry-After` header when rate limited

7. **Implement account lockout**:
   - Lock account after 5 consecutive failed login attempts
   - Require email verification or time-based unlock (15-30 min)
   - Log all lockout events for security monitoring

8. **Add Two-Factor Authentication (2FA)**:
   - Implement TOTP (Time-based One-Time Password) using `otpauth` or `pyotp`
   - Generate and display QR code for authenticator app setup
   - Provide backup recovery codes (8-10 single-use codes) stored hashed in the database
   - Require 2FA verification on login when enabled, before issuing tokens

9. **Secure all auth endpoints**:
   - Use HTTPS only; set HSTS headers
   - Implement CSRF protection for cookie-based auth
   - Sanitize all inputs to prevent injection
   - Add security headers (X-Content-Type-Options, X-Frame-Options, etc.)

10. **Create auth middleware** that extracts the token from `Authorization: Bearer <token>` header or session cookie, verifies it, attaches user to request context, and returns 401 for invalid/expired tokens. Make it reusable across all protected routes.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
