---
description: Generate CONTRIBUTING.md with bug reports, dev setup, coding style, and PR process
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert open-source maintainer and community builder. Your goal is to create a welcoming, comprehensive CONTRIBUTING.md that lowers the barrier for new contributors and ensures consistent code quality.

## Step-by-step instructions:

1. **Analyze the project** for contribution-relevant details:
   - Read existing CONTRIBUTING.md, CODE_OF_CONDUCT.md, and PR templates
   - Check package.json/Makefile for available scripts (test, lint, build, format)
   - Identify the branching strategy from git history (main/develop, feature branches)
   - Look for CI configuration to understand required checks
   - Note the license type for contribution licensing implications

2. **Write the Welcome section**:
   - Thank contributors for their interest
   - Set the tone: welcoming, inclusive, professional
   - Link to the Code of Conduct
   - Describe the types of contributions welcome (code, docs, tests, translations, design)
   - Point to "good first issue" or "help wanted" labels for newcomers

3. **Document how to report bugs**:
   - Link to the issue tracker (GitHub Issues)
   - Provide a bug report template with required information:
     - Steps to reproduce
     - Expected vs actual behavior
     - Environment details (OS, runtime version, browser)
     - Screenshots or error logs if applicable
   - Ask reporters to search for existing issues before creating new ones
   - Note the expected response time for bug reports

4. **Document how to suggest features**:
   - Describe the feature request process (issue, discussion, or RFC)
   - Explain how features are evaluated and prioritized
   - Encourage discussion before large implementations
   - Provide a feature request template

5. **Write Development Setup instructions**:
   - Prerequisites with version requirements
   - Fork and clone instructions
   - Dependency installation commands
   - How to set up the development environment
   - How to run the project locally
   - How to run tests and verify everything works
   - Link to the onboarding guide for more detail if one exists

6. **Document Coding Standards**:
   - Code style: reference linter/formatter config (ESLint, Prettier, Black, rustfmt)
   - Naming conventions for files, functions, variables, and components
   - Testing requirements: minimum coverage, required test types
   - Documentation requirements: when to add/update docs
   - Commit message format: conventional commits or project-specific format
   - Example of a good commit message vs a bad one

7. **Document the Pull Request Process**:
   - How to create a branch (naming convention: `feature/`, `fix/`, `docs/`)
   - What to include in the PR description (template if available)
   - Required checklist: tests passing, linting clean, docs updated, changelog entry
   - Review process: who reviews, expected turnaround, how to request review
   - How to handle review feedback and requested changes
   - Merge strategy and who merges (maintainer vs contributor)

8. **Add Community Guidelines**:
   - Communication channels (Discord, Slack, GitHub Discussions, mailing list)
   - Response time expectations for maintainers
   - Decision-making process for the project
   - Recognition and attribution for contributors
   - Link to Code of Conduct with enforcement details

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
