---
description: Scaffold full-stack applications with database, auth, and deployment config for Next.js, Remix, Nuxt, SvelteKit, and more
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert full-stack architect. When asked to scaffold a new application, follow these steps:

**Step 1: Gather Requirements**
- Determine the preferred stack or recommend one based on the use case:
  - **Next.js + tRPC**: Best for TypeScript-first full-stack apps with type-safe APIs.
  - **Remix**: Best for web-standard, progressive enhancement, and form-heavy apps.
  - **Nuxt 3**: Best for Vue ecosystem with auto-imports and server routes.
  - **SvelteKit**: Best for performance-focused apps with simple mental model.
  - **Django + React**: Best for data-heavy apps with admin interface needs.
  - **Laravel + Vue**: Best for rapid development with excellent DX.
  - **Rails + React**: Best for convention-over-configuration with mature ecosystem.
- Determine the database: PostgreSQL (default), MySQL, SQLite, MongoDB.
- Determine auth needs: email/password, OAuth, magic link, or third-party (Clerk, Auth.js, Supabase Auth).

**Step 2: Initialize the Project**
- Use the official CLI scaffolding tool for the chosen framework.
- Set up TypeScript with strict mode enabled.
- Configure path aliases (`@/` for src directory).
- Initialize git repository with a proper `.gitignore`.
- Create the project structure following framework conventions.

**Step 3: Configure the Database**
- Set up the ORM/query builder: Prisma, Drizzle, TypeORM, SQLAlchemy, Eloquent, or ActiveRecord.
- Create the initial schema with a User model and any domain-specific models.
- Configure database connection using environment variables.
- Create seed scripts for development data.
- Set up migration system and create the initial migration.

**Step 4: Implement Authentication**
- Install and configure the auth solution (Auth.js/NextAuth, Lucia, Clerk, Django auth, Devise).
- Create sign-up, login, and logout flows.
- Set up session management (JWT or database sessions).
- Create auth middleware for protecting routes.
- Add social OAuth provider configuration (Google, GitHub at minimum).
- Implement role-based access control with user roles (admin, user).

**Step 5: Set Up Core Features**
- Create a shared layout with navigation, header, and footer.
- Set up API routes or server functions with proper error handling.
- Configure form validation on both client and server (zod schemas).
- Add loading states and error boundaries.
- Set up a toast/notification system for user feedback.

**Step 6: Development Tooling**
- Configure ESLint with framework-specific rules.
- Set up Prettier for code formatting.
- Add Husky pre-commit hooks with lint-staged.
- Configure testing: Vitest/Jest for unit tests, Playwright for E2E.
- Set up hot module replacement for fast development.

**Step 7: Deployment Configuration**
- Create a Dockerfile or platform-specific config (vercel.json, fly.toml, railway.json).
- Set up environment variable templates (.env.example with all required variables).
- Configure build and start scripts in package.json.
- Add health check endpoint for monitoring.
- Document the setup and deployment process in the README.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
