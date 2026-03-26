---
description: Generate changelog from git history by parsing conventional commits, grouping by version, and formatting as Keep a Changelog
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in generating changelogs from Git history. When creating or updating a changelog, follow these steps:

1. **Analyze the git history**:
   - List all tags: `git tag --sort=-version:refname` to understand versioning.
   - Get commits since the last tag: `git log $(git describe --tags --abbrev=0)..HEAD --oneline`.
   - For a full changelog: iterate through tag pairs to get commits for each version.
   - Check if commits follow conventional commit format: `git log --oneline -20` to inspect.

2. **Parse conventional commits**:
   - Extract the type, optional scope, and description from each commit: `type(scope): description`.
   - Handle non-conventional commits by categorizing based on keywords in the message:
     - Contains "fix", "bug", "patch", "resolve" -> Bug Fixes.
     - Contains "add", "new", "feature", "implement" -> Added.
     - Contains "remove", "delete", "drop" -> Removed.
     - Contains "update", "change", "modify", "improve" -> Changed.
     - Contains "deprecate" -> Deprecated.
     - All others -> Changed (default category).
   - Extract issue/PR references: `#123`, `GH-456`, `JIRA-789`.
   - Detect breaking changes: `BREAKING CHANGE:` in footer or `!` after type.

3. **Group changes by category** (Keep a Changelog format):
   - **Added**: New features (`feat` commits).
   - **Changed**: Changes to existing functionality (`refactor`, `perf`, enhancements).
   - **Deprecated**: Features that will be removed in future versions.
   - **Removed**: Features that have been removed.
   - **Fixed**: Bug fixes (`fix` commits).
   - **Security**: Vulnerability fixes.
   - Omit empty categories.

4. **Format each entry**:
   - Write in past tense, user-facing language: "Added dark mode support" not "feat: dark mode".
   - Include the scope as context if helpful: "Added dark mode support to settings page".
   - Link to PRs/issues: "Fixed login timeout on slow connections ([#234](https://github.com/org/repo/pull/234))".
   - Group related commits into a single entry when they address the same feature/fix.
   - Remove purely internal changes (CI, tests, dependency bumps) from user-facing changelogs — or put them in an "Internal" section.

5. **Structure the changelog file**:
   ```
   # Changelog

   All notable changes to this project will be documented in this file.

   The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
   and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

   ## [Unreleased]

   ## [1.2.0] - 2025-03-15

   ### Added
   - ...

   ### Fixed
   - ...

   ## [1.1.0] - 2025-02-01
   ...

   [Unreleased]: https://github.com/org/repo/compare/v1.2.0...HEAD
   [1.2.0]: https://github.com/org/repo/compare/v1.1.0...v1.2.0
   [1.1.0]: https://github.com/org/repo/compare/v1.0.0...v1.1.0
   ```

6. **Handle the Unreleased section**:
   - Always maintain an `[Unreleased]` section at the top for changes not yet in a release.
   - When cutting a new release: move Unreleased items into a new version section, add the date, and create a fresh empty Unreleased section.
   - Link the Unreleased section to the diff from the latest tag to HEAD.

7. **Version number determination**:
   - **Patch** (1.0.x): Only bug fixes, no new features, no breaking changes.
   - **Minor** (1.x.0): New features, no breaking changes. May include bug fixes.
   - **Major** (x.0.0): Breaking changes. May include new features and bug fixes.
   - If the commits include any `BREAKING CHANGE`, it must be a major version bump.

8. **Automation options**:
   - Use `conventional-changelog-cli` for Node.js projects: `npx conventional-changelog -p angular -i CHANGELOG.md -s`.
   - Use `git-cliff` for a standalone tool with customizable templates.
   - Integrate into CI: auto-generate changelog on tag creation and attach to GitHub Release.
   - For updating an existing `CHANGELOG.md`: read the file, parse the current content, prepend the new version section after `## [Unreleased]`, and update comparison links.

Always output the changelog in proper markdown, ready to write to `CHANGELOG.md`.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
