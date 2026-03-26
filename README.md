<p align="center">
  <img src="https://img.shields.io/badge/Skills-178+-blue?style=for-the-badge" alt="Skills Count"/>
  <img src="https://img.shields.io/badge/Categories-16-green?style=for-the-badge" alt="Categories"/>
  <img src="https://img.shields.io/badge/License-CC%20BY%204.0-yellow?style=for-the-badge" alt="License"/>
  <img src="https://img.shields.io/github/stars/ShadmanSakibRahman/claude-skills-hub?style=for-the-badge" alt="Stars"/>
  <img src="https://img.shields.io/github/forks/ShadmanSakibRahman/claude-skills-hub?style=for-the-badge" alt="Forks"/>
</p>

<h1 align="center">Claude Skills Hub</h1>

<p align="center">
  <strong>The most comprehensive collection of Claude Code skills in one place.</strong><br/>
  178+ production-ready custom slash commands across 16 categories.<br/>
  Star it. Fork it. Ship faster.
</p>

<p align="center">
  <a href="#-how-to-use">How to Use</a> |
  <a href="#-popular-skills">Popular Skills</a> |
  <a href="#-all-categories">All Categories</a> |
  <a href="#-contributing">Contributing</a>
</p>

<p align="center">
  <sub>Curated and maintained by <a href="https://github.com/ShadmanSakibRahman">@ShadmanSakibRahman</a></sub>
</p>

---

## What is this?

