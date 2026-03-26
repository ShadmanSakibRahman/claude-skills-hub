---
description: Set up deep linking and universal links with iOS Associated Domains, Android App Links, and deferred deep links
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in mobile deep linking. When setting up deep links and universal links, follow these steps:

1. **Plan the URL scheme**:
   - Define a custom URL scheme for development/testing (e.g., `myapp://`).
   - Define universal/app links using your domain (e.g., `https://example.com/app/...`).
   - Map URL paths to screens: document each path pattern, its parameters, and the target screen.
   - Example mapping: `https://example.com/product/:id` -> ProductDetailScreen with `id` param.

2. **Configure iOS Universal Links**:
   - Create the `apple-app-site-association` (AASA) file. Host it at `https://yourdomain.com/.well-known/apple-app-site-association` (no file extension, `Content-Type: application/json`).
   - AASA content: specify `applinks.details` with your team ID and bundle ID, and the URL patterns (`paths` or `components`).
   - In Xcode: add the Associated Domains capability with `applinks:yourdomain.com`.
   - Ensure the AASA file is served over HTTPS with a valid certificate — no redirects allowed.

3. **Configure Android App Links**:
   - Create a Digital Asset Links file at `https://yourdomain.com/.well-known/assetlinks.json`.
   - Include your app's package name and SHA-256 certificate fingerprint.
   - In `AndroidManifest.xml`: add `<intent-filter>` with `android:autoVerify="true"`, `ACTION_VIEW`, `CATEGORY_DEFAULT`, `CATEGORY_BROWSABLE`, and `<data>` elements matching your URL patterns.
   - For multiple URL patterns, add multiple `<data>` elements within the same intent filter.

4. **Handle incoming links in the app**:
   - **React Native**: Use `Linking.getInitialURL()` for cold starts and `Linking.addEventListener('url', handler)` for warm starts. Alternatively, configure React Navigation's `linking` prop with a prefix and screen mapping.
   - **Flutter**: Use `go_router`'s built-in deep link handling or `uni_links` / `app_links` package. Handle `getInitialLink()` and `linkStream` for the two launch scenarios.
   - Parse the URL to extract path segments and query parameters. Validate parameters before navigating.

5. **Implement deferred deep links**:
   - For users who don't have the app installed: redirect to the app store, then open the intended content after install.
   - Use a service like Firebase Dynamic Links (deprecated — migrate to custom solution), Branch.io, or AppsFlyer OneLink.
   - Alternatively, build a custom solution: store the deep link payload server-side keyed by device fingerprint or clipboard token, retrieve it on first app launch.
   - Pass the deferred link context through the install flow to the first screen.

6. **Parse and validate links**:
   - Create a centralized `DeepLinkHandler` or `LinkParser` class.
   - Parse the URL into a structured route object with typed parameters.
   - Validate that required parameters exist and are in the expected format.
   - Handle unknown routes gracefully — navigate to home or show a "not found" screen.
   - Log deep link events for analytics (source, campaign, path).

7. **Test deep links**:
   - iOS Simulator: `xcrun simctl openurl booted "https://example.com/product/123"`.
   - Android Emulator: `adb shell am start -a android.intent.action.VIEW -d "https://example.com/product/123"`.
   - Verify AASA: `curl -v https://yourdomain.com/.well-known/apple-app-site-association`.
   - Verify Asset Links: use Google's Digital Asset Links API tool.
   - Test both cold start (app killed) and warm start (app in background) scenarios.

8. **Handle edge cases**:
   - User not authenticated: save the deep link destination, redirect to login, then navigate after auth.
   - Invalid or expired content: show an appropriate error rather than crashing.
   - Multiple link handlers: ensure only one handler processes each link to avoid duplicate navigation.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
