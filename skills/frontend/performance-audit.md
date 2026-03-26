---
description: Audit frontend performance targeting Core Web Vitals with actionable optimization fixes
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in frontend performance optimization. When this skill is invoked, do the following:

1. Ask the user which pages or components to audit, or audit the entire frontend if not specified.
2. Read the project configuration and source files to assess performance:
   - Check `package.json` for bundle-relevant dependencies and their sizes
   - Read the build configuration (webpack, Vite, Next.js, Turbopack)
   - Identify the framework and rendering strategy (CSR, SSR, SSG, ISR)
   - Check for existing performance optimizations already in place

3. Audit each Core Web Vital and related metrics:

   **Largest Contentful Paint (LCP) - target under 2.5s:**
   - Identify the likely LCP element (hero image, main heading, large text block)
   - Check if LCP images use `priority`/`fetchpriority="high"` and `preload`
   - Verify LCP images are properly sized (not oversized and scaled down)
   - Check for render-blocking CSS and JS in `<head>`
   - Look for server response time issues (large server components, slow APIs)
   - Verify critical CSS is inlined or loaded with high priority

   **First Input Delay / Interaction to Next Paint (FID/INP) - target under 100ms/200ms:**
   - Search for long-running synchronous JavaScript on the main thread
   - Identify heavy event handlers (onClick, onChange) that do expensive work
   - Check for unoptimized re-renders in React (missing memo, missing keys, inline objects/functions)
   - Look for blocking third-party scripts (analytics, chat widgets, ad scripts)
   - Verify Web Workers are used for CPU-intensive operations

   **Cumulative Layout Shift (CLS) - target under 0.1:**
   - Check that all images and videos have explicit `width` and `height` or `aspect-ratio`
   - Look for dynamically injected content above the fold (ads, banners, cookie notices)
   - Verify fonts use `font-display: swap` with a size-adjusted fallback to minimize FOIT/FOUT shift
   - Check for content that shifts after client-side hydration
   - Ensure skeleton loaders match the final content dimensions

4. Analyze bundle size and code splitting:
   - Identify the largest dependencies and check for lighter alternatives (e.g., date-fns vs moment, preact vs react for simple apps)
   - Check for proper tree shaking (named imports vs namespace imports)
   - Verify dynamic imports (`React.lazy`, `next/dynamic`, `import()`) for below-the-fold content
   - Look for duplicate dependencies in the bundle
   - Check that source maps are not shipped to production
   - Recommend bundle analysis tools if not configured (`webpack-bundle-analyzer`, `source-map-explorer`)

5. Check image optimization:
   - Verify use of modern formats (WebP, AVIF) with fallbacks
   - Check that images are properly sized for their display dimensions (no 4000px images in 400px containers)
   - Verify lazy loading for below-the-fold images (`loading="lazy"`)
   - Check for responsive images with `srcset` and `sizes`
   - Ensure `next/image` or equivalent optimization is used

6. Audit caching and loading strategies:
   - Check `Cache-Control` headers for static assets (long-lived caching with content hashing)
   - Verify service worker or caching strategy for repeat visits
   - Check for `preconnect` to required origins (API servers, CDNs, font providers)
   - Verify `dns-prefetch` for third-party domains
   - Check for proper `preload` of critical resources (fonts, above-the-fold images)

7. Review rendering performance:
   - Identify unnecessary re-renders in React components (use React DevTools Profiler patterns)
   - Check for missing `useMemo`, `useCallback`, and `React.memo` on expensive computations or frequently re-rendered components
   - Look for virtualization needs in long lists (recommend `react-window` or `@tanstack/virtual`)
   - Check for layout thrashing (reading DOM properties then immediately writing)
   - Verify CSS containment (`contain: layout paint`) on complex UI sections

8. Generate a prioritized report with three categories:
   - **High Impact:** Changes that will noticeably improve metrics (image optimization, code splitting, render-blocking removal)
   - **Medium Impact:** Changes that improve specific scenarios (caching, font loading, lazy loading)
   - **Low Impact / Best Practices:** Incremental improvements (preconnect hints, minor bundle reductions)
9. For each finding, provide the specific file, the problem, and a concrete code change to fix it.

Best practices to follow:
- Measure before and after; do not optimize without data
- Focus on user-perceived performance, not just bundle metrics
- Prioritize above-the-fold content loading over total page weight
- Ship less JavaScript as the single highest-impact optimization
- Use progressive enhancement: pages should be usable before JS loads where possible

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
