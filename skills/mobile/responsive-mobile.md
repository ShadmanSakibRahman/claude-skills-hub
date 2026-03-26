---
description: Create responsive mobile layouts for different screen sizes, orientations, notches, tablets, and split-screen
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in responsive mobile UI design. When creating or modifying layouts for multiple screen sizes, follow these steps:

1. **Audit the target devices**: Identify the range of devices to support — small phones (iPhone SE / 320pt), standard phones (375-414pt), large phones (428pt+), tablets (768pt+), and foldables. Determine if the app must support both orientations.

2. **Use SafeAreaView correctly**:
   - **React Native**: Wrap screens with `SafeAreaView` from `react-native-safe-area-context` (not the one from `react-native`). Use `useSafeAreaInsets()` hook for granular control over individual edges.
   - **Flutter**: Use `SafeArea` widget or `MediaQuery.of(context).padding` for precise inset values.
   - Apply safe area padding to the outermost container — do not nest multiple SafeAreaViews.
   - Account for bottom insets on phones with home indicator bars.

3. **Handle notches and display cutouts**:
   - Avoid placing interactive elements or critical content in the notch/cutout area.
   - On Android: set `android:windowLayoutInDisplayCutoutMode="shortEdges"` in the theme for edge-to-edge content.
   - Test with different notch configurations using device simulators/emulators.

4. **Implement responsive sizing**:
   - **React Native**: Use `useWindowDimensions()` for reactive width/height. Create a `scale()` utility: `const scale = (size: number) => (width / 375) * size` for proportional sizing based on a 375pt design.
   - **Flutter**: Use `MediaQuery.sizeOf(context)` and `LayoutBuilder` for responsive sizing. Consider the `flutter_screenutil` package for design-pixel-to-device-pixel conversion.
   - Define breakpoints: phone portrait, phone landscape, tablet portrait, tablet landscape.
   - Use percentage-based widths for containers, not fixed pixel values.

5. **Build adaptive layouts**:
   - At phone breakpoint: single column, full-width cards, bottom navigation.
   - At tablet breakpoint: multi-column layouts, side navigation, master-detail views.
   - Use `useWindowDimensions()` (RN) or `LayoutBuilder` (Flutter) to switch layouts.
   - Implement a `ResponsiveBuilder` widget/component that renders different layouts based on breakpoints.

6. **Handle orientation changes**:
   - Listen for orientation changes and rebuild layouts accordingly.
   - In landscape: consider side-by-side layouts, hiding non-essential UI, or adjusting column counts.
   - Lock orientation only when absolutely necessary (e.g., video playback) — otherwise support both.
   - Preserve scroll position and form state across orientation changes.

7. **Support split-screen and multi-window mode**:
   - On Android: the app window can be resized at any time. Do not assume full-screen dimensions.
   - Avoid `Dimensions.get('screen')` — always use `useWindowDimensions()` which reflects the actual window size.
   - Test with Android's split-screen and freeform window modes.
   - On iPadOS: support Slide Over and Split View. Test at 1/3, 1/2, and 2/3 width.

8. **Typography and touch targets**:
   - Scale font sizes responsively but set minimum and maximum bounds for readability.
   - Ensure touch targets are at least 44x44pt (iOS) or 48x48dp (Android) regardless of screen size.
   - Increase spacing and padding proportionally on larger screens.
   - Use `maxWidth` constraints on content containers to prevent overly wide text on tablets.

9. **Test across sizes**:
   - Test on the smallest and largest supported devices.
   - Test in both orientations on phones and tablets.
   - Test with accessibility font sizes (Dynamic Type on iOS, font scale on Android).
   - Test with split-screen on iPad and Android tablets.

Create a shared responsive utilities module that the entire app can use for consistent sizing.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
