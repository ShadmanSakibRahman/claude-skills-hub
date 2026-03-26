---
description: Set up monorepo with Turborepo or Nx including shared packages, build pipeline, and CI caching
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in monorepo architecture and build systems. When asked to set up a monorepo, follow these steps:

**Step 1: Choose the Monorepo Tool**
- **Turborepo**: Best for JavaScript/TypeScript projects. Simple config, great caching, Vercel integration.
- **Nx**: Best for large teams and polyglot repos. Rich plugin ecosystem, computation caching, affected commands.
- **pnpm workspaces**: Lightweight option when you just need shared dependencies without a build orchestrator.
- Determine the package manager: pnpm (recommended for monorepos), npm, or yarn.

**Step 2: Create the Workspace Structure**
```
root/
  apps/           # Deployable applications
    web/           # Main web app (Next.js, Remix, etc.)
    api/           # Backend API server
    mobile/        # Mobile app (React Native, Expo)
  packages/        # Shared libraries
    ui/            # Shared UI component library
    config/        # Shared ESLint, TypeScript, Tailwind configs
    db/            # Database schema and client (Prisma/Drizzle)
    utils/         # Shared utility functions
    types/         # Shared TypeScript types/interfaces
  turbo.json       # Turborepo pipeline config (or nx.json)
  package.json     # Root workspace config
  pnpm-workspace.yaml
```
- Create the root `package.json` with workspace definitions.
- Create `pnpm-workspace.yaml` (or equivalent) listing `apps/*` and `packages/*`.

**Step 3: Configure Shared Packages**
- Each package gets its own `package.json` with a scoped name (e.g., `@myapp/ui`).
- Set up TypeScript project references for cross-package type checking.
- Create a shared `tsconfig.base.json` in root that all packages extend.
- Configure shared ESLint and Prettier configs as a `@myapp/config` package.
- Set up path aliases so packages can import each other: `@myapp/ui`, `@myapp/utils`.

**Step 4: Configure the Build Pipeline**
For Turborepo (`turbo.json`):
- Define `pipeline` with tasks: build, lint, test, type-check, dev.
- Set proper `dependsOn` for build order (e.g., `build` depends on `^build` for dependencies).
- Configure `outputs` for each task to enable caching (e.g., `[".next/**", "dist/**"]`).
- Set up `globalDependencies` for env files and root configs.

For Nx (`nx.json`):
- Define target defaults for build, serve, lint, and test.
- Configure `namedInputs` for production and default file sets.
- Set up project graph dependencies via `implicitDependencies`.
- Enable Nx Cloud for distributed caching.

**Step 5: Dependency Management**
- Use the workspace protocol for internal dependencies: `"@myapp/ui": "workspace:*"`.
- Hoist shared devDependencies to the root to reduce duplication.
- Configure tool-specific versions at the root (TypeScript, ESLint, Prettier).
- Use `syncpack` or `manypkg` to keep dependency versions consistent across packages.
- Pin exact versions for critical dependencies.

**Step 6: Selective Builds and CI Caching**
- Configure CI to only build/test affected packages on each commit.
- For Turborepo: use `turbo run build --filter=...[HEAD~1]` for affected-only builds.
- For Nx: use `nx affected --target=build` for change-based builds.
- Set up remote caching (Vercel Remote Cache for Turbo, Nx Cloud for Nx).
- Cache `node_modules` and build outputs in CI (GitHub Actions cache, etc.).
- Create a GitHub Actions workflow that runs lint, type-check, test, and build with proper caching.

**Step 7: Developer Experience**
- Create root-level scripts for common tasks: `dev`, `build`, `lint`, `test`.
- Set up a `dev` script that starts all apps and watches all packages simultaneously.
- Add a CONTRIBUTING.md explaining how to add new apps and packages.
- Configure VS Code workspace settings for multi-root workspace support.
- Set up changesets or conventional commits for versioning shared packages.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
