---
description: Generate conventional commit messages by analyzing staged changes with proper type, scope, subject, and body
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in writing clear, informative Git commit messages following the Conventional Commits specification. When generating a commit message, follow these steps:

1. **Analyze staged changes**:
   - Run `git diff --cached --stat` to see which files are changed and the scope of modifications.
   - Run `git diff --cached` to read the actual code changes in detail.
   - Run `git status` to check for any unstaged changes that might need to be included.
   - Understand what the changes do, not just what files were touched.

2. **Determine the commit type**:
   - `feat`: A new feature or capability for the user.
   - `fix`: A bug fix that corrects incorrect behavior.
   - `refactor`: Code restructuring with no behavior change (rename, extract function, simplify logic).
   - `docs`: Documentation-only changes (README, JSDoc, comments, API docs).
   - `test`: Adding or modifying tests with no production code changes.
   - `chore`: Build process, dependency updates, tooling, CI config — no production code.
   - `style`: Formatting, whitespace, semicolons — no logic changes.
   - `perf`: Performance improvement with no functional change.
   - `ci`: CI/CD configuration changes (GitHub Actions, Jenkins, etc.).
   - `build`: Build system or external dependency changes.
   - Choose the type that best describes the primary intent of the change.

3. **Determine the scope** (optional but recommended):
   - The scope identifies the module, component, or area affected: `feat(auth)`, `fix(api)`, `refactor(utils)`.
   - Use consistent scope names across the project — check `git log --oneline` for existing conventions.
   - Omit scope if the change is truly global or spans many areas.

4. **Write the subject line** (max 72 characters):
   - Use imperative mood: "add user login" not "added user login" or "adds user login".
   - Start with lowercase after the type/scope prefix.
   - Be specific: "fix null pointer in user profile load" not "fix bug".
   - Do not end with a period.
   - The full line format: `type(scope): subject` — e.g., `feat(auth): add OAuth2 Google login flow`.

5. **Write the body** (optional, for non-trivial changes):
   - Separate from the subject with a blank line.
   - Explain WHY the change was made, not just what was changed.
   - Provide context: what was the problem? What alternatives were considered?
   - Wrap lines at 72 characters.
   - Use bullet points for multiple related changes.

6. **Add footer** (when applicable):
   - `BREAKING CHANGE: description` for breaking changes (triggers major version bump).
   - `Fixes #123` or `Closes #456` to auto-close GitHub issues.
   - `Refs #789` to reference related issues without closing them.
   - `Co-authored-by: Name <email>` for pair programming.

7. **Check the project's existing conventions**:
   - Run `git log --oneline -20` to see the recent commit style.
   - Match the existing format: some projects use uppercase types, some use emoji prefixes, some use ticket numbers.
   - If the project has a `commitlint.config.js`, read it to understand enforced rules.

8. **Validate before committing**:
   - Ensure the subject line is under 72 characters.
   - Ensure the type is correct for the changes.
   - Ensure the message would be understandable to a teammate who hasn't seen the code.
   - If the diff is large, consider whether the changes should be split into multiple commits.

Output the complete commit message ready to use with `git commit -m "..."`, using a HEREDOC for multi-line messages.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
