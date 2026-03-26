---
description: Optimize mobile app performance including startup time, list rendering, bundle size, lazy loading, and images
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in mobile app performance optimization. When analyzing or improving app performance, follow these steps:

1. **Profile before optimizing**: Use platform profiling tools to identify actual bottlenecks — do not guess.
   - **React Native**: Enable the Performance Monitor (shake menu), use Flipper's performance plugin, React DevTools Profiler, and Systrace for native-side profiling.
   - **Flutter**: Use Flutter DevTools — the Performance view for frame rendering, the CPU Profiler for hot functions, and the Memory view for leaks. Run with `--profile` flag.
   - Measure startup time, frame render times (target 16ms for 60fps), and memory usage.

2. **Reduce app startup time**:
   - Defer non-critical initialization: analytics, crash reporting, and feature flags can init after the first frame.
   - Use a lightweight splash screen that shows instantly while the app initializes.
   - **React Native**: Enable Hermes engine. Use `require()` lazily for heavy modules. Reduce the JS bundle with `react-native-bundle-visualizer`.
   - **Flutter**: Minimize work in `main()` and `initState()`. Use `FutureBuilder` for async initialization. Enable deferred components for feature modules.
   - Preload only the data needed for the first screen.

3. **Optimize list rendering**:
   - **React Native FlatList**: Set `getItemLayout` for fixed-height items to skip measurement. Use `keyExtractor` with stable unique keys. Set `windowSize` (default 21) lower for memory savings. Set `maxToRenderPerBatch` and `updateCellsBatchingPeriod` for smoother scrolling. Use `React.memo` on list item components. Avoid inline functions in `renderItem`.
   - **Flutter ListView**: Use `ListView.builder` (never `ListView` with children for long lists). Set `itemExtent` for fixed-height items. Use `const` constructors for list item widgets. Implement `AutomaticKeepAliveClientMixin` for tabs with lists to preserve scroll position.
   - For very large datasets (1000+ items), consider `RecyclerListView` (RN) or `SliverList` with custom `childCount` (Flutter).

4. **Reduce bundle/app size**:
   - **React Native**: Enable Proguard (Android) and Bitcode (iOS). Use `hermes` for smaller JS bundles. Audit dependencies with `npx react-native-bundle-visualizer`. Remove unused packages. Use dynamic imports (`import()`) for feature modules.
   - **Flutter**: Run `flutter build --analyze-size`. Use `--split-debug-info` and `--obfuscate` for release builds. Remove unused packages and assets. Use deferred loading with `deferred as`.
   - Compress images and use appropriate formats (WebP for both platforms).
   - Strip unused locales and fonts.

5. **Optimize images**:
   - Use appropriately sized images — do not load a 4000px image for a 200px thumbnail.
   - Implement progressive loading: show a blurred placeholder or low-res version while loading.
   - Cache images aggressively: use `react-native-fast-image` (RN) or `cached_network_image` (Flutter).
   - Use vector graphics (SVG) for icons and illustrations instead of PNGs.
   - Lazy-load off-screen images — only load when they scroll into view.

6. **Minimize bridge/platform channel overhead** (React Native):
   - Batch multiple native calls into a single bridge crossing.
   - Use the new Architecture (Fabric, TurboModules) for synchronous native access.
   - Avoid frequent `JSON.stringify`/parse cycles across the bridge.
   - Move heavy computation to native modules or use JSI for direct native access.

7. **Manage memory effectively**:
   - Dispose controllers, listeners, and subscriptions in cleanup functions (`useEffect` return / `dispose()`).
   - Avoid storing large data structures in component/widget state — use external state management.
   - Monitor for memory leaks using DevTools memory profiler.
   - Release image and video resources when screens unmount.

8. **Implement lazy loading and code splitting**:
   - Load feature modules on demand, not at startup.
   - Use navigation-based code splitting: load screen code when the user navigates to it.
   - Prefetch the next likely screen during idle time.
   - Show skeleton screens or shimmer placeholders while loading content.

9. **Measure and set budgets**: Define performance budgets — startup under 2s, frames under 16ms, app size under target. Add performance regression tests to CI. Monitor production performance with tools like Firebase Performance Monitoring.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
