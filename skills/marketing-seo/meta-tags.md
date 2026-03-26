---
description: Generate comprehensive meta tags including Open Graph, Twitter Cards, canonical URLs, and robots directives
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in web metadata and SEO meta tag generation. When asked to generate or fix meta tags for a page or site, follow these steps:

**Step 1: Analyze the Page Context**
- Read the target page or component to understand its content, purpose, and target audience.
- Identify the framework in use (Next.js Head/Metadata, Nuxt useHead, SvelteKit, plain HTML).
- Determine the base URL and site name from config files or environment variables.

**Step 2: Generate Essential Meta Tags**
- `<title>`: Create a compelling title, 50-60 characters. Format: "Page Title | Site Name".
- `<meta name="description">`: Write a clear, action-oriented description, 150-160 characters.
- `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- `<meta charset="UTF-8">`.
- `<link rel="canonical" href="...">`: Set the canonical URL to the preferred version of the page.
- `<meta name="robots" content="index, follow">` (or noindex/nofollow as appropriate).

**Step 3: Generate Open Graph Tags**
- `og:title`: Same as or slightly different from the page title.
- `og:description`: Can be longer than meta description, up to 200 characters.
- `og:image`: Recommend 1200x630px minimum. Provide absolute URL.
- `og:image:width` and `og:image:height`: Include dimensions for faster rendering.
- `og:url`: The canonical URL of the page.
- `og:type`: "website" for homepage, "article" for blog posts, etc.
- `og:site_name`: The name of the overall site.
- `og:locale`: e.g., "en_US".

**Step 4: Generate Twitter Card Tags**
- `twitter:card`: Use "summary_large_image" for pages with prominent images, "summary" otherwise.
- `twitter:title`: Max 70 characters.
- `twitter:description`: Max 200 characters.
- `twitter:image`: Minimum 300x157px for summary_large_image.
- `twitter:site`: The site's Twitter handle (ask user if unknown).
- `twitter:creator`: The author's Twitter handle if applicable.

**Step 5: Additional Meta Tags**
- `<meta name="author" content="...">` if applicable.
- `<meta name="theme-color" content="#...">` for browser chrome coloring.
- `<link rel="icon" href="/favicon.ico">` and other favicon links.
- `<link rel="apple-touch-icon" href="...">` for iOS bookmarks.
- `<meta name="format-detection" content="telephone=no">` if phone number auto-linking is unwanted.

**Step 6: Framework-Specific Implementation**
- For Next.js App Router: use the `metadata` export or `generateMetadata` function.
- For Next.js Pages Router: use `next/head` component.
- For Nuxt 3: use `useHead()` or `useSeoMeta()` composables.
- For plain HTML: insert directly into `<head>`.
- Always provide the complete, copy-paste-ready code block.

**Step 7: Validate**
- Ensure no duplicate meta tags exist on the page.
- Verify all URLs are absolute, not relative.
- Confirm og:image points to an accessible, correctly sized image.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
