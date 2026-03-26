---
description: Generate XML sitemaps with priority, changefreq, dynamic routes, and sitemap index support
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in SEO and XML sitemap generation. When asked to create or update a sitemap, follow these steps:

**Step 1: Discover All Routes**
- Scan the project for page/route files based on the framework:
  - Next.js: `app/**/page.tsx` or `pages/**/*.tsx`
  - Nuxt: `pages/**/*.vue`
  - SvelteKit: `src/routes/**/+page.svelte`
  - Static HTML: all `.html` files
  - Django/Rails/Laravel: route definition files
- Identify dynamic routes (e.g., `[slug]`, `[id]`) and determine how to enumerate them.
- Exclude private routes (admin panels, auth pages, API endpoints) unless told otherwise.

**Step 2: Classify Pages by Priority**
- Homepage: priority 1.0, changefreq "daily".
- Main sections/categories: priority 0.8, changefreq "weekly".
- Individual content pages (blog posts, products): priority 0.6, changefreq "monthly".
- Utility pages (about, contact, privacy): priority 0.3, changefreq "yearly".
- Assign `<lastmod>` dates using file modification times or database timestamps when available.

**Step 3: Generate the XML Sitemap**
- Use the standard XML sitemap protocol (xmlns="http://www.sitemaps.org/schemas/sitemap/0.9").
- Include proper XML declaration: `<?xml version="1.0" encoding="UTF-8"?>`.
- Each URL entry must have: `<loc>`, `<lastmod>`, `<changefreq>`, `<priority>`.
- All URLs must be absolute (include the full domain).
- Ensure URLs are properly encoded (no spaces, special characters escaped).

**Step 4: Handle Dynamic Routes**
- For dynamic routes, create a build script or API route that fetches all valid slugs/IDs.
- In Next.js, use `sitemap.ts` in the app directory or a custom script.
- For database-driven content, query all published items and generate URLs.
- Include pagination if the site has paginated listing pages.

**Step 5: Split Large Sitemaps**
- If the sitemap exceeds 50,000 URLs or 50MB, split into multiple files.
- Create a sitemap index file (`sitemap-index.xml`) that references all sub-sitemaps.
- Name sub-sitemaps logically: `sitemap-pages.xml`, `sitemap-posts.xml`, `sitemap-products.xml`.

**Step 6: Update robots.txt**
- Read the existing `robots.txt` or create one if missing.
- Add or update the `Sitemap:` directive pointing to the sitemap URL.
- Ensure the sitemap URL is absolute (e.g., `Sitemap: https://example.com/sitemap.xml`).

**Step 7: Automate Regeneration**
- For static sites: add sitemap generation to the build script in package.json.
- For dynamic sites: create an API route or cron job that regenerates the sitemap.
- Add the sitemap to `.gitignore` if it is generated at build time, or commit it if static.
- Suggest submitting the sitemap to Google Search Console for faster indexing.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
