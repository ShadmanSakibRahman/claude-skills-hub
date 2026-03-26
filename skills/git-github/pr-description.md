---
description: Generate detailed PR descriptions with summary, motivation, implementation details, testing, and reviewer checklist
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in writing clear, comprehensive pull request descriptions. When generating a PR description, follow these steps:

1. **Analyze all changes in the branch**:
   - Run `git log --oneline main..HEAD` (or the appropriate base branch) to see all commits.
   - Run `git diff main..HEAD --stat` to see all changed files and their scope.
   - Run `git diff main..HEAD` to understand the actual code changes.
   - Look at all commits, not just the latest — the PR includes the full branch history.

2. **Write the PR title** (under 70 characters):
   - Use the same format as commit messages: `type(scope): description`.
   - Summarize the overall change, not individual commits.
   - Be specific: "Add OAuth2 Google login with session management" not "Auth updates".
   - If the PR addresses an issue, do not put the issue number in the title — put it in the body.

3. **Write the Summary section**:
   - 2-5 bullet points explaining what the PR does at a high level.
   - Focus on the user-visible or developer-visible impact.
   - Each bullet should be a complete thought, not a file name.
   - Example: "Adds Google OAuth2 login flow with automatic account creation for new users" not "Modified auth.ts".

4. **Write the Motivation section**:
   - Explain WHY this change is needed. Link to the issue/ticket: `Closes #123` or `Relates to JIRA-456`.
   - Describe the problem being solved or the feature being added.
   - If there was a bug, describe the symptoms and root cause.
   - Mention any user feedback or metrics that motivated the change.

5. **Describe the Implementation approach**:
   - Explain the key technical decisions and trade-offs.
   - Describe the architecture: new files, modified modules, data flow.
   - Explain why this approach was chosen over alternatives.
   - Highlight any non-obvious design decisions that reviewers should understand.
   - Note any patterns or conventions followed.

6. **Document Testing**:
   - List what was tested: unit tests added/modified, integration tests, manual testing.
   - Describe manual testing steps if applicable.
   - Note test coverage for the changes.
   - Mention edge cases that were specifically tested.
   - If UI changes: describe how to visually verify.

7. **Add Screenshots/Recordings** (for UI changes):
   - Describe before and after states.
   - Note: "Include screenshot of [specific UI element] showing [specific state]."
   - Suggest specific screen sizes or states to capture.
   - For animations or flows, suggest a screen recording.

8. **Flag Breaking Changes and Migration**:
   - Clearly label any breaking changes with a "Breaking Changes" section.
   - Provide migration instructions for consumers of the changed API.
   - Note deprecated features and their replacements.
   - Include example code showing the old way vs new way.

9. **Add Deployment Notes**:
   - List required environment variables, feature flags, or configuration changes.
   - Note database migrations that need to run.
   - Specify deployment order if there are dependencies.
   - Mention any monitoring or alerting to set up.

10. **Create a Reviewer Checklist**:
    - Include a markdown checklist of areas to focus on during review.
    - Highlight files or sections that need extra scrutiny.
    - Note any areas where you are unsure and want specific feedback.
    - Example: `- [ ] Error handling in the OAuth callback is sufficient`.

Output the PR description in markdown format, ready to paste into GitHub's PR creation form.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
