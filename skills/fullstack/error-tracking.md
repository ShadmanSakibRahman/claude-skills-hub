---
description: Set up Sentry error tracking with source maps, release tracking, performance monitoring, and alerting
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in application monitoring and error tracking. When asked to set up error tracking, follow these steps:

**Step 1: Install and Initialize Sentry**
- Install the appropriate Sentry SDK for the framework:
  - Next.js: `@sentry/nextjs` (includes automatic instrumentation).
  - React: `@sentry/react`.
  - Vue: `@sentry/vue`.
  - Node.js: `@sentry/node`.
  - Python/Django: `sentry-sdk`.
- Configure environment variables: `SENTRY_DSN`, `SENTRY_ORG`, `SENTRY_PROJECT`, `SENTRY_AUTH_TOKEN`.
- Initialize Sentry as early as possible in the application lifecycle.
- Set the environment tag: `development`, `staging`, `production`.
- Configure the sample rate: 1.0 for errors (capture all), 0.1-0.2 for performance traces.

**Step 2: Framework-Specific Configuration**
For Next.js (`next.config.js` with `withSentryConfig`):
- Create `sentry.client.config.ts` and `sentry.server.config.ts`.
- Configure `instrumentation.ts` for server-side initialization.
- Set up the Sentry webpack plugin for automatic source map upload.
- Configure `tunnelRoute` to avoid ad blockers.

For other frameworks:
- Wrap the app root with `Sentry.ErrorBoundary` or equivalent.
- Set up the Sentry browser tracing integration for performance monitoring.
- Configure the backend SDK with request handler middleware.

**Step 3: Source Maps Upload**
- Configure the build process to generate and upload source maps to Sentry.
- Use the Sentry webpack/vite/rollup plugin or `sentry-cli` for upload.
- Associate source maps with releases using `SENTRY_RELEASE` (use git commit SHA).
- Delete source maps from the production build after upload (they should not be publicly accessible).
- Verify source maps are correctly linked by checking the Sentry "Artifacts" tab.

**Step 4: Error Context and Grouping**
- Set user context on login: `Sentry.setUser({ id, email, username })`.
- Clear user context on logout: `Sentry.setUser(null)`.
- Add breadcrumbs for key user actions: navigation, button clicks, API calls.
- Use `Sentry.setTag()` for filterable metadata: feature_flag, subscription_plan, locale.
- Use `Sentry.setExtra()` for additional debug data on specific errors.
- Customize error fingerprinting for better grouping when default grouping is too broad or narrow.

**Step 5: Release Tracking**
- Configure releases to match deployment versions (git SHA or semantic version).
- Set up commit tracking: associate Sentry releases with git commits for suspect commits.
- Configure deploy notifications so Sentry knows which release is in which environment.
- Use release health monitoring to track crash-free sessions and users.
- Mark releases as resolved or regressed to track issue recurrence.

**Step 6: Performance Monitoring**
- Enable tracing with appropriate sample rate (start with 0.1, adjust based on volume).
- Track key transactions: page loads, API endpoints, background jobs.
- Set up custom spans for database queries, external API calls, and complex operations.
- Configure performance thresholds and alerts for transaction duration.
- Monitor Web Vitals: LCP, FID, CLS, TTFB automatically captured by the browser SDK.

**Step 7: Alerts and User Feedback**
- Configure alert rules in Sentry:
  - New issue alert: notify immediately on first occurrence.
  - Regression alert: notify when a resolved issue recurs.
  - Spike alert: notify when error frequency exceeds a threshold.
- Set up notification channels: email, Slack, PagerDuty, or webhook.
- Implement the Sentry user feedback widget for users to report additional context on errors.
- Create a custom error page that captures user feedback and sends it to Sentry.
- Assign issue ownership rules based on file paths or error tags so alerts reach the right team.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
