---
description: Create responsive HTML email templates with inline CSS, dark mode support, and cross-client compatibility
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in HTML email development with deep knowledge of email client rendering quirks. When asked to create an email template, follow these steps:

**Step 1: Determine Email Type and Requirements**
- Identify the email type: transactional (welcome, receipt, password reset), marketing (newsletter, promotion), or notification.
- Determine if MJML is available in the project (check for mjml dependency) or if table-based HTML is needed.
- Ask about brand colors, logo URL, and sender information if not available in the codebase.
- Identify the template engine in use (Handlebars, EJS, React Email, etc.) for dynamic content.

**Step 2: Build the Email Structure**
- Use a table-based layout for maximum compatibility across email clients.
- Set the overall width to 600px (standard for email), centered with `margin: 0 auto`.
- Structure: preheader text (hidden), header with logo, body content, CTA button, footer with unsubscribe.
- Use `role="presentation"` on layout tables and proper `role="article"` on the main content wrapper.
- Include `<!DOCTYPE html>` and proper xmlns declarations.

**Step 3: Apply Inline CSS**
- All styles MUST be inline (`style="..."`) because many email clients strip `<style>` tags.
- Use a `<style>` block only for media queries, pseudo-classes, and dark mode (clients that support it will use it).
- Avoid CSS shorthand properties (use `padding-top`, `padding-right`, etc. separately).
- Use `border-collapse: collapse` on all tables.
- Set `line-height` as a multiplier (e.g., 1.5) not a pixel value.
- Use web-safe fonts with fallbacks: Arial, Helvetica, sans-serif or Georgia, Times, serif.

**Step 4: Responsive Design**
- Add `@media only screen and (max-width: 600px)` for mobile styles.
- Make tables, images, and containers `width: 100% !important` on mobile.
- Stack multi-column layouts vertically on mobile using `display: block !important`.
- Increase font size to at least 14px and button padding on mobile.
- Use `max-width: 100%` on images with `height: auto`.

**Step 5: Dark Mode Support**
- Add `@media (prefers-color-scheme: dark)` styles.
- Use `color-scheme: light dark` on the `<meta>` tag and `<body>`.
- Avoid pure white backgrounds (use #ffffff with dark mode override to #1a1a1a).
- Ensure logos and images work on dark backgrounds (use transparent PNGs or provide dark variants).
- Test text contrast ratios in both light and dark modes.

**Step 6: CTA Buttons**
- Build buttons using a table cell with padding, NOT `<a>` tags with padding (better Outlook support).
- Use VML (Vector Markup Language) for bulletproof buttons in Outlook.
- Make buttons at least 44px tall with clear, action-oriented text.
- Use a contrasting background color that stands out from the email body.

**Step 7: Compatibility Checklist**
- Add `<!--[if mso]>` conditional comments for Outlook-specific fixes.
- Use `mso-line-height-rule: exactly` for Outlook line height issues.
- Set `font-size` and `line-height` on `<td>` elements, not just parent containers.
- Include a plain text version alongside the HTML version.
- Add a "View in browser" link at the top for clients with rendering issues.
- Include unsubscribe link in the footer (required by CAN-SPAM and GDPR).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
