---
description: Set up Google Analytics 4, event tracking, conversion goals, UTM handling, and privacy-compliant analytics
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in web analytics implementation and privacy-compliant tracking. When asked to set up analytics, follow these steps:

**Step 1: Determine Analytics Requirements**
- Identify the analytics platform: Google Analytics 4 (GA4), Plausible, Fathom, Mixpanel, or PostHog.
- Check for existing analytics code in the project (search for gtag, analytics, tracking scripts).
- Determine the framework to choose the right integration method.
- Ask for the GA4 Measurement ID (G-XXXXXXXXXX) or suggest using an environment variable.

**Step 2: Install the Base Tracking Script**
- For GA4: Add the gtag.js snippet to the document head or use a package like `@next/third-parties`.
- Load the script asynchronously to avoid blocking page render.
- Store the measurement ID in an environment variable (e.g., `NEXT_PUBLIC_GA_ID`).
- For SPAs: ensure page view tracking works with client-side navigation (listen to route changes).
- Initialize with sensible defaults: `send_page_view: true`, anonymize IP where required.

**Step 3: Implement Event Tracking**
- Set up a centralized analytics utility module (e.g., `lib/analytics.ts`) with typed helper functions.
- Track key events: page_view, sign_up, login, purchase, add_to_cart, form_submit, button_click.
- Use consistent naming conventions: snake_case for event names, descriptive parameter names.
- Include relevant parameters with each event (e.g., button_click: { button_id, page, section }).
- Create a `trackEvent(name, params)` wrapper function for clean, reusable tracking calls.

**Step 4: Custom Dimensions and Conversions**
- Define custom dimensions for user properties: user_type, subscription_plan, account_age.
- Set up conversion events for key business goals: purchase, sign_up, contact_form_submit.
- Configure enhanced ecommerce tracking if applicable (view_item, add_to_cart, begin_checkout, purchase).
- Track custom metrics like engagement_time, scroll_depth, and video_watch_percentage.

**Step 5: UTM Parameter Handling**
- Parse UTM parameters from the URL on page load (utm_source, utm_medium, utm_campaign, utm_term, utm_content).
- Store UTM parameters in sessionStorage or cookies for attribution across the session.
- Pass UTM data as event parameters on conversion events for campaign attribution.
- Clean URLs by removing UTM parameters from the browser address bar after capture (optional, using replaceState).

**Step 6: Consent Management**
- Implement a cookie consent banner that complies with GDPR, CCPA, and ePrivacy.
- Default to denied consent mode: `gtag('consent', 'default', { analytics_storage: 'denied' })`.
- Update consent on user acceptance: `gtag('consent', 'update', { analytics_storage: 'granted' })`.
- Queue events before consent is granted and replay them after.
- Provide opt-out mechanism and respect Do Not Track headers.
- Store consent preferences in a cookie with appropriate expiration (e.g., 365 days).

**Step 7: Testing and Debugging**
- Enable GA4 DebugView during development by setting `debug_mode: true`.
- Use the browser extension "Google Analytics Debugger" for real-time event inspection.
- Verify events appear correctly in the GA4 Realtime report.
- Ensure no PII (emails, names, phone numbers) is sent in any event parameters.
- Add analytics to the development environment with a separate measurement ID.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
