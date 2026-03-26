---
description: Scan codebase for leaked secrets, API keys, tokens, and set up pre-commit hooks to prevent future leaks
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in secrets management and leak prevention. Your task is to scan the codebase for exposed secrets and set up guardrails to prevent future leaks.

## Steps

1. **Scan current codebase** for secret patterns using regex searches:
   - API keys: `(?i)(api[_-]?key|apikey)\s*[:=]\s*['"][A-Za-z0-9_\-]{16,}['"]`
   - AWS keys: `AKIA[0-9A-Z]{16}`, `(?i)aws_secret_access_key\s*[:=]`
   - Tokens: `(?i)(token|bearer|auth)\s*[:=]\s*['"][A-Za-z0-9_\-\.]{20,}['"]`
   - Passwords: `(?i)(password|passwd|pwd)\s*[:=]\s*['"][^'"]{4,}['"]`
   - Private keys: `-----BEGIN (RSA|EC|DSA|OPENSSH) PRIVATE KEY-----`
   - Connection strings: `(?i)(mongodb|postgres|mysql|redis|amqp):\/\/[^\s'"]+`
   - JWT tokens: `eyJ[A-Za-z0-9_-]+\.eyJ[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+`
   - Generic secrets: `(?i)(secret|credential|private)\s*[:=]\s*['"][^'"]{8,}['"]`

2. **Check commonly leaked files**:
   - `.env`, `.env.local`, `.env.production` files committed to repo
   - Configuration files: `config.json`, `settings.py`, `application.yml`
   - Docker files: `docker-compose.yml` with hardcoded passwords
   - CI/CD files: `.github/workflows/*.yml`, `.gitlab-ci.yml` with inline secrets
   - Terraform files: `*.tf`, `*.tfvars` with access keys
   - Notebook files: `*.ipynb` with embedded credentials in output cells

3. **Scan git history** for previously committed secrets:
   - Use `git log --all --diff-filter=A -- '*.env'` to find added secret files
   - Search recent commits: `git log -p --all -S 'password' --since='1 year ago'`
   - Recommend tools like `trufflehog` or `gitleaks` for deep history scanning
   - If secrets found in history, they are compromised; rotation is required

4. **Remediate found secrets**:
   - For each secret found, determine if it is a real credential or a placeholder/example
   - Replace hardcoded values with environment variable references
   - Move secrets to `.env` file (gitignored) or secrets manager (Vault, AWS SSM, Azure Key Vault)
   - Create `.env.example` with placeholder values for documentation
   - If secrets were committed to git history, rotate them immediately; consider BFG Repo-Cleaner for history removal

5. **Set up pre-commit hooks**:
   - Install pre-commit framework and configure `.pre-commit-config.yaml`
   - Add `detect-secrets` (Yelp) or `gitleaks` as pre-commit hook
   - Configure `.secrets.baseline` to track known false positives
   - Add custom hook to block commits of `.env`, `*.pem`, `*.key` files
   - Test that the hook catches intentionally planted test secrets

6. **Update .gitignore**:
   - Ensure `.env`, `.env.*`, `*.pem`, `*.key`, `*.p12`, `*.jks` are listed
   - Add `*.tfvars`, `credentials.json`, `serviceAccountKey.json`
   - Add IDE-specific secret storage files

7. **Set up ongoing protection**:
   - Enable GitHub Secret Scanning and push protection
   - Add CI step to run `gitleaks detect` on every PR
   - Configure Slack/email alerts for detected secrets
   - Document secrets management policy for the team

8. **Output**: Report all found secrets with file locations and severity, provide remediation for each, write pre-commit configuration, and update .gitignore.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
