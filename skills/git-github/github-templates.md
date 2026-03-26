---
description: Create GitHub issue templates, PR templates, and template chooser with structured forms and checklists
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in creating GitHub issue and PR templates. When setting up templates, follow these steps:

1. **Create the template directory structure**:
   - Create `.github/ISSUE_TEMPLATE/` for issue templates.
   - Issue templates can be YAML forms (`.yml`) or Markdown (`.md`). YAML forms are preferred — they provide structured input fields.
   - PR templates go at `.github/pull_request_template.md` (single template) or `.github/PULL_REQUEST_TEMPLATE/` (multiple templates).

2. **Create a bug report template** (`.github/ISSUE_TEMPLATE/bug_report.yml`):
   - Name: "Bug Report", description, labels: `["bug"]`.
   - Fields:
     - **Description** (textarea, required): "A clear description of the bug."
     - **Steps to Reproduce** (textarea, required): Numbered steps. Placeholder with example steps.
     - **Expected Behavior** (textarea, required): What should happen.
     - **Actual Behavior** (textarea, required): What actually happens.
     - **Environment** (dropdown or textarea): OS, browser/runtime version, app version.
     - **Screenshots** (textarea, optional): "If applicable, add screenshots."
     - **Additional Context** (textarea, optional): Logs, error messages, workarounds tried.
   - Use `validations: required: true` for critical fields.

3. **Create a feature request template** (`.github/ISSUE_TEMPLATE/feature_request.yml`):
   - Name: "Feature Request", labels: `["enhancement"]`.
   - Fields:
     - **Problem Statement** (textarea, required): "What problem does this feature solve?" Encourage "As a [user], I want [goal] so that [benefit]."
     - **Proposed Solution** (textarea, required): The desired feature or behavior.
     - **Alternatives Considered** (textarea, optional): Other solutions explored and why they were rejected.
     - **Additional Context** (textarea, optional): Mockups, examples from other tools, priority/urgency.
   - Keep it focused on the problem, not just the solution — this enables better discussion.

4. **Create a question/support template** (optional, `.github/ISSUE_TEMPLATE/question.yml`):
   - Name: "Question", labels: `["question"]`.
   - Fields:
     - **Question** (textarea, required): The question in detail.
     - **What I've Tried** (textarea, optional): Research and attempts already made.
     - **Context** (textarea, optional): Version, environment, relevant code.
   - Consider redirecting questions to GitHub Discussions instead (see step 6).

5. **Create the PR template** (`.github/pull_request_template.md`):
   ```markdown
   ## Description
   <!-- Describe your changes in detail. What does this PR do? -->

   ## Related Issue
   <!-- Link to the issue this PR addresses: Fixes #(issue number) -->

   ## Type of Change
   - [ ] Bug fix (non-breaking change that fixes an issue)
   - [ ] New feature (non-breaking change that adds functionality)
   - [ ] Breaking change (fix or feature that would cause existing functionality to change)
   - [ ] Documentation update
   - [ ] Refactoring (no functional changes)

   ## How Has This Been Tested?
   <!-- Describe the tests you ran and how to reproduce them -->

   ## Checklist
   - [ ] My code follows the project's style guidelines
   - [ ] I have performed a self-review of my code
   - [ ] I have added tests that prove my fix/feature works
   - [ ] New and existing tests pass locally
   - [ ] I have updated the documentation accordingly
   - [ ] My changes generate no new warnings
   ```
   - Keep the checklist relevant — remove items that don't apply to your project.
   - Use HTML comments for instructions that should not appear in the final PR.

6. **Configure the template chooser** (`.github/ISSUE_TEMPLATE/config.yml`):
   ```yaml
   blank_issues_enabled: false
   contact_links:
     - name: Questions & Support
       url: https://github.com/org/repo/discussions/categories/q-a
       about: Ask questions and get help from the community.
     - name: Documentation
       url: https://docs.example.com
       about: Check the documentation for guides and API reference.
     - name: Security Vulnerabilities
       url: https://github.com/org/repo/security/advisories/new
       about: Report security vulnerabilities privately.
   ```
   - Set `blank_issues_enabled: false` to force users to use templates (prevents low-quality issues).
   - Add links to discussions, docs, and security advisories to redirect common queries.

7. **Best practices for templates**:
   - Keep templates concise — long templates discourage submissions.
   - Use placeholder text to show examples of good input.
   - Mark only truly essential fields as required.
   - Add assignees and labels automatically via template metadata.
   - Test templates by creating test issues/PRs to verify formatting.
   - Review and update templates quarterly based on the quality of incoming issues/PRs.

8. **Verify the templates**:
   - Check YAML syntax: validate with a YAML linter.
   - Test by navigating to the repository's "New Issue" page on GitHub.
   - Ensure the template chooser appears with all options.
   - Create a test issue with each template to verify fields render correctly.
   - Verify labels referenced in templates exist in the repository.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
