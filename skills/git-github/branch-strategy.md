---
description: Set up Git branching strategy with branch protection, naming conventions, and merge strategies
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in Git branching strategies and repository workflows. When setting up or advising on a branching strategy, follow these steps:

1. **Assess the team and project needs**:
   - Team size: solo, small team (2-5), large team (5+).
   - Release cadence: continuous deployment, scheduled releases, or long-lived versions.
   - Environment count: just production, or dev/staging/production.
   - Existing workflow: check `git branch -r` for current branch structure and `git log --oneline --graph -20` for merge patterns.

2. **Choose the strategy**:
   - **GitHub Flow** (recommended for most teams): Single `main` branch that is always deployable. Create feature branches from `main`, open PRs, merge back to `main`, deploy. Best for: continuous deployment, small-medium teams, web apps.
   - **Git Flow**: `main` (production) + `develop` (integration) + feature/release/hotfix branches. Best for: scheduled releases, versioned software, multiple supported versions.
   - **Trunk-Based Development**: Very short-lived branches (< 1 day) or commit directly to `main`. Use feature flags for incomplete work. Best for: experienced teams with strong CI/CD and test coverage.

3. **Define naming conventions**:
   - Feature branches: `feature/short-description` or `feature/TICKET-123-short-description`.
   - Bug fixes: `fix/short-description` or `bugfix/TICKET-456-description`.
   - Hotfixes: `hotfix/critical-issue-description`.
   - Release branches (Git Flow): `release/v1.2.0`.
   - Use lowercase, hyphens between words, no special characters.
   - Keep names short but descriptive — they appear in merge commits and logs.

4. **Configure branch protection rules** (via GitHub settings or `gh` CLI):
   - Protect `main` (and `develop` if using Git Flow):
     - Require pull request reviews: at least 1 approval (2 for large teams).
     - Require status checks to pass: CI tests, linting, build.
     - Require branches to be up to date before merging.
     - Require signed commits (optional but recommended for open source).
     - Restrict who can push directly (admin override only for emergencies).
     - Do not allow force pushes or branch deletion.
   - Apply rules using: `gh api repos/{owner}/{repo}/branches/main/protection -X PUT --input protection.json`.

5. **Choose merge strategy**:
   - **Squash merge**: Combines all commits into one clean commit on `main`. Best for: feature branches with messy commit history. Keeps `main` history clean.
   - **Merge commit**: Creates a merge commit preserving all branch commits. Best for: when individual commits are meaningful and well-structured.
   - **Rebase merge**: Replays commits on top of `main` without a merge commit. Best for: linear history preference. Requires clean, atomic commits.
   - Recommendation: Squash merge for feature branches, merge commit for release branches.
   - Configure default in GitHub repo settings.

6. **Set up environment branches** (if applicable):
   - Map branches to environments: `main` -> production, `develop` or `staging` -> staging.
   - Configure CI/CD to auto-deploy when the mapped branch is updated.
   - For preview environments: deploy each PR to a temporary environment for testing.

7. **Define the workflow for common scenarios**:
   - **New feature**: Create branch from `main`, develop, push, open PR, get review, merge.
   - **Bug fix**: Same as feature but with `fix/` prefix.
   - **Hotfix**: Branch from `main`, fix, PR with expedited review, merge to `main`, cherry-pick to `develop` if using Git Flow.
   - **Release** (Git Flow): Branch from `develop`, version bump, final testing, merge to `main` and tag, merge back to `develop`.

8. **Document the strategy**:
   - Create a `CONTRIBUTING.md` with the branching strategy, naming conventions, and merge process.
   - Include examples of branch names and the full workflow for a typical feature.
   - Document any automation: auto-delete branches after merge, required labels, CI/CD triggers.
   - Add a diagram showing the branch flow if using Git Flow.

Keep the strategy as simple as possible — complexity leads to mistakes and slows development.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
