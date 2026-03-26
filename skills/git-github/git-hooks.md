---
description: Set up Git hooks with Husky and pre-commit for linting, commit validation, pre-push tests, and branch enforcement
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in Git hooks and developer workflow automation. When setting up Git hooks, follow these steps:

1. **Choose the hook management tool**:
   - **JavaScript/TypeScript projects**: Use Husky v9+ with lint-staged. Install: `npm install -D husky lint-staged`.
   - **Python projects**: Use `pre-commit` framework. Install: `pip install pre-commit`, then create `.pre-commit-config.yaml`.
   - **Other languages**: Use Husky (if Node.js is in the toolchain) or manual `.git/hooks/` scripts with a setup script.
   - Check if the project already has hooks configured — look for `.husky/`, `.pre-commit-config.yaml`, or `lefthook.yml`.

2. **Initialize Husky** (JavaScript/TypeScript):
   - Run `npx husky init` to create the `.husky/` directory and add the `prepare` script to `package.json`.
   - This creates `.husky/pre-commit` as a starting point.
   - Hooks are shell scripts in `.husky/` — they run via Git's hook mechanism.
   - Ensure `"prepare": "husky"` is in `package.json` scripts so hooks install automatically after `npm install`.

3. **Configure lint-staged for pre-commit**:
   - Add lint-staged config to `package.json` or `.lintstagedrc`:
     ```
     "lint-staged": {
       "*.{ts,tsx}": ["eslint --fix", "prettier --write"],
       "*.{css,scss}": ["prettier --write"],
       "*.{json,md}": ["prettier --write"]
     }
     ```
   - In `.husky/pre-commit`: `npx lint-staged`.
   - lint-staged only processes staged files — fast even in large repos.
   - Configure different commands per file type for optimal performance.

4. **Set up commit message validation** (commitlint):
   - Install: `npm install -D @commitlint/cli @commitlint/config-conventional`.
   - Create `commitlint.config.js`: `module.exports = { extends: ['@commitlint/config-conventional'] };`.
   - Create `.husky/commit-msg`: `npx --no -- commitlint --edit $1`.
   - Customize rules if needed: allowed types, max subject length, scope requirements.
   - This enforces conventional commit format on every commit.

5. **Set up pre-push hooks**:
   - Create `.husky/pre-push` with test commands: `npm test` or `npm run test:ci`.
   - Keep pre-push checks fast — run only critical tests, not the full suite.
   - Consider running type checking: `npx tsc --noEmit`.
   - Optionally check for console.log statements or debug code.
   - Allow bypassing in emergencies with `git push --no-verify` (document when this is acceptable).

6. **Branch name enforcement**:
   - Create a pre-commit or pre-push hook that validates the branch name:
     ```
     branch=$(git rev-parse --abbrev-ref HEAD)
     if ! echo "$branch" | grep -qE '^(feature|fix|hotfix|release|chore)/[a-z0-9._-]+$|^(main|develop)$'; then
       echo "Branch name '$branch' does not match the required pattern."
       exit 1
     fi
     ```
   - Allow `main`, `develop`, and patterned branches (feature/, fix/, etc.).
   - Print a helpful error message showing the expected format.

7. **Python pre-commit framework setup**:
   - Create `.pre-commit-config.yaml` with hooks:
     ```
     repos:
       - repo: https://github.com/pre-commit/pre-commit-hooks
         rev: v4.5.0
         hooks: [trailing-whitespace, end-of-file-fixer, check-yaml, check-json, check-added-large-files]
       - repo: https://github.com/astral-sh/ruff-pre-commit
         rev: v0.3.0
         hooks: [ruff, ruff-format]
       - repo: https://github.com/pre-commit/mirrors-mypy
         rev: v1.8.0
         hooks: [mypy]
     ```
   - Run `pre-commit install` to install the hooks.
   - Run `pre-commit run --all-files` for initial validation.
   - Add `pre-commit autoupdate` to your maintenance routine.

8. **Performance considerations**:
   - Keep pre-commit hooks under 10 seconds — developers will bypass slow hooks.
   - Use lint-staged to only process changed files, not the whole codebase.
   - Run expensive checks (full test suite, E2E tests) in CI, not in hooks.
   - Cache tool installations (pre-commit caches automatically).
   - Provide clear error messages so developers know how to fix issues.

9. **Team onboarding**:
   - Document the hooks in `CONTRIBUTING.md`: what they do, how to set up, how to bypass when needed.
   - Ensure hooks install automatically: Husky's `prepare` script, or a `make setup` target.
   - Test that hooks work on macOS, Linux, and Windows (Git Bash/WSL).
   - If a hook blocks a valid commit, fix the hook — never just tell developers to skip it.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
