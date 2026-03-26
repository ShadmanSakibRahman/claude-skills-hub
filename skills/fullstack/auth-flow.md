---
description: Implement end-to-end authentication with sign up, login, OAuth, RBAC, email verification, and protected routes
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in authentication and authorization for web applications. When asked to implement auth, follow these steps:

**Step 1: Choose the Auth Strategy**
- Identify the framework and recommend the best auth solution:
  - **Next.js**: Auth.js (NextAuth), Clerk, Lucia, or Supabase Auth.
  - **Remix**: Remix Auth, custom session-based auth.
  - **SvelteKit**: Lucia, SvelteKit built-in auth hooks.
  - **Django**: Django built-in auth, django-allauth.
  - **Laravel**: Laravel Breeze/Jetstream, Fortify.
  - **Rails**: Devise, Rodauth.
- Decide between session-based (recommended for server-rendered apps) and JWT-based (for APIs/SPAs).
- Determine required auth methods: email/password, magic link, OAuth, or passwordless.

**Step 2: Database Schema**
- Create the user model with: id, email (unique), name, password_hash, role, email_verified, created_at, updated_at.
- Create the session model with: id, user_id, token/session_token, expires_at, ip_address, user_agent.
- Create the account model for OAuth: id, user_id, provider, provider_account_id, access_token, refresh_token.
- Create the verification_token model: id, token, email, type (email_verify, password_reset), expires_at.
- Run the migration to create these tables.

**Step 3: Sign Up Flow**
- Create a registration form: email, password, confirm password, name.
- Validate inputs: email format, password strength (min 8 chars, complexity rules), matching passwords.
- Hash the password using bcrypt or argon2 (never store plain text).
- Check for existing accounts with the same email.
- Create the user record and send an email verification link.
- Redirect to a "check your email" page or auto-login based on requirements.

**Step 4: Login and Session Management**
- Create a login form: email, password, optional "remember me" checkbox.
- Verify credentials: look up user by email, compare password hash.
- Implement rate limiting on login attempts (5 attempts per 15 minutes per IP/email).
- On success: create a session record, set an HTTP-only secure cookie with the session token.
- Implement CSRF protection for session-based auth.
- Add "remember me" functionality: extend session duration from hours to days.

**Step 5: OAuth Social Login**
- Configure OAuth providers: Google, GitHub, Discord (or as needed).
- Set up callback URLs and register them with the provider's developer console.
- Handle the OAuth flow: redirect to provider, receive callback, extract user info.
- Link OAuth accounts to existing users if the email matches.
- Handle edge cases: user denies permission, provider returns incomplete data.
- Store provider tokens for potential API access.

**Step 6: Password Reset and Email Verification**
- Password reset: generate a time-limited token (1 hour expiry), send reset link via email.
- Reset form: validate the token, accept new password, hash and update, invalidate all existing sessions.
- Email verification: send a verification link on sign-up, mark email_verified on click.
- Resend verification: allow users to request a new verification email with rate limiting.

**Step 7: Role-Based Access Control (RBAC)**
- Define roles: admin, user, moderator (or as needed for the application).
- Create middleware/guards that check user roles before allowing access to routes.
- Protect API routes: verify session, check permissions, return 401/403 as appropriate.
- Protect frontend routes: redirect unauthenticated users to login, unauthorized users to a 403 page.
- Create a `useAuth()` hook or context provider for accessing the current user and their permissions in components.
- Implement both route-level and component-level authorization checks.

**Step 8: Logout and Security**
- Implement logout: destroy the session record, clear the session cookie.
- Add "logout all devices" functionality that invalidates all sessions for a user.
- Set secure cookie attributes: HttpOnly, Secure, SameSite=Lax, appropriate domain/path.
- Implement session expiration and cleanup of stale sessions.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
