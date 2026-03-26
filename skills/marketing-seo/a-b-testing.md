---
description: Set up A/B testing framework with variant rendering, random assignment, statistical significance, and result tracking
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in A/B testing, experimentation, and statistical analysis for web applications. When asked to set up A/B testing, follow these steps:

**Step 1: Choose the Testing Approach**
- Determine if a third-party tool is preferred (LaunchDarkly, Optimizely, GrowthBook, Statsig) or a custom solution.
- For custom solutions, decide between server-side (more reliable, no flicker) and client-side (easier setup) rendering.
- Identify the framework and rendering strategy (SSR, CSR, SSG) to ensure variants render correctly.
- Plan the data storage: cookies, localStorage, or database for assignment persistence.

**Step 2: Build the Assignment System**
- Create a function that deterministically assigns users to variants based on a user ID or session ID.
- Use consistent hashing (e.g., murmurhash on user_id + experiment_name) for stable assignment.
- If no user ID exists, generate a random UUID and persist it in a cookie (lasting 30-90 days).
- Support traffic allocation: e.g., 50/50 split, 90/10 for cautious rollouts, or multi-variant (A/B/C).
- Implement mutual exclusion layers so users are not in conflicting experiments simultaneously.

**Step 3: Create the Variant Rendering System**
- Build a reusable `<ABTest>` component (or equivalent) that accepts experiment name and variant renderers.
- Prevent flickering: determine the variant before the first render (use SSR, cookies, or a loading state).
- Support feature flags alongside A/B tests for gradual rollouts.
- Example API: `<ABTest name="hero-cta" control={<ButtonA />} variant={<ButtonB />} />`.
- For server-side: read the assignment from cookie/session in middleware or getServerSideProps.

**Step 4: Implement Event Tracking**
- Track experiment exposure events: log when a user sees a variant (experiment_name, variant, timestamp).
- Track conversion events tied to experiments: sign_up, purchase, click, etc.
- Integrate with the existing analytics setup (GA4 custom dimensions, Mixpanel, or custom backend).
- Deduplicate exposure events: only track the first exposure per session.
- Include the active experiments and variants as properties on all analytics events.

**Step 5: Statistical Significance Calculation**
- Implement or integrate a significance calculator using the chi-squared test or Z-test for proportions.
- Calculate: conversion rate per variant, relative uplift, p-value, confidence interval.
- Set the significance threshold (typically p < 0.05 or 95% confidence).
- Estimate required sample size before starting: use power analysis (80% power standard).
- Warn against peeking at results too early (define a minimum observation period).

**Step 6: Results Dashboard**
- Create an admin page or API endpoint that shows active experiments and their results.
- Display: variant names, sample sizes, conversion rates, uplift percentage, p-value, and status.
- Visualize results with a simple bar chart or table comparing variants.
- Include a "call experiment" button that locks in the winning variant.
- Archive completed experiments with their results and decision rationale.

**Step 7: Cleanup and Governance**
- After an experiment concludes, remove the losing variant code to reduce tech debt.
- Document experiment results: hypothesis, variants, sample size, outcome, and learnings.
- Set experiment expiration dates to prevent indefinitely running tests.
- Create a naming convention for experiments: `section-element-hypothesis-date` (e.g., `hero-cta-urgency-2025q1`).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
