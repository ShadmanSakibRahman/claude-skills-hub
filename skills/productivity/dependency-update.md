---
description: Update dependencies safely with changelog review, incremental updates, testing, and separate commits
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in dependency management and safe upgrade strategies. When asked to update dependencies, follow these steps:

**Step 1: Audit Current Dependencies**
- Run the package manager's outdated command to list all packages with available updates.
  - npm/pnpm: `pnpm outdated` or `npm outdated`.
  - pip: `pip list --outdated`.
  - bundler: `bundle outdated`.
- Categorize updates by severity: patch (0.0.x), minor (0.x.0), major (x.0.0).
- Identify security vulnerabilities: `pnpm audit`, `npm audit`, `pip-audit`, `bundler-audit`.
- List dev dependencies separately from production dependencies.

**Step 2: Prioritize Updates**
- **Critical priority**: Security vulnerabilities (update immediately).
- **High priority**: Major framework updates (Next.js, React, Vue) that unlock new features.
- **Medium priority**: Minor version updates with useful improvements.
- **Low priority**: Patch updates and dev dependency updates.
- For major updates, check the migration guide before proceeding.
- Identify dependencies that must be updated together (peer dependency groups).

**Step 3: Research Breaking Changes**
- For each major or significant minor update, review:
  - The CHANGELOG.md or release notes on GitHub.
  - The migration guide (if available).
  - Common issues reported in GitHub issues or discussions.
- Identify breaking changes that affect the codebase: API changes, removed features, new requirements.
- Note any new peer dependency requirements.
- Create a list of code changes needed for each breaking change.

**Step 4: Update One at a Time**
- Start with the most critical update (security fixes first).
- Update a single package or a tightly coupled group:
  - `pnpm update package-name@latest` for a specific package.
  - `pnpm update @scope/*` for scoped packages.
- For major updates: `pnpm add package-name@latest` to update beyond the semver range.
- After each update, verify the lock file changed correctly.

**Step 5: Test After Each Update**
- Run the linter to catch any new type or import errors: `pnpm lint`.
- Run the type checker: `pnpm tsc --noEmit` or equivalent.
- Run the test suite: `pnpm test`.
- Build the project: `pnpm build` to catch build-time issues.
- If tests or build fail, fix the issues before moving to the next update.
- For UI dependencies: manually verify critical pages render correctly.

**Step 6: Apply Breaking Change Fixes**
- Update import paths if the package changed its export structure.
- Replace deprecated API calls with their recommended replacements.
- Update configuration files if the package changed its config format.
- Adjust TypeScript types if the package changed its type definitions.
- Update any wrapper utilities that depend on the package's API.

**Step 7: Commit and Document**
- Create a separate commit for each dependency update (or logical group).
- Use a consistent commit message format: `chore(deps): update package-name to vX.Y.Z`.
- For major updates with code changes: include the migration details in the commit body.
- After all updates, run the full test suite one final time.
- Update any documentation that references specific dependency versions.
- If a dependency cannot be safely updated, document why and create a tracking issue.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
