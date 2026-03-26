---
description: Create comprehensive .gitignore files tailored to the project's tech stack covering all common artifacts
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in configuring Git ignore rules. When creating or updating a `.gitignore` file, follow these steps:

1. **Detect the project's tech stack**:
   - Check for `package.json` (Node.js/JavaScript/TypeScript), `requirements.txt`/`pyproject.toml` (Python), `Cargo.toml` (Rust), `go.mod` (Go), `pom.xml`/`build.gradle` (Java), `Gemfile` (Ruby), `pubspec.yaml` (Flutter/Dart), `*.csproj` (C#/.NET).
   - Check for frameworks: React, Next.js, Angular, Vue, Django, Flask, Rails, Spring Boot.
   - Check for infrastructure: Docker, Terraform, Kubernetes configs.
   - Read existing `.gitignore` to preserve custom rules.

2. **Add dependency directories**:
   - Node.js: `node_modules/`, `.pnp.*`, `.yarn/cache`, `.yarn/unplugged`.
   - Python: `venv/`, `.venv/`, `env/`, `__pycache__/`, `*.pyc`, `*.pyo`, `.eggs/`, `*.egg-info/`.
   - Go: `vendor/` (if not vendoring intentionally).
   - Ruby: `vendor/bundle/`.
   - Dart/Flutter: `.dart_tool/`, `.packages`.
   - .NET: `packages/`.

3. **Add build artifacts**:
   - General: `dist/`, `build/`, `out/`, `target/`.
   - JavaScript/TypeScript: `.next/`, `.nuxt/`, `.output/`, `.turbo/`, `*.tsbuildinfo`.
   - Python: `*.egg`, `*.whl`, `dist/`, `build/`, `*.so`.
   - Java: `*.class`, `*.jar`, `*.war`, `target/`.
   - .NET: `bin/`, `obj/`.
   - Rust: `target/`.
   - Flutter: `build/`, `.flutter-plugins`, `.flutter-plugins-dependencies`.

4. **Add environment and secret files**:
   - `.env`, `.env.local`, `.env.*.local` — never commit secrets.
   - `.env.development` and `.env.production` only if they contain secrets (sometimes these are committed with non-secret defaults).
   - `*.pem`, `*.key`, `*.cert`, `*.p12` — private keys and certificates.
   - `credentials.json`, `service-account.json`, `secrets.yaml`.
   - `*.secret`, `.secret.*`.

5. **Add IDE and editor files**:
   - VS Code: `.vscode/` (or selectively keep `settings.json` and `extensions.json`).
   - JetBrains (IntelliJ, WebStorm, PyCharm): `.idea/`, `*.iml`, `*.iws`.
   - Vim: `*.swp`, `*.swo`, `*~`, `.vim/`.
   - Emacs: `*~`, `\#*\#`, `.dir-locals.el`.
   - Sublime Text: `*.sublime-project`, `*.sublime-workspace`.

6. **Add OS-specific files**:
   - macOS: `.DS_Store`, `.AppleDouble`, `.LSOverride`, `._*`, `.Spotlight-V100`, `.Trashes`.
   - Windows: `Thumbs.db`, `ehthumbs.db`, `Desktop.ini`, `$RECYCLE.BIN/`.
   - Linux: `*~`, `.fuse_hidden*`, `.Trash-*`.

7. **Add testing and coverage artifacts**:
   - `coverage/`, `.coverage`, `htmlcov/`, `*.lcov`.
   - `.nyc_output/`, `jest-coverage/`.
   - `*.test-result`, `test-results/`.
   - `.pytest_cache/`, `.mypy_cache/`, `.ruff_cache/`.

8. **Add generated and miscellaneous files**:
   - Logs: `*.log`, `logs/`, `npm-debug.log*`, `yarn-debug.log*`.
   - Lock files (project-dependent): generally DO commit `package-lock.json`, `yarn.lock`, `Pipfile.lock`, `poetry.lock`. Do NOT commit `Gemfile.lock` for libraries.
   - Compiled output: `*.o`, `*.obj`, `*.dll`, `*.dylib`.
   - Database files: `*.sqlite`, `*.db` (local dev databases only).
   - Temporary files: `tmp/`, `temp/`, `.tmp/`.

9. **Organize the file**:
   - Group rules with comment headers: `# Dependencies`, `# Build`, `# Environment`, `# IDE`, `# OS`, `# Testing`, `# Misc`.
   - Order from most important (dependencies, secrets) to least (OS files).
   - Use negation patterns sparingly: `!.gitkeep` to track empty directories.
   - Add a note at the top: `# Project-specific ignores` for custom rules.

10. **Verify the result**:
    - Run `git status` to ensure currently tracked files are not affected.
    - If a file that should be ignored is already tracked: `git rm --cached <file>` to stop tracking without deleting.
    - Test patterns: `git check-ignore -v <filepath>` to verify a specific file is ignored.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
