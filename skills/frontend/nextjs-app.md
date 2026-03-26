---
description: Scaffold Next.js App Router pages with metadata, loading/error states, and data fetching
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert Next.js developer specializing in the App Router (Next.js 13+). When this skill is invoked, do the following:

1. Ask the user what page or feature to scaffold, or infer from context.
2. Read the existing project structure to understand conventions:
   - Check `next.config.js`/`next.config.ts` for configuration
   - Identify the `app/` directory structure and existing route patterns
   - Check for shared layouts, middleware, and route groups
   - Identify data fetching patterns (Server Components, `fetch`, Prisma, tRPC, etc.)
   - Note the styling approach and component library in use
3. Create the route directory and necessary files:

   **page.tsx** (the main page component):
   - Default to Server Component unless client interactivity is required
   - Add `"use client"` directive only for components that need browser APIs, hooks, or event handlers
   - Implement data fetching directly in the component using `async/await` for Server Components
   - Add proper TypeScript types for params and searchParams
   - Use `generateStaticParams` for static routes with dynamic segments

   **layout.tsx** (if a new layout scope is needed):
   - Accept `children` prop with proper typing
   - Add shared UI elements (sidebar, sub-navigation) scoped to this route segment
   - Fetch shared data that child routes need

   **loading.tsx** (loading UI):
   - Create a meaningful skeleton/shimmer UI that matches the page layout
   - Use proper ARIA attributes (`aria-busy`, `aria-live="polite"`)
   - Avoid generic spinners; match the content structure for reduced layout shift

   **error.tsx** (error boundary):
   - Mark as `"use client"` (required by Next.js)
   - Accept `error` and `reset` props
   - Display a user-friendly error message with a retry button
   - Log the error for debugging without exposing details to users

   **not-found.tsx** (404 handling):
   - Create if the route might receive invalid dynamic params
   - Provide helpful navigation back to valid pages

4. Implement proper metadata for SEO:
   - Use `generateMetadata` for dynamic metadata based on route params
   - Include `title`, `description`, `openGraph`, `twitter` card metadata
   - Add `robots` configuration for pages that should not be indexed
   - Set canonical URLs for pages with multiple access paths
   - Use the `metadata` export for static metadata on simple pages

5. Set up data fetching with the appropriate strategy:
   - **SSR (dynamic):** Use `export const dynamic = 'force-dynamic'` or `{ cache: 'no-store' }` for real-time data
   - **SSG (static):** Use `generateStaticParams` with `export const dynamicParams = false` for known routes
   - **ISR (revalidation):** Use `export const revalidate = 3600` or `{ next: { revalidate: 3600 } }` for time-based revalidation
   - Use `revalidatePath` or `revalidateTag` in Server Actions for on-demand revalidation
6. Separate server and client concerns:
   - Keep data fetching and sensitive logic in Server Components
   - Extract interactive pieces into separate Client Components with `"use client"`
   - Pass server data to client components as serializable props
   - Use Server Actions for mutations (form submissions, data updates)
7. Add route handlers (`route.ts`) for API endpoints if the feature needs them:
   - Handle proper HTTP methods (GET, POST, PUT, DELETE)
   - Add input validation and error handling
   - Return appropriate status codes and JSON responses
8. Implement middleware if the route needs authentication, redirects, or headers.

Best practices to follow:
- Prefer Server Components for everything that does not need interactivity
- Colocate components, utilities, and types within the route directory
- Use parallel routes (`@slot`) and intercepting routes (`(.)`) where they simplify UX
- Streaming with Suspense boundaries for progressive page loading
- Never expose environment variables or secrets in Client Components
- Use `next/image` for all images, `next/link` for all navigation
- Add proper error boundaries at each route segment level

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
