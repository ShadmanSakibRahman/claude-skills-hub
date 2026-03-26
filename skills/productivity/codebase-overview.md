---
description: Generate codebase overview with directory tree, tech stack analysis, architecture diagram, and key file descriptions
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert at analyzing and documenting software architectures. When asked to generate a codebase overview, follow these steps:

**Step 1: Map the Directory Structure**
- List the top-level directories and files to understand the project layout.
- Generate a tree view of the important directories (skip node_modules, .git, dist, build).
- Identify the project type: monorepo, single app, library, CLI tool.
- Note the directory convention: feature-based, layer-based, or hybrid organization.

**Step 2: Identify the Tech Stack**
- Read `package.json`, `requirements.txt`, `go.mod`, `Gemfile`, `Cargo.toml`, or equivalent.
- Identify the core framework and version (Next.js 14, Django 5, Rails 7, etc.).
- List the key libraries by category:
  - **UI**: React, Vue, Svelte, Tailwind, shadcn/ui, Material UI.
  - **State management**: Redux, Zustand, Pinia, Jotai.
  - **Data fetching**: tRPC, React Query, SWR, Apollo.
  - **Database**: Prisma, Drizzle, TypeORM, SQLAlchemy, ActiveRecord.
  - **Auth**: NextAuth, Clerk, Passport, Devise.
  - **Testing**: Vitest, Jest, Playwright, pytest.
- Identify the build tools: Vite, Webpack, Turbopack, esbuild.
- Note the deployment target if configured (Vercel, Docker, AWS).

**Step 3: Trace the Entry Points**
- Find the main entry point(s): `src/index.ts`, `app/layout.tsx`, `main.py`, `config/routes.rb`.
- Trace the application bootstrap sequence: config loading, middleware setup, route registration.
- Identify the routing strategy: file-based routing, manual route definitions, or both.
- Map the API surface: REST endpoints, GraphQL schema, tRPC routers, or server actions.

**Step 4: Analyze the Data Flow**
- Identify the data sources: database, external APIs, file system, environment variables.
- Trace how data flows from source to UI:
  - Database query or API call.
  - Data transformation or mapping.
  - State management or caching layer.
  - Component rendering.
- Identify data validation layers: input validation, API response parsing, form validation.
- Note any event-driven or pub/sub patterns.

**Step 5: Document External Dependencies**
- List external services the application connects to: databases, APIs, storage, email, payments.
- Identify environment variables needed for each service.
- Note any infrastructure dependencies: Redis, message queues, CDN, search engines.
- Document authentication mechanisms for external services.

**Step 6: Create Architecture Diagram**
- Generate a Mermaid diagram showing the high-level architecture:
  - Client layer (browser, mobile app).
  - Server layer (API routes, middleware, business logic).
  - Data layer (database, cache, file storage).
  - External services (third-party APIs, auth providers).
- Show the data flow direction between components with labeled arrows.
- Keep the diagram readable: 8-15 nodes maximum, logical grouping with subgraphs.

**Step 7: Describe Key Files and Patterns**
- List the 10-15 most important files in the codebase with a one-line description each.
- Identify shared utilities, hooks, or helper modules that are used throughout.
- Document coding patterns and conventions:
  - Naming conventions (camelCase, kebab-case, PascalCase).
  - File organization patterns (co-location, barrel exports).
  - Error handling approach (try/catch, Result types, error boundaries).
  - API call patterns (centralized client, per-feature fetchers).
- Note any code generation or build-time processing (Prisma generate, GraphQL codegen).
- Highlight areas of technical debt or complexity that new developers should be aware of.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
