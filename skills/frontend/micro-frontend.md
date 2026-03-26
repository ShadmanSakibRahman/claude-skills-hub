---
description: Set up micro-frontend architecture with Module Federation, shared dependencies, and routing
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in micro-frontend architecture. When this skill is invoked, do the following:

1. Ask the user about their requirements, or infer from context:
   - How many micro-apps/teams will exist
   - Whether they share a framework or use different ones
   - Deployment strategy (independent or coordinated)
   - Level of isolation needed between micro-apps
   - Shared UI requirements (common header, navigation, design system)

2. Read the existing project to understand the current setup:
   - Check the build tool (Webpack 5, Vite, Next.js, Rspack)
   - Identify the framework(s) in use
   - Understand the current routing structure
   - Check for monorepo tooling (Nx, Turborepo, Lerna, pnpm workspaces)

3. Recommend the right micro-frontend approach:

   **Module Federation (Webpack 5 / Rspack)** - Best for React/Vue apps with Webpack:
   - Set up a host (shell) application that orchestrates micro-apps
   - Configure each micro-app as a remote with exposed modules
   - Define shared dependencies with version constraints to avoid duplication
   - Handle async loading of remote modules with Suspense and error boundaries

   **Vite Module Federation** - Best for Vite-based projects:
   - Use `@originjs/vite-plugin-federation` or `@module-federation/vite`
   - Configure remotes and exposes in Vite config
   - Handle HMR across federated modules

   **Single-SPA** - Best for polyglot (multi-framework) architectures:
   - Set up the root config (orchestrator) with registered applications
   - Create single-spa parcels for each micro-app
   - Define activity functions for route-based activation
   - Handle framework-specific adapters (single-spa-react, single-spa-vue, single-spa-angular)

   **iframe-based** - Best for maximum isolation:
   - Set up iframe containers with proper sizing and communication
   - Implement cross-frame messaging with `postMessage` and typed message contracts
   - Handle shared authentication via tokens passed through postMessage
   - Manage navigation synchronization between host and iframe

4. Set up the shell (host) application:
   - Create the application shell with shared layout (header, navigation, footer)
   - Implement a routing strategy that delegates to micro-apps:
     - Route-based: each micro-app owns a URL prefix (e.g., `/dashboard/*`, `/settings/*`)
     - Component-based: micro-apps are embedded as components within host pages
   - Add a micro-app registry that maps routes to remote entry points
   - Implement loading states with skeletons while micro-apps load
   - Add error boundaries that gracefully handle micro-app failures without crashing the shell
   - Set up a fallback UI when a micro-app is unavailable

5. Configure shared dependencies to avoid duplication:
   - Share framework packages as singletons (`react`, `react-dom`, `vue`)
   - Share the design system / component library
   - Share state management library if cross-app state is needed
   - Set version requirements with `requiredVersion` to prevent incompatibilities
   - Use `eager: true` for dependencies the shell needs immediately
   - Mark shared libraries as `singleton: true` to prevent multiple instances
   - Define a shared package policy document listing all shared dependencies and their version ranges

6. Implement cross-app communication:
   - **Custom Events:** Use `CustomEvent` for loosely coupled broadcasts (notifications, theme changes)
   - **Shared State:** Use a lightweight event bus or shared Zustand/Redux store for state that multiple micro-apps need
   - **URL/Query Params:** Pass context through the URL for navigation-driven communication
   - **Props/Callbacks:** Pass data directly when one micro-app renders another as a component
   - Define a typed communication contract (TypeScript interfaces) shared across all micro-apps
   - Avoid tight coupling: micro-apps should function independently even if communication fails

7. Handle shared authentication and authorization:
   - Implement auth in the shell application
   - Pass auth tokens to micro-apps via shared module, custom events, or props
   - Handle token refresh centrally in the shell
   - Ensure micro-apps can verify auth state independently for security
   - Implement logout that cleans up all micro-app state

8. Set up development workflow:
   - Configure each micro-app to run independently with its own dev server
   - Set up a development mode where the shell loads local micro-apps instead of deployed ones
   - Create a shared TypeScript types package for cross-app contracts
   - Set up CI/CD pipelines for independent deployment of each micro-app
   - Add integration tests that verify micro-apps work together in the shell

9. Plan deployment strategy:
   - Each micro-app deploys independently to its own CDN path or container
   - The shell references micro-apps by URL (configurable per environment)
   - Implement versioned remote entry points for rollback capability
   - Set up canary deployments for safe rollouts of individual micro-apps
   - Configure CORS headers for cross-origin module loading
   - Set appropriate caching headers (short TTL for remote entry, long TTL for chunks)

Best practices to follow:
- Keep the shell thin: it handles layout, routing, and auth, nothing else
- Each micro-app must be independently deployable, testable, and developable
- Share as little as possible; over-sharing creates coupling that defeats the purpose
- Define clear ownership boundaries: one team owns one micro-app
- Use TypeScript interfaces for all cross-app contracts
- Test micro-apps both in isolation and integrated in the shell
- Monitor bundle sizes per micro-app; the sum should not exceed a reasonable monolith
- Document the architecture, communication patterns, and shared dependency policy
- Plan for graceful degradation: if one micro-app fails, the rest should still work

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
