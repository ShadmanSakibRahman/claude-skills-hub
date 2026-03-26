---
description: Create deployment configurations for Vercel, Netlify, Railway, Fly.io, or AWS with CI/CD and preview deployments
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in cloud deployment and DevOps for web applications. When asked to set up deployment, follow these steps:

**Step 1: Analyze the Project**
- Identify the framework and runtime: Next.js, Remix, Nuxt, SvelteKit, Express, Django, Rails, etc.
- Determine the build output: static files, serverless functions, Docker container, or hybrid.
- Check for external dependencies: database, Redis, file storage, background jobs.
- Identify the preferred deployment platform or recommend one based on the stack.

**Step 2: Platform-Specific Configuration**

For **Vercel**:
- Create `vercel.json` with build settings, rewrites, headers, and function config.
- Configure framework preset detection or set manually.
- Set up environment variables via `vercel env` or dashboard.
- Configure serverless function regions and memory/duration limits.

For **Netlify**:
- Create `netlify.toml` with build command, publish directory, and redirects.
- Configure serverless functions directory and edge functions.
- Set up environment variables and build plugins.

For **Railway**:
- Create `railway.json` or `Procfile` with start command.
- Configure attached databases (Postgres, Redis, MySQL).
- Set up health check endpoint and restart policies.

For **Fly.io**:
- Create `fly.toml` with app name, region, services, and health checks.
- Create a `Dockerfile` optimized for the runtime with multi-stage builds.
- Configure persistent volumes for database or file storage.
- Set up machine sizing and auto-scaling rules.

For **AWS**:
- Create infrastructure as code (CDK, Terraform, or SAM template).
- Configure ECS/Fargate for containerized apps or Lambda for serverless.
- Set up ALB, CloudFront, Route53, and ACM for domain and SSL.

**Step 3: Build Configuration**
- Define the build command and output directory in the platform config.
- Set up build-time environment variables (prefix with appropriate framework marker).
- Configure build caching to speed up deployments.
- Add a build step that runs database migrations if needed.
- Ensure the build process generates source maps for error tracking.

**Step 4: Domain and SSL Setup**
- Document how to add a custom domain on the chosen platform.
- Configure DNS records: A/AAAA records or CNAME pointing to the platform.
- Verify SSL certificate auto-provisioning is enabled.
- Set up redirects: www to non-www (or vice versa), HTTP to HTTPS.
- Configure CORS headers if the API is on a different subdomain.

**Step 5: Preview Deployments**
- Enable preview/staging deployments for pull requests.
- Configure separate environment variables for preview environments.
- Set up preview database instances or use a shared staging database.
- Add the preview URL pattern to allowed origins in CORS and OAuth configs.
- Configure branch-based deployment rules (main = production, develop = staging).

**Step 6: CI/CD Pipeline**
- Create a GitHub Actions workflow (or GitLab CI/CircleCI) for automated deployments.
- Pipeline stages: lint, type-check, test, build, deploy.
- Run database migrations as a post-deploy step.
- Set up notifications for deploy success/failure (Slack, email).
- Configure rollback strategy: automatic rollback on health check failure.

**Step 7: Monitoring and Post-Deploy**
- Add a health check endpoint (`/api/health`) that verifies database connectivity.
- Configure uptime monitoring (UptimeRobot, Better Uptime, or platform-native).
- Set up logging aggregation (platform logs, or external like Datadog/Logtail).
- Document the deployment process, rollback procedure, and environment architecture.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
