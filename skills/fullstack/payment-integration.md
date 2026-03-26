---
description: Integrate Stripe payments with checkout, subscriptions, webhooks, customer portal, and tax calculation
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in payment integration, specifically with Stripe. When asked to integrate payments, follow these steps:

**Step 1: Initial Setup**
- Install the Stripe SDK: `stripe` (server-side) and `@stripe/stripe-js` + `@stripe/react-stripe-js` (client-side).
- Configure environment variables: `STRIPE_SECRET_KEY`, `STRIPE_PUBLISHABLE_KEY`, `STRIPE_WEBHOOK_SECRET`.
- Use test mode keys during development (keys starting with `sk_test_` and `pk_test_`).
- Create a Stripe client instance in a shared module (e.g., `lib/stripe.ts`).
- Set the API version explicitly for stability.

**Step 2: Products and Prices**
- Create products and prices either via the Stripe Dashboard or programmatically.
- For programmatic setup: create a seed script that syncs products/prices to Stripe.
- Store Stripe product/price IDs in environment variables or a config file.
- Support multiple pricing models: one-time, recurring (monthly/yearly), metered, tiered.
- Create a pricing page that displays plans fetched from Stripe or hardcoded with Stripe price IDs.

**Step 3: Checkout Sessions**
- Create an API endpoint (e.g., `POST /api/checkout`) that creates a Stripe Checkout Session.
- Configure the session: line_items, mode (payment/subscription), success_url, cancel_url.
- Pass the customer email or Stripe customer ID if the user is logged in.
- Enable automatic tax calculation if needed (`automatic_tax: { enabled: true }`).
- Allow promotion codes if applicable (`allow_promotion_codes: true`).
- Redirect the user to `session.url` on the client side.

**Step 4: Webhook Handling**
- Create a webhook endpoint (e.g., `POST /api/webhooks/stripe`).
- Verify the webhook signature using `stripe.webhooks.constructEvent()` with the raw body.
- Handle critical events:
  - `checkout.session.completed`: Fulfill the order, grant access, update user subscription status.
  - `invoice.payment_succeeded`: Record successful payment, extend subscription.
  - `invoice.payment_failed`: Notify user, update subscription status to past_due.
  - `customer.subscription.updated`: Sync plan changes to the database.
  - `customer.subscription.deleted`: Revoke access, update status to canceled.
- Implement idempotency: check if the event has already been processed before taking action.
- Return 200 quickly; process heavy logic asynchronously if needed.

**Step 5: Subscription Management**
- Create or retrieve Stripe customers when users sign up (store `stripe_customer_id` in the user table).
- Implement plan upgrade/downgrade: use `stripe.subscriptions.update()` with proration.
- Handle cancellation: cancel at period end (`cancel_at_period_end: true`) to allow access until expiry.
- Implement reactivation for canceled-but-not-expired subscriptions.
- Show current plan, next billing date, and payment method in the user's account settings.

**Step 6: Customer Portal**
- Create a Customer Portal session for self-service billing management.
- Configure the portal in Stripe Dashboard: allow plan changes, cancellation, payment method updates.
- Create an API endpoint that generates a portal session URL and redirects the user.
- This handles most billing management without custom UI.

**Step 7: Error Handling and Production Checklist**
- Handle Stripe errors gracefully: card declined, expired, insufficient funds.
- Display user-friendly error messages (never expose raw Stripe errors).
- Implement retry logic for transient failures with exponential backoff.
- Set up Stripe webhook event logging for debugging.
- Before going live: switch to live keys, test the full purchase flow, verify webhook endpoint is reachable, and enable fraud prevention (Radar).
- Document the payment flow, webhook events handled, and how to test with Stripe CLI.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
