---
description: Set up environment configuration with validation, secrets management, Docker env injection, and documentation
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in environment configuration and secrets management for web applications. When asked to set up env configuration, follow these steps:

**Step 1: Audit Existing Configuration**
- Search the codebase for `process.env`, `import.meta.env`, `os.environ`, or similar environment access patterns.
- Identify all environment variables currently in use and their purposes.
- Check for hardcoded secrets, API keys, or credentials that should be environment variables.
- Look for existing `.env` files and `.env.example` templates.

**Step 2: Create Environment Files**
- `.env.example`: Template with all variable names, descriptions, and placeholder values. Commit this to git.
- `.env.local` or `.env`: Actual values for local development. Add to `.gitignore`.
- `.env.test`: Test-specific overrides (test database, mock API keys).
- `.env.production`: Production values reference (never commit real secrets).
- Use clear naming conventions: `DATABASE_URL`, `NEXT_PUBLIC_API_URL`, `SMTP_PASSWORD`.
- Prefix client-exposed variables appropriately: `NEXT_PUBLIC_`, `VITE_`, `NUXT_PUBLIC_`.

**Step 3: Implement Validation**
- Create an env validation module (e.g., `src/env.ts` or `src/config/env.ts`).
- Use zod or joi to define a schema for all environment variables with types and constraints.
- Validate at application startup and fail fast with clear error messages if variables are missing.
- Separate server-only and client-safe variables into different schemas.
- Export typed environment objects so all access is type-safe throughout the codebase.
- Example pattern for Next.js: use `@t3-oss/env-nextjs` or a custom zod schema.

**Step 4: Organize by Category**
Group variables logically in the `.env.example` file:
- **App**: `APP_NAME`, `APP_URL`, `NODE_ENV`, `PORT`.
- **Database**: `DATABASE_URL`, `DB_HOST`, `DB_PORT`, `DB_NAME`, `DB_USER`, `DB_PASSWORD`.
- **Auth**: `JWT_SECRET`, `SESSION_SECRET`, `OAUTH_CLIENT_ID`, `OAUTH_CLIENT_SECRET`.
- **Email**: `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASSWORD`, `FROM_EMAIL`.
- **Storage**: `S3_BUCKET`, `S3_REGION`, `S3_ACCESS_KEY`, `S3_SECRET_KEY`.
- **External APIs**: `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `OPENAI_API_KEY`.
- Add comments above each group and variable explaining its purpose and format.

**Step 5: Docker Environment Injection**
- Create a `docker-compose.yml` with `env_file` directive pointing to `.env`.
- Use `environment` key in docker-compose for service-specific variables.
- For Kubernetes: create ConfigMap and Secret manifests.
- Avoid baking environment variables into Docker images (use runtime injection).
- Document how to pass environment variables in different deployment environments.

**Step 6: Secrets Management**
- Never commit secrets to version control (verify `.gitignore` covers all env files).
- For production: recommend using platform secrets (Vercel, Railway, AWS SSM, Vault).
- Document the process for rotating secrets (especially JWT_SECRET, API keys).
- Set up a pre-commit hook that scans for accidentally committed secrets (e.g., `detect-secrets`).
- Suggest using `1Password CLI` or `doppler` for team secret sharing.

**Step 7: Documentation**
- Add a comment block at the top of `.env.example` with setup instructions.
- Document which variables are required vs optional (mark optional with `# Optional:`).
- Specify valid formats and examples for each variable (e.g., `DATABASE_URL=postgresql://user:pass@host:5432/db`).
- Note which variables need to be set differently per environment.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
