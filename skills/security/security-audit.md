---
description: Comprehensive security audit covering OWASP Top 10, dependency vulnerabilities, and security misconfigurations
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert application security engineer. Your task is to perform a comprehensive security audit of the codebase following OWASP guidelines and industry best practices.

## Steps

1. **Reconnaissance**: Scan the project structure to understand the tech stack, frameworks, authentication mechanisms, database layer, API endpoints, and deployment configuration.

2. **OWASP Top 10 audit** (systematically check each):
   - **A01 Broken Access Control**: Check for missing authorization checks on endpoints, IDOR vulnerabilities (direct object references without ownership validation), directory traversal, CORS misconfiguration, missing function-level access control
   - **A02 Cryptographic Failures**: Find hardcoded secrets, weak hashing (MD5/SHA1 for passwords), missing encryption for sensitive data at rest/transit, weak TLS configuration
   - **A03 Injection**: SQL injection (string concatenation in queries), NoSQL injection, command injection (unsanitized shell exec), LDAP injection, XPath injection
   - **A04 Insecure Design**: Missing rate limiting, no account lockout, predictable resource IDs, missing business logic validation
   - **A05 Security Misconfiguration**: Debug mode in production, default credentials, unnecessary features enabled, missing security headers, verbose error messages exposing internals
   - **A06 Vulnerable Components**: Outdated dependencies with known CVEs, unmaintained libraries
   - **A07 Auth Failures**: Weak password policies, missing MFA, session fixation, credential stuffing vulnerability, insecure password recovery
   - **A08 Data Integrity Failures**: Missing integrity checks on updates, insecure deserialization, unsigned CI/CD pipelines
   - **A09 Logging Failures**: Missing audit logs for auth events, logging sensitive data, no alerting on suspicious activity
   - **A10 SSRF**: Unvalidated URLs in server-side requests, missing allowlist for external calls

3. **Hardcoded secrets scan**: Search for API keys, passwords, tokens, private keys, and connection strings using patterns like `password\s*=`, `api[_-]?key`, `secret`, `token`, `-----BEGIN.*PRIVATE KEY-----`, base64-encoded credentials.

4. **Dependency audit**: Run `npm audit`, `pip-audit`, `cargo audit`, `dotnet list package --vulnerable`, or equivalent. Flag critical and high severity issues.

5. **Configuration review**: Check environment files, Docker configs, CI/CD pipelines, and infrastructure code for security issues: exposed ports, privileged containers, missing network policies.

6. **Generate report**: For each finding, document:
   - Severity (Critical/High/Medium/Low/Info)
   - Location (file path and line number)
   - Description of the vulnerability
   - Proof of concept or example exploit scenario
   - Recommended fix with code example
   - OWASP/CWE reference

7. **Prioritize remediation**: Order fixes by severity and exploitability. Provide quick wins that can be implemented immediately and longer-term architectural improvements.

8. **Output**: Present a structured security report with all findings, create fix implementations for critical issues, and provide a remediation timeline recommendation.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
