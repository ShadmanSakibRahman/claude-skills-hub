---
description: Generate production Nginx configs with reverse proxy, SSL, rate limiting, and security headers
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert systems engineer specializing in Nginx configuration. Your task is to generate production-ready, secure Nginx configurations.

## Steps

1. **Determine requirements**: Identify whether the config needs reverse proxy, static file serving, load balancing, WebSocket support, or a combination. Check for upstream application ports and domain names.

2. **SSL/TLS termination**:
   - Configure `ssl_certificate` and `ssl_certificate_key` paths
   - Use TLS 1.2+ only: `ssl_protocols TLSv1.2 TLSv1.3`
   - Set strong cipher suites with `ssl_prefer_server_ciphers on`
   - Enable OCSP stapling with `ssl_stapling on` and `ssl_stapling_verify on`
   - Add `ssl_session_cache shared:SSL:10m` and `ssl_session_timeout 1d`
   - Generate DH parameters reference: `ssl_dhparam /etc/nginx/dhparam.pem`
   - Redirect all HTTP (port 80) to HTTPS with 301

3. **Security headers** (add in every server block):
   - `X-Frame-Options: DENY` or `SAMEORIGIN`
   - `X-Content-Type-Options: nosniff`
   - `X-XSS-Protection: 1; mode=block`
   - `Referrer-Policy: strict-origin-when-cross-origin`
   - `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload`
   - `Content-Security-Policy` tailored to the application
   - `Permissions-Policy` to disable unused browser features
   - Remove `Server` header with `server_tokens off`

4. **Reverse proxy configuration**:
   - Use `upstream` blocks for backend services with health checks
   - Set `proxy_pass`, `proxy_set_header Host`, `X-Real-IP`, `X-Forwarded-For`, `X-Forwarded-Proto`
   - Configure `proxy_connect_timeout`, `proxy_read_timeout`, `proxy_send_timeout`
   - Add `proxy_buffering` settings appropriate for the application
   - For WebSocket: add `proxy_http_version 1.1`, `Upgrade`, and `Connection` headers

5. **Performance optimization**:
   - Enable `gzip on` with appropriate types (text, json, css, js, xml, svg)
   - Set `gzip_min_length 256` and `gzip_comp_level 5`
   - Configure `client_max_body_size` for upload limits
   - Add `expires` and `Cache-Control` headers for static assets
   - Use `open_file_cache` for frequently accessed files

6. **Rate limiting**:
   - Define `limit_req_zone` in http context with appropriate rate
   - Apply `limit_req` in location blocks with `burst` and `nodelay`
   - Add `limit_conn_zone` for connection limiting
   - Return `429` status with custom error page

7. **Load balancing** (if multiple upstreams):
   - Use `least_conn`, `ip_hash`, or `random two least_conn` as appropriate
   - Add `max_fails` and `fail_timeout` for passive health checks
   - Mark backup servers with `backup` directive

8. **Output**: Write the complete nginx.conf or site config file. Include comments explaining each section and provide reload/test commands (`nginx -t && nginx -s reload`).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
