---
description: Generate release notes from commits and PRs between tags with categorized changes and migration instructions
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in generating clear, useful release notes. When creating release notes, follow these steps:

1. **Identify the version range**:
   - Find the latest tag: `git describe --tags --abbrev=0`.
   - Find the previous tag: `git describe --tags --abbrev=0 HEAD~1` or `git tag --sort=-version:refname | head -5`.
   - Get commits between tags: `git log v1.1.0..v1.2.0 --oneline --no-merges`.
   - Get PRs merged between tags: `git log v1.1.0..v1.2.0 --merges --oneline` or use `gh pr list --state merged --base main`.
   - If no tags exist, compare against the previous release branch or a specific commit.

2. **Categorize changes**:
   - Parse commit messages for conventional commit types or PR labels.
   - Categories and their display order:
     - **Breaking Changes**: Any `BREAKING CHANGE` footer or `!` after type. Always list first with a warning symbol.
     - **New Features**: `feat` commits. What users can now do that they couldn't before.
     - **Bug Fixes**: `fix` commits. What was broken and is now working.
     - **Performance Improvements**: `perf` commits.
     - **Documentation**: `docs` commits (optional — sometimes omitted from user-facing notes).
     - **Other Changes**: `refactor`, `chore`, `test`, `ci` (summarize briefly or omit for user-facing notes).
   - If commits do not follow conventional commits, categorize manually by reading the diffs.

3. **Write user-friendly descriptions**:
   - Rewrite terse commit messages into clear, user-facing language.
   - Focus on the impact: "Users can now export reports as PDF" not "add PDF export module".
   - Group related changes: if 5 commits all improve the search feature, write one bullet summarizing the overall improvement.
   - Link to PRs or issues: `Add dark mode support (#234)`.
   - Credit contributors: `Thanks to @username for contributing this feature!`

4. **Highlight breaking changes prominently**:
   - List each breaking change with a clear description of what changed.
   - Explain the migration path: what users or developers need to do.
   - Provide before/after code examples for API changes.
   - If there are many breaking changes, consider a separate "Migration Guide" section.

5. **Include migration instructions** (for major or breaking releases):
   - Step-by-step upgrade guide from the previous version.
   - Required configuration changes, environment variables, or database migrations.
   - Deprecated features and their replacements with timelines.
   - Minimum dependency version requirements.

6. **Credit contributors**:
   - List all contributors for the release: `git log v1.1.0..v1.2.0 --format='%aN' | sort -u`.
   - Highlight first-time contributors: "Welcome @newuser to the project!"
   - Thank reviewers and testers if applicable.

7. **Add metadata**:
   - Release date.
   - Version number following semver: major (breaking), minor (features), patch (fixes).
   - Link to the full diff: `https://github.com/org/repo/compare/v1.1.0...v1.2.0`.
   - Link to the release on the package registry (npm, PyPI, etc.) if applicable.
   - Docker image tag or download links if applicable.

8. **Format the output**:
   - Use markdown with clear headers for each category.
   - Use bullet points for individual changes.
   - Keep it scannable — busy users should understand the release in 30 seconds.
   - For GitHub Releases: use `gh release create v1.2.0 --title "v1.2.0" --notes-file release-notes.md`.

Generate the release notes in markdown format, ready for GitHub Releases, a CHANGELOG file, or a blog post.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
