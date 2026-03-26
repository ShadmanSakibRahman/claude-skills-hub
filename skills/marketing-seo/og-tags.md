---
description: Generate Open Graph and Twitter Card tags for rich social media previews
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in social media optimization and Open Graph protocol. When asked to create or fix OG/Twitter tags for rich social previews, follow these steps:

**Step 1: Assess Current State**
- Read the target page/component and check for existing OG and Twitter meta tags.
- Identify the framework and how meta tags are managed (Head component, metadata export, useHead).
- Determine the site's base URL from environment config or hardcoded values.
- Check if an OG image already exists or needs to be created.

**Step 2: Generate Open Graph Tags**
- `og:title`: Compelling, 60-90 characters. Should entice clicks when shared.
- `og:description`: Summarize the page value, 100-200 characters. Include a call to action.
- `og:image`: Must be an absolute URL. Recommended size: 1200x630px (1.91:1 ratio).
- `og:image:width`: Set to 1200 (or actual width).
- `og:image:height`: Set to 630 (or actual height).
- `og:image:alt`: Descriptive alt text for the image.
- `og:url`: Canonical URL of the page.
- `og:type`: Use "website" for homepages, "article" for blog posts, "product" for product pages.
- `og:site_name`: The brand or site name.
- `og:locale`: Primary locale (e.g., "en_US"). Add `og:locale:alternate` for multilingual sites.

**Step 3: Generate Twitter Card Tags**
- `twitter:card`: Use "summary_large_image" (800x418px min) for visual content, "summary" (144x144px min) for text-heavy pages.
- `twitter:title`: Max 70 characters, can differ from og:title.
- `twitter:description`: Max 200 characters.
- `twitter:image`: Same as og:image or a Twitter-optimized version (2:1 ratio, max 5MB).
- `twitter:site`: The brand's Twitter/X handle (e.g., "@mybrand").
- `twitter:creator`: The content author's handle if applicable.

**Step 4: Platform-Specific Considerations**
- Facebook/Meta: Uses OG tags. Image minimum 200x200px, recommended 1200x630px.
- LinkedIn: Uses OG tags. Image recommended 1200x627px. Supports og:article:author.
- Pinterest: Add `<meta name="pinterest-rich-pin" content="true">` if applicable.
- Slack: Uses OG tags. Ensure og:image is under 500KB for inline preview.
- Discord: Uses OG tags. Supports `og:video` for video embeds.
- WhatsApp: Uses OG tags. Image must be at least 300x200px.

**Step 5: Dynamic OG Image Generation (if needed)**
- For Next.js: suggest using `@vercel/og` or `next/og` ImageResponse API.
- For other frameworks: suggest using a serverless function with Satori or Puppeteer.
- Include the page title, site branding, and relevant visuals in the generated image.
- Cache generated images to avoid regeneration on every request.

**Step 6: Implement in the Codebase**
- Write the complete meta tag code using the project's framework conventions.
- For multi-page sites, create a reusable SEO/OG component that accepts props.
- Set sensible defaults that can be overridden per-page.
- Ensure tags are in the `<head>` section and server-rendered (not client-only).

**Step 7: Validation Guidance**
- Suggest testing with Facebook Sharing Debugger, Twitter Card Validator, and LinkedIn Post Inspector.
- Remind the user to clear cached previews after updating tags.
- Verify that og:image URL is publicly accessible (not behind auth or localhost).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
