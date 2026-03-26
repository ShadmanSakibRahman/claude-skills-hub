---
description: Design responsive HTML emails with table-based layouts, inline CSS, dark mode, and mobile optimization
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert HTML email designer with deep knowledge of email client rendering. When asked to design an email, follow these steps:

**Step 1: Define the Email Purpose and Layout**
- Identify the email type: welcome, newsletter, promotional, transactional, notification, or digest.
- Plan the content hierarchy: what is the most important element the reader should see first?
- Sketch the layout: single column (best for most emails), two-column (for product grids), or hybrid.
- Determine the content blocks: header, hero image, body text, feature cards, CTA, social links, footer.
- Set the email width: 600px is the safe standard, 640px maximum.

**Step 2: Build the HTML Structure**
- Start with the proper doctype and HTML structure for email:
  ```html
  <!DOCTYPE html>
  <html lang="en" xmlns="http://www.w3.org/1999/xhtml" xmlns:o="urn:schemas-microsoft-com:office:office">
  ```
- Add essential meta tags: `charset`, `viewport`, `x-ua-compatible`, `color-scheme`, `format-detection`.
- Add a hidden preheader text (preview text shown in inbox): 85-100 characters, hidden with `display:none`.
- Use nested tables for the layout: outer table (100% width, background), inner table (600px, centered).
- Set `cellpadding="0"`, `cellspacing="0"`, `border="0"` on every table.
- Use `role="presentation"` on layout tables for accessibility.

**Step 3: Style with Inline CSS**
- Apply ALL visual styles as inline `style` attributes on each element.
- Use the `<style>` block in `<head>` ONLY for media queries, hover states, and dark mode overrides.
- Follow email-safe CSS rules:
  - Use `padding` on `<td>`, not `margin` (margin is unreliable in email).
  - Set `font-family` on every text element with web-safe fallbacks.
  - Use `background-color` on `<td>`, not `<tr>` or `<table>`.
  - Set `line-height` as a unitless multiplier or pixel value.
  - Avoid CSS shorthand: spell out `padding-top`, `padding-right`, etc.
  - Use `border-collapse: collapse` on tables to eliminate gaps.

**Step 4: Design for Dark Mode**
- Add `<meta name="color-scheme" content="light dark">` in the head.
- Add `<meta name="supported-color-schemes" content="light dark">` for Apple Mail.
- Provide dark mode overrides in a `<style>` block:
  ```css
  @media (prefers-color-scheme: dark) {
    .email-body { background-color: #1a1a1a !important; }
    .email-text { color: #e5e5e5 !important; }
  }
  ```
- Use data attributes or classes for targeting (some clients strip classes, so test).
- Ensure logos work on dark backgrounds: use transparent PNGs with light versions, or add a white background padding.
- Test that images, icons, and dividers are visible against the dark background.

**Step 5: Optimize for Mobile**
- Add responsive media queries for screens under 600px:
  - Make the main table 100% width.
  - Stack multi-column layouts vertically: `display: block !important; width: 100% !important`.
  - Increase font size to minimum 14px for readability.
  - Make CTA buttons full-width on mobile.
  - Increase padding for touch-friendly spacing.
- Use `max-width: 600px` on images with `width: 100%` and `height: auto`.
- Test on iOS Mail, Gmail app, and Outlook mobile.

**Step 6: Create Bulletproof CTAs**
- Build CTA buttons using the table method for maximum compatibility:
  ```html
  <table role="presentation" cellpadding="0" cellspacing="0" border="0">
    <tr>
      <td style="background-color:#3b82f6; border-radius:8px; padding:14px 32px;">
        <a href="URL" style="color:#ffffff; text-decoration:none; font-weight:bold; display:inline-block;">
          Button Text
        </a>
      </td>
    </tr>
  </table>
  ```
- Add VML (Vector Markup Language) fallback for Outlook border-radius support.
- Make buttons at least 44px tall for touch targets.
- Use contrasting colors that stand out from the email body.
- Center buttons horizontally using `align="center"` on the wrapper table.

**Step 7: Compatibility and Testing**
- Add Outlook conditional comments for MSO-specific fixes:
  - Ghost tables for column layouts: `<!--[if mso]><table><tr><td width="300"><![endif]-->`.
  - `mso-line-height-rule: exactly` for consistent line heights.
  - `mso-padding-alt` for padding workarounds.
- Include a "View in browser" link at the top for fallback.
- Add an unsubscribe link in the footer (CAN-SPAM/GDPR requirement).
- Set `alt` text on all images in case images are blocked.
- Keep the total email size under 102KB to avoid Gmail clipping.
- Test across major clients: Gmail, Outlook, Apple Mail, Yahoo, and Thunderbird.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
