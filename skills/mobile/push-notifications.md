---
description: Implement push notifications with FCM/APNs including token management, topics, and rich notifications
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in mobile push notification systems. When implementing push notifications, follow these steps:

1. **Determine the platform and framework**: Check `package.json` or `pubspec.yaml`. For React Native use `@react-native-firebase/messaging` or `expo-notifications`. For Flutter use `firebase_messaging` and `flutter_local_notifications`.

2. **Configure Firebase Cloud Messaging (FCM)**:
   - Ensure `google-services.json` (Android) and `GoogleService-Info.plist` (iOS) are in the correct locations.
   - For Android: add the Firebase plugin to `build.gradle` files, declare the messaging service in `AndroidManifest.xml`.
   - For iOS: enable Push Notifications and Background Modes (Remote notifications) capabilities in Xcode. Upload APNs key to Firebase Console.

3. **Implement token management**:
   - Request notification permissions with `requestPermission()` — handle denied/provisional states gracefully.
   - Retrieve the FCM token with `getToken()` and send it to your backend API.
   - Listen for token refresh events (`onTokenRefresh`) and update the backend.
   - Store the token locally to avoid redundant API calls.
   - Handle token invalidation on logout — delete the token server-side and call `deleteToken()`.

4. **Set up topic subscriptions**:
   - Subscribe users to relevant topics (e.g., `news`, `user_<id>`, `promo`).
   - Unsubscribe when preferences change or user logs out.
   - Use topics for broadcast messages, direct tokens for user-specific notifications.

5. **Handle notification states**:
   - **Foreground**: Use `onMessage` listener. Display a local notification or in-app banner since FCM does not auto-display in foreground. Parse the data payload and update UI state if needed.
   - **Background**: Use `setBackgroundMessageHandler` (RN) or `onBackgroundMessage` (Flutter). Keep processing minimal — no UI work. Store data for when the app resumes.
   - **Terminated/Killed**: Check `getInitialNotification()` on app launch to handle the notification that opened the app. Navigate to the appropriate screen.

6. **Implement rich notifications**:
   - Add images using the `image` field in the notification payload. For iOS, implement a Notification Service Extension to download and attach the image.
   - Add action buttons by defining notification categories (iOS) or actions (Android). Handle each action's tap in the message handler.
   - Use Android notification channels for categorization (API 26+). Create channels at startup with appropriate importance levels.

7. **Build the notification payload** (server-side guidance):
   - Use both `notification` (for display) and `data` (for logic) fields.
   - Include a `click_action` or `category` to route taps correctly.
   - Set `priority: "high"` for time-sensitive notifications.
   - Include `badge` count for iOS.

8. **Test thoroughly**:
   - Test on real devices — simulators have limited notification support.
   - Test all three states: foreground, background, and terminated.
   - Test with the app force-killed by the user.
   - Verify deep link navigation from notification taps.
   - Use Firebase Console or `fcm-cli` for quick test sends.

Handle all error cases: permission denied, network failures during token registration, and malformed payloads.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
