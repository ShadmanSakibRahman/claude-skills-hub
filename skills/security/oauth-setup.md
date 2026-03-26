---
description: Implement OAuth 2.0 / OpenID Connect with PKCE, token management, refresh rotation, and provider integration
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert identity and access management engineer. Your task is to implement secure OAuth 2.0 / OpenID Connect authentication flows in the application.

## Steps

1. **Determine the appropriate flow**:
   - **Authorization Code with PKCE**: For SPAs, mobile apps, and server-rendered apps (recommended for all clients)
   - **Client Credentials**: For machine-to-machine / service-to-service communication
   - **Device Authorization**: For input-constrained devices (smart TVs, CLIs)
   - Never use Implicit flow (deprecated) or Resource Owner Password flow (insecure)

2. **Authorization Code Flow with PKCE implementation**:
   - Generate `code_verifier`: 43-128 character random string using `[A-Za-z0-9-._~]`
   - Compute `code_challenge`: Base64URL-encode(SHA256(code_verifier))
   - Redirect to authorization endpoint with params: `response_type=code`, `client_id`, `redirect_uri`, `scope`, `state` (CSRF token), `code_challenge`, `code_challenge_method=S256`
   - Handle callback: verify `state` matches, exchange `code` for tokens at token endpoint with `code_verifier`
   - Validate `id_token`: verify signature (JWK), issuer, audience, expiry, nonce

3. **Token management**:
   - **Access Token**: Short-lived (5-15 minutes), used for API authorization in `Authorization: Bearer` header
   - **Refresh Token**: Longer-lived (7-30 days), stored securely, used to obtain new access tokens
   - **ID Token**: Contains user identity claims, validate on receipt, do not send to APIs
   - Store tokens server-side in session or in HttpOnly/Secure cookies (never in localStorage)
   - For SPAs with BFF pattern: keep tokens in backend, use session cookie for frontend

4. **Refresh token rotation**:
   - Enable refresh token rotation: each refresh request returns a new refresh token
   - Invalidate the old refresh token after use (one-time use)
   - Implement reuse detection: if a rotated-out refresh token is used, revoke the entire token family (indicates theft)
   - Set absolute expiry on refresh tokens (e.g., 30 days max regardless of activity)
   - Implement idle timeout (e.g., 7 days of inactivity revokes refresh token)

5. **Scope management**:
   - Request minimum scopes needed: `openid profile email` for basic identity
   - Use incremental consent: request additional scopes only when the feature is used
   - Map OAuth scopes to application permissions/roles
   - Validate scopes on resource server for every API request
   - Document all scopes and their purposes

6. **Provider integration**:
   - **Google**: Use `accounts.google.com` discovery endpoint, scopes for profile/email/calendar
   - **GitHub**: OAuth app or GitHub App, scopes for `user:email`, `read:org`
   - **Auth0**: Configure tenant, application, connections, rules/actions
   - **Microsoft**: Azure AD with MSAL library, configure app registration
   - Use OpenID Connect Discovery (`/.well-known/openid-configuration`) for automatic endpoint configuration
   - Store client secrets in environment variables or secrets manager

7. **Security hardening**:
   - Validate `redirect_uri` exactly (no wildcards, no open redirects)
   - Use `state` parameter to prevent CSRF on authorization callback
   - Implement token revocation endpoint for logout
   - Set up back-channel logout or front-channel logout for SSO
   - Implement `aud` (audience) validation on all tokens
   - Use HTTPS for all OAuth endpoints (reject HTTP even in development)
   - Handle token expiry gracefully with automatic refresh and retry logic

8. **Output**: Write the OAuth integration code (routes, middleware, token management), configuration for the chosen provider, and provide setup instructions including provider console configuration steps.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
