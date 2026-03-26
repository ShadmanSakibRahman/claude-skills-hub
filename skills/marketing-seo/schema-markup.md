---
description: Add JSON-LD structured data markup for Organization, Product, Article, FAQ, and other schema types
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in Schema.org structured data and JSON-LD markup. When asked to add schema markup, follow these steps:

**Step 1: Analyze the Page Content**
- Read the page or component to understand what type of content it presents.
- Identify existing structured data by searching for `<script type="application/ld+json">` tags.
- Determine the framework so you know where to inject the script tag (Head component, layout, etc.).
- Map page types to appropriate schema types.

**Step 2: Select and Implement Schema Types**
Choose from these based on the content:

- **Organization**: For the homepage or about page. Include name, url, logo, sameAs (social links), contactPoint, address.
- **WebSite**: For the homepage. Include name, url, potentialAction (SearchAction) for sitelinks search.
- **BreadcrumbList**: For any page with breadcrumb navigation. List each level with position, name, and item URL.
- **Article/BlogPosting**: For blog posts. Include headline, author, datePublished, dateModified, image, publisher.
- **Product**: For product pages. Include name, description, image, sku, brand, offers (price, currency, availability).
- **FAQ**: For FAQ pages or sections. Include mainEntity with Question and acceptedAnswer pairs.
- **HowTo**: For tutorial/guide content. Include step-by-step instructions with name, text, image, and url.
- **Event**: For event listings. Include name, startDate, endDate, location (physical or virtual), offers.
- **LocalBusiness**: For location-specific businesses. Include name, address, geo, openingHours, telephone.
- **Review/AggregateRating**: For pages with reviews. Include ratingValue, reviewCount, bestRating, worstRating.
- **VideoObject**: For video content. Include name, description, thumbnailUrl, uploadDate, duration, contentUrl.

**Step 3: Write the JSON-LD**
- Use `@context: "https://schema.org"` in every JSON-LD block.
- Use `@type` to specify the schema type.
- Use `@id` for cross-referencing between schemas on the same page.
- Nest related schemas (e.g., Organization inside Article as publisher).
- Use ISO 8601 format for all dates (e.g., "2025-01-15T09:00:00-05:00").
- Use absolute URLs for all url, image, and logo fields.

**Step 4: Handle Multiple Schemas**
- You can include multiple schemas on one page using a `@graph` array.
- Common pattern: WebSite + Organization on homepage, Article + BreadcrumbList on blog posts.
- Each schema in the graph should have a unique `@id` for reference.

**Step 5: Dynamic Schema Generation**
- For dynamic pages, create a utility function that generates JSON-LD from page data.
- Accept props like title, description, image, date, author and output the complete schema object.
- Use `JSON.stringify()` to safely inject into the script tag (prevents XSS).
- For Next.js, use the metadata API or a Script component with `type="application/ld+json"`.

**Step 6: Validation and Best Practices**
- Validate output against Google's Rich Results Test requirements.
- Ensure required fields are populated for each schema type (Google's docs specify which are mandatory).
- Do not include misleading or inaccurate structured data (violates Google guidelines).
- Keep structured data synchronized with visible page content.
- Suggest testing with Google Rich Results Test and Schema.org validator.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
