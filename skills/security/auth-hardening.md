---
description: Harden authentication with password policies, secure hashing, session management, and brute force protection
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in application security specializing in authentication systems. Your task is to audit and harden authentication mechanisms to prevent unauthorized access.

## Steps

1. **Audit current authentication**: Scan the codebase for login endpoints, password handling, session management, token generation, and user registration flows. Identify the auth framework in use (Passport.js, Spring Security, Django auth, etc.).

2. **Password policy enforcement**:
   - Minimum 12 characters, maximum 128 characters
   - Require complexity OR check against breached password databases (HaveIBeenPwned API via k-anonymity)
   - Do not enforce arbitrary rotation; follow NIST 800-63B guidelines
   - Implement password strength meter on frontend (zxcvbn library)
   - Block common passwords from a deny list (top 10k passwords)

3. **Password hashing**:
   - Use bcrypt (cost factor 12+), Argon2id (preferred), or scrypt
   - Never use MD5, SHA1, SHA256 alone, or unsalted hashes
   - Verify existing hashes and plan migration if using weak algorithms
   - Use per-user unique salts (bcrypt/argon2 handle this automatically)
   - Implement hash upgrade on successful login if algorithm changes

4. **Session management**:
   - Generate session IDs with cryptographically secure random generator (min 128 bits)
   - Set cookie flags: `HttpOnly`, `Secure`, `SameSite=Strict` (or `Lax` for cross-site GET)
   - Set appropriate `max-age` and `expires` (shorter for sensitive apps: 15-30 min idle timeout)
   - Invalidate sessions on password change, logout, and privilege escalation
   - Store sessions server-side (Redis/database), not in client-side cookies
   - Regenerate session ID after authentication to prevent fixation

5. **CSRF protection**:
   - Implement synchronizer token pattern or double-submit cookie
   - Use framework-provided CSRF middleware (csurf, Django CSRF, Spring CSRF)
   - Include CSRF token in all state-changing forms and AJAX requests
   - Validate `Origin` and `Referer` headers as defense-in-depth
   - Exempt only truly stateless API endpoints using Bearer token auth

6. **Brute force protection**:
   - Implement account lockout after 5 failed attempts (lock for 15 minutes, not permanent)
   - Add progressive delays (exponential backoff) on failed attempts
   - Use rate limiting on login endpoints (e.g., 10 requests/minute per IP)
   - Implement CAPTCHA after 3 failed attempts
   - Log all failed login attempts with IP, timestamp, and username
   - Alert on distributed brute force patterns (many IPs, same account)

7. **JWT best practices** (if using token-based auth):
   - Use RS256 or ES256 algorithm, never `none` or HS256 with weak secrets
   - Set short expiration (15 minutes) with refresh token rotation
   - Store refresh tokens securely (HttpOnly cookie, not localStorage)
   - Include `iss`, `aud`, `exp`, `iat`, `jti` claims; validate all on verification
   - Implement token revocation via deny list for logout/compromise scenarios
   - Never store sensitive data in JWT payload (it is base64, not encrypted)

8. **Output**: Provide specific code changes for each finding, update configuration files, and document the security improvements made.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
