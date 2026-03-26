---
description: Set up linting and formatting with ESLint, Prettier, Ruff, Biome, rustfmt, or clippy including pre-commit hooks and editor config
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in code quality tooling. Set up comprehensive linting and formatting that enforces consistent code style across the team.

Follow these steps precisely:

1. **Detect the Project Stack**: Identify the language and existing tools:
   - JavaScript/TypeScript: Check for existing `.eslintrc`, `prettier.config`, `biome.json`.
   - Python: Check for `pyproject.toml` (Ruff, Black, isort), `setup.cfg`, `.flake8`.
   - Rust: Check for `rustfmt.toml`, `clippy.toml`.
   - Go: Check for `golangci-lint` config.
   - Read `package.json`, `pyproject.toml`, `Cargo.toml` for existing lint dependencies.

2. **Install Required Packages**: Generate the install command:
   - JS/TS with ESLint+Prettier: `eslint`, `prettier`, `eslint-config-prettier`, `eslint-plugin-import`, framework-specific plugins (React, Vue, Next.js).
   - JS/TS with Biome: `@biomejs/biome` (replaces both ESLint and Prettier).
   - Python with Ruff: `ruff` (replaces flake8, isort, pyflakes, and more).
   - Include TypeScript parser and plugin if TypeScript is used.

3. **Configure the Linter**: Create or update config files with:
   - **Rules**: Start with a recommended preset, then customize. Enable rules that catch bugs (no-unused-vars, no-implicit-coercion). Disable overly opinionated rules that cause friction.
   - **Environments**: Set browser, node, es2022 as appropriate.
   - **Overrides**: Different rules for test files (allow devDependencies, longer lines).
   - **Ignore Patterns**: Ignore build output, node_modules, generated files.
   - Document the reasoning for any non-default rule settings.

4. **Configure the Formatter**: Set up auto-formatting:
   - Print width (80-120), tab width, single vs double quotes, semicolons, trailing commas.
   - Match existing project conventions if code already exists.
   - Create `.prettierrc` or equivalent with explicit settings.
   - Create `.prettierignore` for files that shouldn't be formatted.

5. **Create Editor Config**: Write `.editorconfig` file:
   - Set indent style (spaces/tabs), indent size, end of line, charset.
   - Configure per-file-type overrides (YAML uses 2 spaces, Python uses 4).
   - Ensure trim trailing whitespace and insert final newline.

6. **Set Up Pre-commit Hooks**: Configure automatic linting on commit:
   - JS/TS: Use `husky` + `lint-staged` to run linter only on staged files.
   - Python: Use `pre-commit` framework with `.pre-commit-config.yaml`.
   - Configure to run lint, format check, and type check on staged files.
   - Add the hook installation to the project setup instructions.

7. **Add NPM/Package Scripts**: Create convenience scripts:
   - `lint`: Run linter on entire project.
   - `lint:fix`: Auto-fix all fixable issues.
   - `format`: Format all files.
   - `format:check`: Check formatting without changing files (for CI).

8. **CI Integration**: Suggest CI pipeline additions:
   - Run lint check, format check, and type check in CI.
   - Fail the build on any linting errors.
   - Provide the CI configuration snippet.

Apply the new config to the existing codebase incrementally. Run the formatter first, then fix linting errors in priority order.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
