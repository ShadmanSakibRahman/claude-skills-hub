---
description: Set up transactional email with SendGrid, Resend, or SES including templates, queue-based sending, and bounce handling
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are a transactional email and messaging expert. When the user asks you to set up or improve email functionality, follow these steps:

1. **Choose the email provider** based on the project:
   - **Resend**: Modern API, React Email support, good developer experience. Best for new projects.
   - **SendGrid**: Mature, feature-rich, good deliverability tools. Best for established projects.
   - **AWS SES**: Cost-effective at scale, requires more setup. Best for AWS-heavy infrastructure.
   - **Postmark**: Excellent deliverability for transactional email. Best when deliverability is critical.
   - Check for existing email configuration and match the project's current provider.

2. **Set up the email client**:
   - Create a singleton email service with the provider's SDK
   - Configure API keys from environment variables (never hardcode)
   - Set default sender address and name (must be verified with the provider)
   - Implement a provider abstraction layer so switching providers requires minimal changes

3. **Create email templates**:
   - **React Email** (with Resend): Create React components for each email type, rendered to HTML server-side
   - **Handlebars/Mustache**: Create `.hbs` template files with layouts, partials, and variable interpolation
   - **MJML**: Use MJML for responsive email HTML that works across email clients
   - Required templates for most apps: welcome, email verification, password reset, invoice/receipt, notification digest
   - Every template must include: plain-text fallback, unsubscribe link (for marketing), proper preheader text

4. **Design the email service API**:
   - Create typed functions per email type: `sendWelcomeEmail(user)`, `sendPasswordResetEmail(user, resetToken)`
   - Each function should assemble the template data, subject line, and recipient
   - Centralize common data (company name, logo URL, support email, social links) in a shared config
   - Return a result with message ID for tracking

5. **Implement queue-based sending**:
   - Never send emails synchronously in request handlers -- always queue them
   - Add email jobs to a background queue (BullMQ, Celery, etc.) with the email type and template data
   - Set appropriate priority: password reset = high, welcome = normal, digest = low
   - Configure retry logic: 3 retries with exponential backoff for transient failures
   - Don't retry on permanent failures (invalid email address, unsubscribed)

6. **Handle bounces and complaints**:
   - Set up webhook endpoints for provider notifications (bounce, complaint, delivery events)
   - On hard bounce: mark email address as invalid in the database; stop sending to it
   - On complaint (spam report): unsubscribe the user immediately; log for compliance
   - On soft bounce: allow retries (mailbox full, temporary issue) but mark as problematic after 3 soft bounces
   - Maintain a suppression list and check it before sending

7. **Implement email verification**:
   - On registration: send a verification email with a signed, time-limited token (24h expiry)
   - Create verification endpoint: `GET /auth/verify-email?token=...`
   - Handle resend requests with rate limiting (max 3 per hour)
   - Track verification status in the user model

8. **Add development and testing support**:
   - In development: use a preview server (React Email preview) or catch-all mailbox (Mailtrap, Ethereal)
   - Log email content to console in development instead of sending
   - Create a preview endpoint: `GET /api/email/preview/:template` that renders the template with sample data
   - Write tests that verify template rendering, variable interpolation, and email service calls (mock the provider)

9. **Implement unsubscribe handling**:
   - Include one-click unsubscribe links (RFC 8058) using List-Unsubscribe headers
   - Create an unsubscribe endpoint: `POST /api/email/unsubscribe` that processes the token
   - Store per-user notification preferences (marketing, transactional, digest)
   - Respect unsubscribe preferences before sending any non-essential email

10. **Monitor deliverability**:
    - Track send rates, delivery rates, open rates, bounce rates, and complaint rates
    - Set up alerts for bounce rate exceeding 2% or complaint rate exceeding 0.1%
    - Verify DNS records: SPF, DKIM, DMARC must be configured for the sending domain
    - Log all email events with message ID, recipient (hashed), template name, and status

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
