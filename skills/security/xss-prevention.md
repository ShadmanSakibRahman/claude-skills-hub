---
description: Prevent XSS vulnerabilities with output encoding, CSP, DOMPurify, HttpOnly cookies, and framework protections
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert web security engineer specializing in Cross-Site Scripting prevention. Your task is to audit the codebase for XSS vulnerabilities and implement comprehensive defenses.

## Steps

1. **Audit for XSS vulnerabilities**: Search the codebase for dangerous patterns:
   - **Reflected XSS**: User input rendered directly in HTML responses without encoding. Search for query params, form values, URL fragments echoed back in templates.
   - **Stored XSS**: User-generated content (comments, profiles, messages) stored in database and rendered without sanitization. Check all places where DB content is rendered.
   - **DOM-based XSS**: Client-side JavaScript using `innerHTML`, `outerHTML`, `document.write()`, `eval()`, `setTimeout(string)`, `location.href` with user-controlled data. Search for `dangerouslySetInnerHTML` (React), `v-html` (Vue), `[innerHTML]` (Angular).
   - Template rendering without auto-escaping: `|safe` in Jinja2, `{!! !!}` in Blade, `<%- %>` in EJS, `ng-bind-html` in Angular.

2. **Output encoding** (context-dependent):
   - **HTML context**: Encode `<>&"'` to HTML entities (`&lt;`, `&gt;`, `&amp;`, `&quot;`, `&#x27;`)
   - **HTML attribute context**: Encode all non-alphanumeric characters; always quote attribute values
   - **JavaScript context**: Use `JSON.stringify()` for data injected into `<script>` blocks; never interpolate into JS code strings
   - **URL context**: Use `encodeURIComponent()` for query parameters; validate scheme is http/https
   - **CSS context**: Encode non-alphanumeric characters; avoid user input in style attributes
   - Use framework-provided encoding functions; do not build custom encoders

3. **Framework-specific protections**:
   - **React**: JSX auto-escapes by default. Audit all uses of `dangerouslySetInnerHTML`; ensure content is sanitized with DOMPurify before insertion. Never pass user input to `href` with `javascript:` protocol.
   - **Vue**: `{{ }}` auto-escapes. Audit all uses of `v-html`; replace with `v-text` where possible or sanitize with DOMPurify. Check for `v-bind:href` with user URLs.
   - **Angular**: Built-in sanitizer for `[innerHTML]`. Audit `bypassSecurityTrustHtml()` calls; each must be justified with sanitized input. Enable strict contextual auto-escaping.
   - **Server-side templates**: Enable auto-escaping globally (Jinja2 `autoescape=True`, Django default, Go `html/template`). Audit all instances where escaping is explicitly disabled.

4. **DOMPurify for rich content**:
   - Install DOMPurify for any place that must render user-provided HTML (WYSIWYG editors, markdown rendering, email templates)
   - Configure allowed tags and attributes: `DOMPurify.sanitize(dirty, {ALLOWED_TAGS: ['b', 'i', 'em', 'strong', 'a', 'p', 'br', 'ul', 'ol', 'li'], ALLOWED_ATTR: ['href', 'title']})`
   - Strip all event handler attributes (`onclick`, `onerror`, etc.)
   - Remove `javascript:`, `data:`, and `vbscript:` URI schemes
   - Sanitize on the server side before storage AND on the client side before rendering (defense in depth)

5. **Cookie and header protections**:
   - Set `HttpOnly` flag on all session cookies to prevent JavaScript access
   - Set `Secure` flag to ensure cookies are only sent over HTTPS
   - Set `SameSite=Strict` or `SameSite=Lax` to prevent cross-site cookie sending
   - Implement Content Security Policy headers (see csp-headers skill for details)
   - Set `X-Content-Type-Options: nosniff` to prevent MIME type sniffing
   - Set `X-XSS-Protection: 0` (modern recommendation; rely on CSP instead)

6. **Additional defense layers**:
   - Use `Trusted Types` API for DOM XSS prevention in supported browsers
   - Implement input validation as first layer (reject unexpected characters) but never rely on it alone
   - Use `textContent` instead of `innerHTML` when inserting plain text
   - Sanitize filenames in Content-Disposition headers to prevent header injection
   - Escape data in JSON responses served with `text/html` Content-Type
   - Use Subresource Integrity (SRI) hashes for CDN scripts

7. **Testing**:
   - Test with common XSS payloads: `<script>alert(1)</script>`, `<img onerror=alert(1) src=x>`, `javascript:alert(1)`, `"><svg/onload=alert(1)>`
   - Test attribute injection: `" onfocus=alert(1) autofocus="`
   - Test in different contexts: HTML body, attributes, JavaScript blocks, URLs, CSS
   - Add automated tests that verify encoding of special characters in all output points
   - Use OWASP ZAP or Burp Suite for automated XSS scanning

8. **Output**: Report all found XSS vulnerabilities with file locations and severity, provide fixes for each instance, add DOMPurify integration where needed, configure security headers, and add regression tests.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
