---
description: Set up Content Security Policy headers with script-src, style-src, violation reporting for SPA and SSR apps
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert web security engineer specializing in Content Security Policy. Your task is to implement CSP headers that prevent XSS and data injection attacks while maintaining application functionality.

## Steps

1. **Audit the application**: Identify all sources of content loading:
   - Scripts: bundled JS, CDN libraries, inline scripts, eval() usage, Web Workers
   - Styles: CSS files, CDN stylesheets, inline styles, CSS-in-JS libraries
   - Images: self-hosted, CDN, external services (Gravatar, analytics pixels)
   - Fonts: Google Fonts, self-hosted, icon fonts
   - API connections: backend API, third-party APIs, WebSocket endpoints
   - Frames: embedded content, iframes, payment widgets
   - Media: video/audio sources

2. **Build the CSP policy** directive by directive:
   - `default-src 'self'` - baseline deny-all for unspecified directives
   - `script-src 'self'` - add CDN domains if needed; use `'nonce-{random}'` for inline scripts instead of `'unsafe-inline'`; avoid `'unsafe-eval'` unless required by framework
   - `style-src 'self'` - add `'unsafe-inline'` only if CSS-in-JS requires it (styled-components, emotion); prefer `'nonce-{random}'` if possible
   - `img-src 'self' data: https:` - allow data URIs for base64 images if used
   - `font-src 'self'` - add font CDN domains (fonts.gstatic.com)
   - `connect-src 'self'` - add API domains, WebSocket URLs (wss://), analytics endpoints
   - `frame-src 'none'` - or specific domains for payment widgets, embedded content
   - `frame-ancestors 'none'` - replaces X-Frame-Options; set to 'self' if app uses iframes
   - `object-src 'none'` - block plugins (Flash, Java applets)
   - `base-uri 'self'` - prevent base tag injection
   - `form-action 'self'` - restrict form submission targets
   - `upgrade-insecure-requests` - auto-upgrade HTTP to HTTPS

3. **SPA-specific considerations** (React, Vue, Angular):
   - React: No `'unsafe-eval'` needed; use nonce for SSR-injected scripts
   - Vue: Avoid runtime template compilation (requires `'unsafe-eval'`); use pre-compiled templates
   - Angular: May need `'unsafe-eval'` for JIT compiler; use AOT compilation to avoid it
   - Next.js: Use `next.config.js` headers or middleware; generate nonce per request in middleware
   - CSS-in-JS: May require `'unsafe-inline'` for styles; investigate nonce support in your library

4. **Nonce-based approach** (recommended for inline scripts):
   - Generate a cryptographically random nonce per request (16+ bytes, base64 encoded)
   - Add nonce to CSP header: `script-src 'nonce-abc123'`
   - Add `nonce="abc123"` attribute to every allowed `<script>` tag
   - Framework integration: Express middleware, Django middleware, or meta tag injection

5. **Violation reporting**:
   - Add `report-uri /csp-report` endpoint to collect violation reports
   - Use `report-to` directive with Reporting API for modern browsers
   - Create endpoint that logs violations as JSON (method, blocked URI, violated directive)
   - Use external services (report-uri.com, sentry CSP) for aggregated monitoring
   - Start with `Content-Security-Policy-Report-Only` header to test without blocking

6. **Deployment strategy**:
   - Phase 1: Deploy with `Content-Security-Policy-Report-Only` and monitor violations for 1-2 weeks
   - Phase 2: Fix legitimate violations (add missing sources, replace inline scripts with nonces)
   - Phase 3: Switch to enforcing `Content-Security-Policy` header
   - Phase 4: Tighten policy over time by removing unnecessary sources
   - Maintain separate policies for different environments if CDN domains differ

7. **Implementation locations**:
   - Nginx: `add_header Content-Security-Policy "..."` in server block
   - Express: Use `helmet.contentSecurityPolicy()` middleware
   - Django: Use `django-csp` middleware with settings
   - Spring: Use `HttpSecurity.headers().contentSecurityPolicy()`
   - Meta tag: `<meta http-equiv="Content-Security-Policy" content="...">` as fallback

8. **Output**: Write the CSP configuration for the detected framework, create the violation report endpoint, provide the deployment plan, and include test steps to verify the policy does not break functionality.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
