---
description: Generate optimized app store listings for iOS App Store and Google Play with descriptions, keywords, and metadata
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in App Store Optimization (ASO). When generating app store listings, follow these steps:

1. **Gather context**: Read the project's README, about page, marketing materials, and existing app store listing (if any). Understand the app's core value proposition, target audience, and competitive differentiators.

2. **Craft the app title** (max 30 characters):
   - Lead with the brand name.
   - Append a short descriptor with a high-value keyword (e.g., "Acme - Task Manager").
   - Avoid keyword stuffing — keep it readable and brandable.
   - Ensure it is distinct from competitor names to avoid rejection.

3. **Write the subtitle** (iOS, max 30 characters):
   - Highlight the primary benefit or use case, not a feature.
   - Include a secondary keyword not used in the title.
   - Example: "Plan, Track & Collaborate" rather than "Project Management App".

4. **Write the short description** (Google Play, max 80 characters):
   - One compelling sentence summarizing the app's value.
   - Include a call-to-action or key benefit.

5. **Write the full description**:
   - **iOS** (max 4000 chars): Focus on benefits over features. Use short paragraphs. No keyword stuffing — Apple's algorithm uses the keyword field, not the description.
   - **Google Play** (max 4000 chars): Front-load keywords naturally. Use bullet points for features. Include keywords in the first 2-3 lines (visible before "Read more"). Structure: hook paragraph, feature list, social proof, CTA.
   - Format with line breaks and Unicode symbols (bullet points, checkmarks) for readability.

6. **Select keywords** (iOS keyword field, max 100 characters):
   - Research competitors' keywords and relevant search terms.
   - Separate with commas, no spaces. Do not repeat words already in the title/subtitle.
   - Prioritize: high relevance + moderate competition keywords.
   - Include common misspellings and synonyms.

7. **Describe screenshots** (provide descriptions/captions for 6-10 screenshots):
   - First two screenshots are most critical — they appear in search results.
   - Each screenshot: a headline (benefit-focused), a brief caption, and what to show visually.
   - Cover the core user journey: onboarding, main feature, secondary features, results/output.
   - Include device frames and consistent branding.

8. **Select categories**:
   - Choose a primary and secondary category on both stores.
   - Primary category should match user intent — where they would search.
   - Secondary category expands discovery.

9. **Outline privacy policy requirements**:
   - List all data types collected (name, email, location, usage analytics, etc.).
   - Specify purpose for each data type (app functionality, analytics, advertising).
   - Note third-party SDKs that collect data (Firebase, analytics, ad networks).
   - Cover data retention, deletion rights, and contact information.
   - Flag requirements for Apple's App Privacy nutrition labels and Google's Data Safety section.

10. **Output the listing** in a structured document with clearly labeled sections for each store, ready to copy-paste into App Store Connect and Google Play Console.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
