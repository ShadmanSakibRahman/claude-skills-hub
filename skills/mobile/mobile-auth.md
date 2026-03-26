---
description: Implement mobile authentication with biometrics, secure token storage, social login, and session management
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in mobile authentication and security. When implementing auth, follow these steps:

1. **Assess requirements**: Determine which auth methods are needed (email/password, social login, biometrics, MFA). Check existing backend auth system (JWT, OAuth2, session-based).

2. **Implement secure token storage**:
   - **iOS**: Use Keychain Services via `react-native-keychain` (RN) or `flutter_secure_storage` (Flutter). Set accessibility level to `kSecAttrAccessibleWhenUnlockedThisDeviceOnly` for sensitive tokens.
   - **Android**: Use Android Keystore system. The `flutter_secure_storage` and `react-native-keychain` packages wrap this automatically. Ensure `encryptedSharedPreferences` is used on API 23+.
   - Never store tokens in AsyncStorage, SharedPreferences, UserDefaults, or plain files.
   - Store: access token, refresh token, and token expiry timestamp.

3. **Implement biometric authentication**:
   - Check biometric availability: `react-native-biometrics` (RN) or `local_auth` (Flutter).
   - Determine supported types: Face ID, Touch ID, fingerprint, or iris.
   - Prompt with a clear reason string: "Authenticate to access your account".
   - Handle fallback to device passcode/PIN if biometrics fail.
   - Store a biometric-protected key in Keychain/Keystore that unlocks the stored credentials.
   - Allow users to opt in/out of biometric login in settings.
   - On iOS: add `NSFaceIDUsageDescription` to `Info.plist`.

4. **Set up social login** (Google, Apple, Facebook):
   - **Sign in with Apple**: Required if you offer any social login on iOS. Use `@invertase/react-native-apple-authentication` (RN) or `sign_in_with_apple` (Flutter). Provide name and email on first sign-in.
   - **Google Sign-In**: Use `@react-native-google-signin/google-signin` (RN) or `google_sign_in` (Flutter). Configure OAuth client IDs for iOS and Android separately.
   - **Facebook Login**: Use the Facebook SDK. Request minimal permissions (`email`, `public_profile`).
   - Exchange the social provider token for your backend's auth token. Create or link user accounts server-side.

5. **Handle the auth flow**:
   - On app launch: check for stored tokens. If access token is valid, proceed. If expired, attempt silent refresh with the refresh token. If refresh fails, redirect to login.
   - After login: store tokens securely, update auth state, and navigate to the main app.
   - On logout: delete all stored tokens, clear sensitive in-memory data, reset navigation to login screen, and optionally revoke the refresh token server-side.

6. **Implement session management**:
   - Attach the access token to all API requests via an HTTP interceptor/middleware.
   - Handle 401 responses: attempt token refresh once, then force logout if refresh fails.
   - Implement token refresh with a request queue — block concurrent requests during refresh, then retry all queued requests with the new token.
   - Set a reasonable session timeout and warn users before expiry.

7. **Add multi-factor authentication (MFA)** if required:
   - Support TOTP (Google Authenticator, Authy) with QR code scanning.
   - Support SMS/email OTP as a fallback.
   - Store MFA enrollment status and handle the verification step in the login flow.

8. **Security best practices**:
   - Use certificate pinning for auth endpoints (`react-native-ssl-pinning` or Dio's certificate pinning).
   - Implement jailbreak/root detection and warn users or restrict functionality.
   - Clear clipboard after pasting passwords or OTPs.
   - Disable screenshots on sensitive screens (Android `FLAG_SECURE`).
   - Log auth events for audit trail (login, logout, failed attempts, biometric fallback).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
