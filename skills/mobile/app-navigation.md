---
description: Set up mobile app navigation with React Navigation or Go Router including deep linking and auth guards
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in mobile app navigation architecture. When setting up or modifying navigation, follow these steps:

1. **Detect the framework** by scanning the project for `package.json` (React Native) or `pubspec.yaml` (Flutter). Check for existing navigation libraries already installed.

2. **React Navigation (React Native)**:
   - Install required packages: `@react-navigation/native`, `@react-navigation/stack` or `@react-navigation/native-stack`, and any tab/drawer navigators needed.
   - Create a `navigation/` directory with separate files for each navigator.
   - Define a `RootStackParamList` type mapping route names to their params for full type safety.
   - Use `useNavigation<StackNavigationProp<RootStackParamList>>()` in components.
   - Configure `NavigationContainer` with a `linking` config for deep link support.

3. **Go Router (Flutter)**:
   - Define routes in a `router.dart` file using `GoRouter` with `GoRoute` entries.
   - Use path parameters (`:id`) and query parameters for data passing.
   - Create route constants or an enum to avoid magic strings.
   - Use `context.go()` for declarative navigation, `context.push()` for imperative.
   - Configure `redirect` callback for auth guards.

4. **Set up deep linking**:
   - Define a URL scheme (e.g., `myapp://`) and universal links domain.
   - Map URL patterns to specific screens with parameter extraction.
   - Handle the initial link that launched the app and links received while running.
   - Test with `adb shell am start -a android.intent.action.VIEW -d "myapp://path"` (Android) and `xcrun simctl openurl booted "myapp://path"` (iOS).

5. **Implement authentication guards**:
   - Create an auth state listener that controls navigation flow.
   - Define separate navigator trees for authenticated and unauthenticated states.
   - Redirect to login screen when auth token is missing or expired.
   - Preserve the intended destination for post-login redirect.
   - Handle token refresh transparently without disrupting navigation.

6. **Configure nested navigation**:
   - Use tab navigators with independent stack navigators per tab.
   - Maintain scroll position and state when switching tabs.
   - Handle "reset to top" on tab re-press.
   - Support modal presentation that overlays the tab bar.

7. **Add transitions and animations**:
   - Use platform-appropriate default transitions (slide from right on iOS, fade on Android).
   - Configure custom transitions for modals (slide from bottom) and special flows.
   - Ensure gesture-based back navigation works on iOS (swipe from edge).

8. **Type-safe route parameters**:
   - Define parameter types for every route — never pass untyped objects.
   - Validate required parameters at navigation time.
   - Provide sensible defaults for optional parameters.

Always register all routes in a central configuration and keep navigation logic separate from UI components.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
