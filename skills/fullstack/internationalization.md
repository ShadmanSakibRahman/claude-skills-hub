---
description: Set up internationalization with locale detection, translation files, RTL support, and formatting
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in web application internationalization (i18n) and localization. When asked to set up i18n, follow these steps:

**Step 1: Choose the i18n Library**
- Identify the framework and select the appropriate library:
  - **Next.js**: `next-intl` (App Router recommended), `next-i18next` (Pages Router), or built-in i18n routing.
  - **React**: `react-i18next` with `i18next` core.
  - **Vue/Nuxt**: `vue-i18n` or `@nuxtjs/i18n`.
  - **Svelte/SvelteKit**: `svelte-i18n` or `paraglide-js`.
- Install the library and its dependencies.
- Determine the supported locales (e.g., en, es, fr, de, ja, ar) and the default locale.

**Step 2: Configure Locale Detection**
- Set up automatic locale detection in this priority order:
  1. URL path prefix (e.g., `/en/about`, `/fr/about`) - recommended for SEO.
  2. Cookie preference (for returning users).
  3. `Accept-Language` header from the browser.
  4. Default locale fallback.
- Configure middleware to detect and redirect to the appropriate locale.
- For Next.js App Router: set up the `[locale]` dynamic segment in the app directory.
- Store the user's locale preference in a cookie when they manually switch languages.

**Step 3: Set Up Translation Files**
- Create a structured directory for translations:
  ```
  messages/
    en/
      common.json    # Shared strings (nav, footer, buttons)
      auth.json      # Auth-related strings
      dashboard.json # Dashboard-specific strings
    es/
      common.json
      auth.json
      dashboard.json
  ```
- Use nested keys for organization: `{ "auth": { "login": { "title": "Sign In", "submit": "Log In" } } }`.
- Use ICU message format for complex messages with variables, plurals, and gender.
- Add translator comments for context where the meaning might be ambiguous.

**Step 4: Implement Translation in Components**
- Use the translation hook/function in every component with user-facing text.
- Replace all hardcoded strings with translation keys: `t('auth.login.title')`.
- Handle interpolation: `t('greeting', { name: user.name })` renders "Hello, {name}!".
- Support HTML in translations safely (use rich text components, not `dangerouslySetInnerHTML`).
- Create a language switcher component that lists available locales with native language names.

**Step 5: Date, Number, and Currency Formatting**
- Use the `Intl` API or library formatters for locale-aware formatting:
  - Dates: `Intl.DateTimeFormat` or `formatDate()` from the i18n library.
  - Numbers: `Intl.NumberFormat` for decimal separators and grouping.
  - Currency: `Intl.NumberFormat` with `style: 'currency'` and the appropriate currency code.
  - Relative time: `Intl.RelativeTimeFormat` for "2 hours ago", "in 3 days".
- Create shared formatting utilities that accept a locale parameter.
- Handle timezone display using `Intl.DateTimeFormat` with `timeZone` option.

**Step 6: Pluralization and Complex Messages**
- Use ICU message syntax for plurals: `{count, plural, one {# item} other {# items}}`.
- Handle gender: `{gender, select, male {He} female {She} other {They}} liked your post`.
- Handle ordinals: `{position, selectordinal, one {#st} two {#nd} few {#rd} other {#th}}`.
- Test pluralization rules for each supported locale (Arabic has 6 plural forms, for example).

**Step 7: RTL Support and Accessibility**
- Set the `dir` attribute on `<html>` dynamically based on the locale (RTL for Arabic, Hebrew, Persian, Urdu).
- Use CSS logical properties: `margin-inline-start` instead of `margin-left`, `padding-inline-end` instead of `padding-right`.
- Mirror layouts for RTL: flip icons with directional meaning, adjust text alignment.
- Set the `lang` attribute on `<html>` to the current locale for screen readers.
- Add `hreflang` link tags for all locale variants for SEO.
- Test the UI thoroughly in at least one RTL locale.

**Step 8: Translation Workflow**
- Create a script to extract translation keys from source code.
- Set up a process for sending translations to translators (export JSON, or integrate with Crowdin/Lokalise/Phrase).
- Implement fallback chains: missing translation falls back to default locale.
- Add CI checks for missing translation keys across locales.
- Log missing translations in development to catch untranslated strings early.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