[Claude Code](https://docs.anthropic.com/en/docs/claude-code) supports **custom slash commands** — reusable skill files that turn Claude into a specialized expert for any task. This repo is the **largest curated collection** of these skills, organized by domain.

Each skill is a `.md` file you place into your `.claude/commands/` folder. Then type `/skill-name` in Claude Code and it activates.

---

## How to Use

### Step 1: Star & Fork this repo

Click the **Star** button above to bookmark this collection, then **Fork** it to your own GitHub account so you always have access and get updates.

### Step 2: Clone your fork

```bash
git clone https://github.com/<your-username>/claude-skills-hub.git
```

### Step 3: Set up a symlink to your Claude commands

**macOS / Linux:**
```bash
ln -s "$(pwd)/claude-skills-hub/skills" ~/.claude/skills-hub
```

**Windows (PowerShell as Admin):**
```powershell
New-Item -ItemType SymbolicLink -Path "$HOME\.claude\skills-hub" -Target "$(Get-Location)\claude-skills-hub\skills"
```

### Step 4: Stay updated

Since you forked, you can pull updates anytime:
```bash
cd claude-skills-hub
git pull upstream main
```

### Project-Level Usage (for teams)

Add this repo as a **git submodule** so your whole team gets the skills:

```bash
cd your-project
git submodule add https://github.com/ShadmanSakibRahman/claude-skills-hub.git .claude/skills-hub
git commit -m "Add Claude Skills Hub as submodule"
```

> **License:** This collection is licensed under [CC BY 4.0](LICENSE). You are free to use and adapt these skills, but **you must give credit** to this repo and its author. See [LICENSE](LICENSE) for details.

---

## Popular Skills

The most widely used and community-favorite skills. Start here.

| Skill | Description | Use Case |
|-------|-------------|----------|
| [`/frontend-design`](skills/popular/frontend-design.md) | Expert frontend designer with bold, modern aesthetics | Build stunning UIs that stand out |
| [`/ui-ux-pro-max`](skills/popular/ui-ux-pro-max.md) | Elite UI/UX — bento grids, glassmorphism, micro-interactions | Transform any interface to world-class |
| [`/web-artifacts-builder`](skills/popular/web-artifacts-builder.md) | Self-contained HTML artifacts with React + Tailwind | Create interactive demos and dashboards |
| [`/superpowers`](skills/popular/superpowers.md) | Engineering super-bundle: plan, review, test, debug, ship | All-in-one senior engineer mode |
| [`/deep-research`](skills/popular/deep-research.md) | Multi-step research with source analysis | Research any topic thoroughly |
| [`/code-guardian`](skills/popular/code-guardian.md) | Security scanning + code review with OWASP checks | Catch bugs and vulnerabilities |
| [`/test-driven-development`](skills/popular/test-driven-development.md) | Strict Red/Green/Refactor TDD workflow | Never write code without tests |
| [`/mcp-builder`](skills/popular/mcp-builder.md) | Build production-ready MCP servers | Extend Claude with custom tools |
| [`/skill-creator`](skills/popular/skill-creator.md) | Meta-skill — create new skills interactively | Build your own custom skills |
| [`/full-stack-feature`](skills/popular/full-stack-feature.md) | End-to-end feature: DB, API, frontend, tests | Ship complete features fast |
| [`/smart-debug`](skills/popular/smart-debug.md) | Systematic debugging with root cause analysis | Fix bugs intelligently |
| [`/performance-optimizer`](skills/popular/performance-optimizer.md) | Full-stack performance profiling and fixes | Make everything faster |
| [`/deploy-pilot`](skills/popular/deploy-pilot.md) | Deployment automation for any platform | Ship to production confidently |
| [`/algorithmic-art`](skills/popular/algorithmic-art.md) | Generative art with p5.js — fractals, particles, noise | Create beautiful generative visuals |
| [`/prompt-optimizer`](skills/popular/prompt-optimizer.md) | Optimize LLM prompts for quality and cost | Get better AI outputs |
| [`/docx`](skills/popular/docx.md) | Create and edit Word documents programmatically | Generate reports and proposals |
| [`/pdf`](skills/popular/pdf.md) | PDF extraction, creation, merging, splitting | Handle PDF workflows |
| [`/xlsx`](skills/popular/xlsx.md) | Excel with formulas, charts, pivot tables | Automate spreadsheet tasks |
| [`/pptx`](skills/popular/pptx.md) | PowerPoint with professional layouts | Create presentations from code |
| [`/webapp-testing`](skills/popular/webapp-testing.md) | Playwright-based web app testing | Test any web application |
| [`security-guidance`](skills/popular/security-guidance/) | Official Anthropic security hook plugin | Auto-warn about XSS, injection, eval, pickle |

> **Note:** `security-guidance` is a **plugin** (not a slash command). It uses hooks to automatically warn you about security vulnerabilities when editing files. See its [README](skills/popular/security-guidance/) for installation.

---

## All Categories

### Frontend Development (15 skills)

Build modern, responsive, accessible user interfaces.

| Skill | Description |
|-------|-------------|
| [`/react-component`](skills/frontend/react-component.md) | Production-ready React components with TypeScript and hooks |
| [`/vue-component`](skills/frontend/vue-component.md) | Vue 3 SFCs with Composition API and typed props/emits |
| [`/css-to-tailwind`](skills/frontend/css-to-tailwind.md) | Convert CSS/SCSS to Tailwind utility classes |
| [`/responsive-design`](skills/frontend/responsive-design.md) | Make layouts responsive across all breakpoints |
| [`/accessibility-audit`](skills/frontend/accessibility-audit.md) | WCAG 2.1 AA audit with automated fixes |
| [`/nextjs-app`](skills/frontend/nextjs-app.md) | Next.js App Router pages with SSR/SSG/ISR |
| [`/animation-creator`](skills/frontend/animation-creator.md) | CSS/Framer Motion animations with reduced-motion support |
| [`/design-system`](skills/frontend/design-system.md) | Design tokens, theming, and component library |
| [`/performance-audit`](skills/frontend/performance-audit.md) | Core Web Vitals optimization (LCP, FID, CLS) |
| [`/state-management`](skills/frontend/state-management.md) | Redux Toolkit, Zustand, Jotai, or Pinia setup |
| [`/form-builder`](skills/frontend/form-builder.md) | Complex forms with React Hook Form + Zod validation |
| [`/html-to-jsx`](skills/frontend/html-to-jsx.md) | Convert HTML to properly formatted JSX/TSX |
| [`/dark-mode`](skills/frontend/dark-mode.md) | Dark mode with system detection and smooth transitions |
| [`/svg-optimizer`](skills/frontend/svg-optimizer.md) | Optimize SVGs and convert to React components |
| [`/micro-frontend`](skills/frontend/micro-frontend.md) | Micro-frontend architecture with Module Federation |

### Backend Development (15 skills)

Build robust, scalable server-side applications.

| Skill | Description |
|-------|-------------|
| [`/rest-api`](skills/backend/rest-api.md) | RESTful APIs with validation, pagination, and error handling |
| [`/graphql-schema`](skills/backend/graphql-schema.md) | GraphQL schemas with resolvers and DataLoader |
| [`/auth-system`](skills/backend/auth-system.md) | JWT, OAuth2, session auth, 2FA implementation |
| [`/middleware-creator`](skills/backend/middleware-creator.md) | Express/Fastify/Koa/Django middleware |
| [`/caching-strategy`](skills/backend/caching-strategy.md) | Redis caching with invalidation and stampede prevention |
| [`/rate-limiter`](skills/backend/rate-limiter.md) | Rate limiting with sliding window and token bucket |
| [`/webhook-handler`](skills/backend/webhook-handler.md) | Secure webhook handlers with HMAC verification |
| [`/background-jobs`](skills/backend/background-jobs.md) | BullMQ/Celery/Sidekiq job processing |
| [`/error-handler`](skills/backend/error-handler.md) | Centralized error handling with custom error classes |
| [`/websocket-server`](skills/backend/websocket-server.md) | WebSocket server with rooms, auth, and scaling |
| [`/file-upload`](skills/backend/file-upload.md) | Secure file upload with S3/R2 storage |
| [`/email-service`](skills/backend/email-service.md) | Transactional email with SendGrid/Resend/SES |
| [`/microservice`](skills/backend/microservice.md) | Microservice scaffold with health checks and logging |
| [`/api-versioning`](skills/backend/api-versioning.md) | API versioning with deprecation and migration |
| [`/search-engine`](skills/backend/search-engine.md) | Full-text search with Elasticsearch/Meilisearch |

### Full Stack (10 skills)

End-to-end application development across the entire stack.

| Skill | Description |
|-------|-------------|
| [`/scaffold-app`](skills/fullstack/scaffold-app.md) | Scaffold full-stack apps (Next.js, Remix, Nuxt, SvelteKit) |
| [`/env-setup`](skills/fullstack/env-setup.md) | Environment config with validation and secrets management |
| [`/deployment-config`](skills/fullstack/deployment-config.md) | Deploy to Vercel, Netlify, Railway, Fly.io, or AWS |
| [`/monorepo-setup`](skills/fullstack/monorepo-setup.md) | Monorepo with Turborepo or Nx |
| [`/auth-flow`](skills/fullstack/auth-flow.md) | End-to-end auth: signup, login, OAuth, RBAC |
| [`/file-storage`](skills/fullstack/file-storage.md) | File storage with S3/R2, CDN, and presigned URLs |
| [`/payment-integration`](skills/fullstack/payment-integration.md) | Stripe checkout, subscriptions, and webhooks |
| [`/realtime-feature`](skills/fullstack/realtime-feature.md) | Real-time features with WebSockets/SSE |
| [`/internationalization`](skills/fullstack/internationalization.md) | i18n with locale detection and RTL support |
| [`/error-tracking`](skills/fullstack/error-tracking.md) | Sentry error tracking and performance monitoring |

### DevOps & Infrastructure (12 skills)

Automate deployments, infrastructure, and operations.

| Skill | Description |
|-------|-------------|
| [`/github-actions`](skills/devops/github-actions.md) | CI/CD workflows with matrix testing and caching |
| [`/dockerfile`](skills/devops/dockerfile.md) | Optimized multi-stage Dockerfiles |
| [`/kubernetes-manifest`](skills/devops/kubernetes-manifest.md) | K8s Deployments, Services, Ingress, HPA |
| [`/terraform-module`](skills/devops/terraform-module.md) | Terraform modules with state management |
| [`/nginx-config`](skills/devops/nginx-config.md) | Production Nginx with SSL and reverse proxy |
| [`/monitoring-setup`](skills/devops/monitoring-setup.md) | Prometheus + Grafana monitoring and alerting |
| [`/docker-compose`](skills/devops/docker-compose.md) | Docker Compose for dev and production |
| [`/helm-chart`](skills/devops/helm-chart.md) | Helm charts with multi-environment support |
| [`/ci-pipeline`](skills/devops/ci-pipeline.md) | GitLab CI, CircleCI, or Jenkins pipelines |
| [`/ssl-setup`](skills/devops/ssl-setup.md) | SSL/TLS with Let's Encrypt and auto-renewal |
| [`/log-aggregation`](skills/devops/log-aggregation.md) | Centralized logging with ELK or Loki+Grafana |
| [`/infrastructure-as-code`](skills/devops/infrastructure-as-code.md) | IaC with Terraform, Pulumi, or CloudFormation |

### Security (12 skills)

Protect your applications from vulnerabilities and attacks.

| Skill | Description |
|-------|-------------|
| [`/security-audit`](skills/security/security-audit.md) | OWASP Top 10 comprehensive security audit |
| [`/dependency-check`](skills/security/dependency-check.md) | CVE scanning for vulnerable dependencies |
| [`/auth-hardening`](skills/security/auth-hardening.md) | Harden authentication and session management |
| [`/input-validation`](skills/security/input-validation.md) | Input validation and sanitization |
| [`/secrets-scanner`](skills/security/secrets-scanner.md) | Scan for leaked API keys and credentials |
| [`/cors-config`](skills/security/cors-config.md) | Configure CORS for production |
| [`/csp-headers`](skills/security/csp-headers.md) | Content Security Policy setup |
| [`/penetration-test`](skills/security/penetration-test.md) | Guided penetration testing checklist |
| [`/encryption-setup`](skills/security/encryption-setup.md) | Encryption at rest and in transit |
| [`/oauth-setup`](skills/security/oauth-setup.md) | OAuth 2.0 / OpenID Connect implementation |
| [`/sql-injection-prevention`](skills/security/sql-injection-prevention.md) | SQL injection audit and prevention |
| [`/xss-prevention`](skills/security/xss-prevention.md) | XSS vulnerability prevention |

### Testing (12 skills)

Write better tests and ship with confidence.

| Skill | Description |
|-------|-------------|
| [`/unit-test`](skills/testing/unit-test.md) | Comprehensive unit tests with edge cases |
| [`/integration-test`](skills/testing/integration-test.md) | API and service integration tests |
| [`/e2e-test`](skills/testing/e2e-test.md) | Playwright/Cypress end-to-end tests |
| [`/test-coverage`](skills/testing/test-coverage.md) | Analyze coverage gaps and generate missing tests |
| [`/mock-generator`](skills/testing/mock-generator.md) | Type-safe mocks, stubs, and fixtures |
| [`/load-test`](skills/testing/load-test.md) | Load/stress testing with k6 or Artillery |
| [`/api-test`](skills/testing/api-test.md) | API endpoint test suites |
| [`/tdd-guide`](skills/testing/tdd-guide.md) | Red-Green-Refactor TDD workflow |
| [`/snapshot-test`](skills/testing/snapshot-test.md) | React/Vue component snapshot testing |
| [`/contract-test`](skills/testing/contract-test.md) | Consumer-driven contract tests with Pact |
| [`/visual-regression`](skills/testing/visual-regression.md) | Visual regression testing setup |
| [`/test-refactor`](skills/testing/test-refactor.md) | Refactor tests for readability |

### Code Quality (12 skills)

Write cleaner, more maintainable code.

| Skill | Description |
|-------|-------------|
| [`/code-review`](skills/code-quality/code-review.md) | Comprehensive code review with severity levels |
| [`/refactor`](skills/code-quality/refactor.md) | Apply refactoring patterns (extract, inline, decompose) |
| [`/lint-config`](skills/code-quality/lint-config.md) | ESLint, Prettier, Ruff, or Biome setup |
| [`/type-safety`](skills/code-quality/type-safety.md) | Add TypeScript types and fix type errors |
| [`/dead-code`](skills/code-quality/dead-code.md) | Find and remove unused code |
| [`/complexity-reducer`](skills/code-quality/complexity-reducer.md) | Reduce cyclomatic complexity |
| [`/naming-conventions`](skills/code-quality/naming-conventions.md) | Audit and fix naming conventions |
| [`/solid-principles`](skills/code-quality/solid-principles.md) | Refactor to follow SOLID principles |
| [`/design-patterns`](skills/code-quality/design-patterns.md) | Apply appropriate design patterns |
| [`/clean-architecture`](skills/code-quality/clean-architecture.md) | Restructure with clean architecture layers |
| [`/performance-profiler`](skills/code-quality/performance-profiler.md) | Profile and optimize performance bottlenecks |
| [`/dependency-cleanup`](skills/code-quality/dependency-cleanup.md) | Remove unused and outdated dependencies |

### Database (10 skills)

Design, optimize, and manage databases.

| Skill | Description |
|-------|-------------|
| [`/schema-design`](skills/database/schema-design.md) | Normalized schema design with ER diagrams |
| [`/migration-generator`](skills/database/migration-generator.md) | Database migrations with zero-downtime strategies |
| [`/query-optimizer`](skills/database/query-optimizer.md) | Analyze and optimize slow SQL queries |
| [`/seed-data`](skills/database/seed-data.md) | Generate realistic seed data |
| [`/orm-model`](skills/database/orm-model.md) | ORM models for Prisma, TypeORM, SQLAlchemy, Django |
| [`/index-advisor`](skills/database/index-advisor.md) | Suggest optimal database indexes |
| [`/nosql-schema`](skills/database/nosql-schema.md) | MongoDB, DynamoDB, Firestore schema design |
| [`/redis-setup`](skills/database/redis-setup.md) | Redis for caching, sessions, queues, pub/sub |
| [`/data-migration`](skills/database/data-migration.md) | ETL data migration with validation |
| [`/sql-builder`](skills/database/sql-builder.md) | Complex SQL from natural language |

### Documentation (10 skills)

Generate professional documentation effortlessly.

| Skill | Description |
|-------|-------------|
| [`/readme-generator`](skills/documentation/readme-generator.md) | Comprehensive README with badges and examples |
| [`/api-docs`](skills/documentation/api-docs.md) | OpenAPI 3.0/Swagger spec generation |
| [`/changelog-generator`](skills/documentation/changelog-generator.md) | Keep a Changelog from git history |
| [`/jsdoc-generator`](skills/documentation/jsdoc-generator.md) | JSDoc/TSDoc comments with proper tags |
| [`/architecture-docs`](skills/documentation/architecture-docs.md) | System architecture with Mermaid diagrams |
| [`/onboarding-guide`](skills/documentation/onboarding-guide.md) | Developer onboarding documentation |
| [`/runbook`](skills/documentation/runbook.md) | Operational incident response runbooks |
| [`/adr-generator`](skills/documentation/adr-generator.md) | Architecture Decision Records |
| [`/contributing-guide`](skills/documentation/contributing-guide.md) | CONTRIBUTING.md generation |
| [`/migration-guide`](skills/documentation/migration-guide.md) | Breaking change migration guides |

### Git & GitHub (10 skills)

Master version control and collaboration workflows.

| Skill | Description |
|-------|-------------|
| [`/commit-message`](skills/git-github/commit-message.md) | Conventional commit message generation |
| [`/pr-description`](skills/git-github/pr-description.md) | Detailed PR descriptions with checklists |
| [`/branch-strategy`](skills/git-github/branch-strategy.md) | Git Flow, GitHub Flow, or Trunk-based setup |
| [`/release-notes`](skills/git-github/release-notes.md) | Release notes from commits and PRs |
| [`/gitignore-generator`](skills/git-github/gitignore-generator.md) | Comprehensive .gitignore for any stack |
| [`/git-hooks`](skills/git-github/git-hooks.md) | Husky + lint-staged + commitlint setup |
| [`/merge-conflict`](skills/git-github/merge-conflict.md) | Intelligent merge conflict resolution |
| [`/repo-setup`](skills/git-github/repo-setup.md) | Initialize repos with all best practices |
| [`/changelog-from-git`](skills/git-github/changelog-from-git.md) | Changelog from conventional commits |
| [`/github-templates`](skills/git-github/github-templates.md) | Issue and PR templates |

### Mobile Development (10 skills)

Build cross-platform mobile applications.

| Skill | Description |
|-------|-------------|
| [`/react-native-component`](skills/mobile/react-native-component.md) | React Native components with TypeScript |
| [`/flutter-widget`](skills/mobile/flutter-widget.md) | Flutter widgets with Riverpod/BLoC |
| [`/app-navigation`](skills/mobile/app-navigation.md) | React Navigation / Go Router setup |
| [`/push-notifications`](skills/mobile/push-notifications.md) | FCM/APNs push notification integration |
| [`/offline-storage`](skills/mobile/offline-storage.md) | Offline-first data storage and sync |
| [`/app-store-listing`](skills/mobile/app-store-listing.md) | ASO-optimized app store descriptions |
| [`/deep-linking`](skills/mobile/deep-linking.md) | Universal links and deep linking |
| [`/mobile-auth`](skills/mobile/mobile-auth.md) | Biometric auth with secure token storage |
| [`/responsive-mobile`](skills/mobile/responsive-mobile.md) | Responsive layouts for all screen sizes |
| [`/app-performance`](skills/mobile/app-performance.md) | Mobile app performance optimization |

### AI & Machine Learning (10 skills)

Build intelligent applications with AI/ML.

| Skill | Description |
|-------|-------------|
| [`/prompt-engineering`](skills/ai-ml/prompt-engineering.md) | LLM prompt design with few-shot and CoT |
| [`/rag-setup`](skills/ai-ml/rag-setup.md) | RAG pipeline with vector stores and embeddings |
| [`/ml-pipeline`](skills/ai-ml/ml-pipeline.md) | ML training and inference pipelines |
| [`/data-preprocessing`](skills/ai-ml/data-preprocessing.md) | Dataset cleaning and feature engineering |
| [`/model-evaluation`](skills/ai-ml/model-evaluation.md) | ML model evaluation with metrics and bias detection |
| [`/chatbot-builder`](skills/ai-ml/chatbot-builder.md) | Conversational AI with tool use and streaming |
| [`/embeddings-setup`](skills/ai-ml/embeddings-setup.md) | Vector embeddings and similarity search |
| [`/ai-agent`](skills/ai-ml/ai-agent.md) | AI agents with ReAct pattern and tool use |
| [`/fine-tuning`](skills/ai-ml/fine-tuning.md) | Model fine-tuning with LoRA/QLoRA |
| [`/langchain-setup`](skills/ai-ml/langchain-setup.md) | LangChain/LlamaIndex pipeline setup |

### Marketing & SEO (10 skills)

Optimize for search engines and conversions.

| Skill | Description |
|-------|-------------|
| [`/seo-optimizer`](skills/marketing-seo/seo-optimizer.md) | Comprehensive SEO audit and optimization |
| [`/meta-tags`](skills/marketing-seo/meta-tags.md) | Meta tags, Open Graph, and Twitter Cards |
| [`/sitemap-generator`](skills/marketing-seo/sitemap-generator.md) | XML sitemap generation |
| [`/og-tags`](skills/marketing-seo/og-tags.md) | Open Graph tags for rich social previews |
| [`/landing-page`](skills/marketing-seo/landing-page.md) | High-converting landing page creation |
| [`/email-template`](skills/marketing-seo/email-template.md) | Responsive HTML email templates |
| [`/schema-markup`](skills/marketing-seo/schema-markup.md) | JSON-LD structured data markup |
| [`/analytics-setup`](skills/marketing-seo/analytics-setup.md) | Google Analytics 4 and event tracking |
| [`/a-b-testing`](skills/marketing-seo/a-b-testing.md) | A/B testing framework setup |
| [`/keyword-research`](skills/marketing-seo/keyword-research.md) | Keyword research and content strategy |

### Productivity (10 skills)

Work smarter and ship faster.

| Skill | Description |
|-------|-------------|
| [`/project-setup`](skills/productivity/project-setup.md) | New project with best practices configured |
| [`/env-debug`](skills/productivity/env-debug.md) | Debug environment and configuration issues |
| [`/dependency-update`](skills/productivity/dependency-update.md) | Safely update dependencies with changelog review |
| [`/error-debugger`](skills/productivity/error-debugger.md) | Systematic error debugging with root cause analysis |
| [`/code-explainer`](skills/productivity/code-explainer.md) | Explain complex code with diagrams |
| [`/regex-builder`](skills/productivity/regex-builder.md) | Build and test regex patterns step by step |
| [`/codebase-overview`](skills/productivity/codebase-overview.md) | Generate full codebase architecture overview |
| [`/tech-debt`](skills/productivity/tech-debt.md) | Identify and prioritize technical debt |
| [`/boilerplate-remover`](skills/productivity/boilerplate-remover.md) | Remove repetitive code and apply DRY |
| [`/workspace-setup`](skills/productivity/workspace-setup.md) | VS Code workspace and extension config |

### Creative & Design (10 skills)

Create visually stunning assets and designs.

| Skill | Description |
|-------|-------------|
| [`/svg-art`](skills/creative-design/svg-art.md) | SVG artwork, icons, and animated illustrations |
| [`/color-palette`](skills/creative-design/color-palette.md) | WCAG-compliant color palette generation |
| [`/ui-mockup`](skills/creative-design/ui-mockup.md) | HTML/CSS UI mockups and prototypes |
| [`/icon-set`](skills/creative-design/icon-set.md) | Consistent SVG icon set creation |
| [`/email-design`](skills/creative-design/email-design.md) | Responsive HTML email design |
| [`/presentation`](skills/creative-design/presentation.md) | HTML slide presentations with Reveal.js |
| [`/data-visualization`](skills/creative-design/data-visualization.md) | Charts and dashboards with D3/Chart.js |
| [`/ascii-art`](skills/creative-design/ascii-art.md) | ASCII art for CLI tools and banners |
| [`/css-effects`](skills/creative-design/css-effects.md) | Glassmorphism, gradients, parallax effects |
| [`/theme-generator`](skills/creative-design/theme-generator.md) | Complete UI theme generation with dark mode |

---

## How Skills Work

Each skill is a Markdown file with YAML frontmatter:

```markdown
---
description: What this skill does (shown in Claude Code's UI)
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

Detailed instructions that tell Claude exactly what to do
when this skill is invoked...
```

- **`description`** — Shown when browsing skills in Claude Code
- **`allowed-tools`** — Which Claude Code tools the skill can use
- **The body** — The prompt that activates when you use `/skill-name`

### Usage

Once installed, type `/` in Claude Code to see all available commands:

```
> /react-component
> /security-audit
> /unit-test
> /deploy-pilot
```

---

## Related Resources

Looking for more Claude Code tools? Check these out:

- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) — Curated list of Claude Code resources
- [awesome-claude-code-toolkit](https://github.com/rohitg00/awesome-claude-code-toolkit) — 135 agents, 35 skills, 42 commands
- [Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code) — Official documentation
- [obra/superpowers](https://github.com/obra/superpowers) — Battle-tested engineering skills
- [Trail of Bits Security Skills](https://github.com/trailofbits/skills) — Professional security-focused skills

---

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Quick steps:**
1. Fork this repo
2. Add your skill to the appropriate `skills/` folder
3. Submit a PR

---

## License

[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE)

You are free to use, share, and adapt these skills — but **you must give appropriate credit** to this repository and its author [@ShadmanSakibRahman](https://github.com/ShadmanSakibRahman).

---

<p align="center">
  <strong>Found this useful? Give it a star — it helps others discover the collection.</strong>
</p>
