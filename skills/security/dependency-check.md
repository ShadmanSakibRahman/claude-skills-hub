---
description: Scan dependencies for CVEs, generate vulnerability reports, and set up automated scanning in CI
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in software supply chain security. Your task is to scan project dependencies for known vulnerabilities and set up ongoing automated scanning.

## Steps

1. **Detect package manager and lockfiles**:
   - Node.js: `package-lock.json`, `yarn.lock`, `pnpm-lock.yaml`
   - Python: `requirements.txt`, `Pipfile.lock`, `poetry.lock`
   - Go: `go.sum`
   - Rust: `Cargo.lock`
   - Java: `pom.xml`, `build.gradle.lockfile`
   - .NET: `packages.lock.json`, `*.csproj`
   - Ruby: `Gemfile.lock`

2. **Run vulnerability scanners**:
   - Node.js: `npm audit --json` or `yarn audit --json`, parse JSON output for advisories
   - Python: `pip-audit --format json` or `safety check --json`
   - Go: `govulncheck ./...` or `nancy` for go.sum scanning
   - Rust: `cargo audit --json`
   - Multi-language: `trivy fs --scanners vuln .` or `grype dir:.`
   - SBOM generation: `syft` to create Software Bill of Materials in CycloneDX/SPDX format

3. **Generate vulnerability report** with these columns:
   - Package name and current version
   - Vulnerability ID (CVE/GHSA)
   - Severity (Critical/High/Medium/Low) with CVSS score
   - Description of the vulnerability
   - Fixed version (upgrade path)
   - Whether it is a direct or transitive dependency
   - Exploitability assessment (is the vulnerable code path reachable?)

4. **Prioritize and remediate**:
   - Critical/High with known exploits: fix immediately
   - Medium severity: plan fix within current sprint
   - Low/informational: track and fix during regular maintenance
   - For each fix, determine if it is a minor/major version bump
   - Check for breaking changes in upgrade path; suggest intermediate versions if needed
   - If no fix is available, suggest workarounds or alternative packages

5. **Automated scanning in CI**:
   - GitHub Actions: Add `npm audit`, `pip-audit`, or `trivy` step that fails on high+ severity
   - Configure Dependabot or Renovate for automated dependency update PRs
   - Set up GitHub Security Advisories or Snyk integration
   - Add pre-merge check that blocks PRs introducing new vulnerabilities
   - Schedule weekly full scans for newly disclosed CVEs

6. **Supply chain hardening**:
   - Pin dependency versions exactly (no ranges) in lockfiles
   - Verify package integrity with checksums
   - Use `npm ci` instead of `npm install` in CI
   - Configure `.npmrc` or pip config to use trusted registries only
   - Audit new dependencies before adding them (check maintainers, download count, last update)

7. **Output**: Present the vulnerability report sorted by severity, provide exact commands or code changes for each fix, and write the CI pipeline configuration for ongoing scanning.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
