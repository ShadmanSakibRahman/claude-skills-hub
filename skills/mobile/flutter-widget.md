---
description: Create Flutter widgets with state management, Material 3 theming, responsive layouts, and platform-adaptive design
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert Flutter developer. When creating or modifying Flutter widgets, follow these steps precisely:

1. **Analyze the request**: Determine whether the widget should be Stateless or Stateful. Prefer StatelessWidget when using external state management (Riverpod/BLoC). Only use StatefulWidget for ephemeral UI state (animations, form focus, scroll position).

2. **Choose state management**:
   - **Riverpod**: Use `ConsumerWidget` / `ConsumerStatefulWidget`. Define providers in a separate `providers/` file. Use `ref.watch()` for reactive UI, `ref.read()` for one-off actions.
   - **BLoC**: Create `Bloc`/`Cubit` classes with well-defined events and states. Use `BlocBuilder`, `BlocListener`, or `BlocConsumer` in the widget tree.
   - **Provider**: Use `ChangeNotifierProvider` and `Consumer` or `context.watch()`.
   - Match whatever the existing project uses.

3. **Apply Material 3 theming**:
   - Use `Theme.of(context).colorScheme` for colors — never hardcode color values.
   - Use `Theme.of(context).textTheme` for typography (displayLarge, bodyMedium, etc.).
   - Define custom component themes in the app's `ThemeData` rather than inline overrides.
   - Support both light and dark themes via `ColorScheme.fromSeed()`.

4. **Build responsive layouts**:
   - Use `MediaQuery.of(context).size` and `LayoutBuilder` for responsive sizing.
   - Implement breakpoints: compact (<600dp), medium (600-840dp), expanded (>840dp).
   - Use `Flexible`, `Expanded`, and `FractionallySizedBox` instead of fixed sizes.
   - Use `OrientationBuilder` when layout changes between portrait and landscape.

5. **Platform-adaptive design**:
   - Use `Platform.isIOS` / `Platform.isAndroid` for platform-specific behavior.
   - Consider `CupertinoPageRoute` on iOS vs `MaterialPageRoute` on Android.
   - Use adaptive constructors (e.g., `Switch.adaptive`, `AlertDialog.adaptive`) when available.

6. **Structure the widget**:
   - Keep `build()` methods short — extract sub-widgets as private methods or separate widget classes.
   - Use `const` constructors wherever possible for performance.
   - Add `Key` parameter to constructors when widgets appear in lists.
   - Document public APIs with `///` doc comments.

7. **Handle edge cases**:
   - Show loading states with `CircularProgressIndicator` or shimmer placeholders.
   - Handle empty states with informative messages and CTAs.
   - Display errors gracefully with retry options.
   - Use `SafeArea` to avoid system UI overlap.

8. **Write tests**: Create widget tests in `test/` using `testWidgets()`, `pumpWidget()`, and `find.*` matchers. Mock state management dependencies.

Follow the project's existing directory structure, naming conventions, and lint rules (`analysis_options.yaml`).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
