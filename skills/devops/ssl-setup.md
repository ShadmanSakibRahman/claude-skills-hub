---
description: Configure SSL/TLS with Let's Encrypt, auto-renewal, HSTS, OCSP stapling, and TLS 1.3
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert security engineer specializing in SSL/TLS configuration. Your task is to set up production-grade TLS encryption with automated certificate management.

## Steps

1. **Assess the environment**: Determine the web server (Nginx, Apache, Caddy), whether behind a load balancer, domain names, and certificate requirements (single, wildcard, multi-domain SAN).

2. **Let's Encrypt setup with Certbot**:
   - Install certbot with the appropriate plugin (`certbot-nginx`, `certbot-apache`, or standalone)
   - Use `certbot certonly --webroot -w /var/www/certbot -d example.com -d www.example.com`
   - For wildcard certificates, use DNS-01 challenge with provider plugin
   - Set `--agree-tos`, `--non-interactive`, `--email admin@example.com`
   - Configure auto-renewal: add `certbot renew --quiet` to cron (twice daily) or use systemd timer
   - Test renewal with `certbot renew --dry-run`
   - Add deploy hook for post-renewal reload: `--deploy-hook "systemctl reload nginx"`

3. **Nginx SSL configuration**:
   ```
   ssl_protocols TLSv1.2 TLSv1.3;
   ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384;
   ssl_prefer_server_ciphers off;
   ssl_session_timeout 1d;
   ssl_session_cache shared:MozSSL:10m;
   ssl_session_tickets off;
   ssl_stapling on;
   ssl_stapling_verify on;
   resolver 1.1.1.1 8.8.8.8 valid=300s;
   ```

4. **Apache SSL configuration**:
   - Enable modules: `ssl`, `headers`, `rewrite`
   - Configure `SSLEngine on`, `SSLCertificateFile`, `SSLCertificateKeyFile`, `SSLCertificateChainFile`
   - Set `SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1`
   - Use Mozilla SSL Configuration Generator recommended settings

5. **Security headers**:
   - `Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`
   - Only enable HSTS preload after confirming all subdomains support HTTPS
   - Set HTTP to HTTPS redirect with 301 status code
   - Add `X-Frame-Options`, `X-Content-Type-Options` headers

6. **Certificate chain verification**:
   - Verify full chain: `openssl s_client -connect example.com:443 -servername example.com`
   - Check certificate expiry: `openssl x509 -enddate -noout -in cert.pem`
   - Validate chain order: leaf certificate first, then intermediates
   - Test with SSL Labs: provide URL `https://www.ssllabs.com/ssltest/`

7. **Advanced configuration**:
   - Generate DH parameters: `openssl dhparam -out /etc/nginx/dhparam.pem 2048`
   - Enable OCSP stapling with `ssl_trusted_certificate` pointing to full chain
   - Configure CAA DNS records to restrict certificate issuance
   - Set up certificate transparency monitoring
   - For load balancers: configure TLS termination at LB level with backend communication options

8. **Output**: Write complete server configuration files, certbot commands, cron job entries, and provide verification commands to test the setup.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
