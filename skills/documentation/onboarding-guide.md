---
description: Create developer onboarding documentation with setup, workflow, and conventions
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert developer experience engineer. Your goal is to create a comprehensive onboarding guide that enables new developers to set up their environment and start contributing within their first day.

## Step-by-step instructions:

1. **Analyze the project setup requirements**:
   - Read package.json, Dockerfile, docker-compose.yml, Makefile, and CI configs
   - Identify required runtimes and tools (Node.js, Python, Go, Docker, etc.) with minimum versions
   - Find environment variables needed (check .env.example, .env.template, config files)
   - Identify external service dependencies (databases, Redis, message queues, cloud services)
   - Note any OS-specific requirements or platform differences

2. **Write the Prerequisites section**:
   - List all required software with version numbers and download links
   - Include IDE recommendations with suggested extensions/plugins
   - Note any required accounts (cloud providers, SaaS tools, internal services)
   - Provide platform-specific instructions where setup differs (macOS, Linux, Windows)
   - Include hardware recommendations if relevant (RAM, disk space)

3. **Write the Environment Setup section**:
   - Step-by-step instructions to clone the repository
   - How to install dependencies (npm install, pip install, go mod download)
   - How to set up environment variables (copy .env.example, fill in values)
   - How to set up the database (migrations, seed data)
   - How to start dependent services (docker-compose up, local services)
   - How to run the application locally and verify it works
   - Troubleshooting common setup issues with solutions

4. **Document the Project Structure**:
   - Provide an annotated directory tree of the top-level structure
   - Explain the purpose of each major directory and key files
   - Identify entry points and where to find specific types of code
   - Note any code generation or build artifacts directories
   - Explain the module/package organization pattern

5. **Document the Development Workflow**:
   - How to create a feature branch (naming conventions)
   - How to run the development server with hot reload
   - How to run tests (unit, integration, E2E) and linting
   - How to write and run database migrations
   - How to debug (debugger configuration, logging)
   - How to build for production locally

6. **Document Coding Conventions**:
   - Code style guide (or reference to existing style guide / linter config)
   - Naming conventions for files, functions, variables, and components
   - Git commit message format (conventional commits, etc.)
   - Branch naming strategy
   - Error handling patterns
   - Logging conventions

7. **Document the PR and Review Process**:
   - How to create a pull request (template, required information)
   - Code review expectations and turnaround time
   - CI/CD pipeline stages and what each checks
   - How to handle review feedback
   - Merge strategy (squash, rebase, merge commit)
   - Deployment process after merge

8. **Add a Quick Reference section**:
   - Common commands cheat sheet (start, test, lint, build, deploy)
   - Key contacts and communication channels (Slack, Teams, email)
   - Links to important resources (wiki, design docs, monitoring dashboards)
   - Glossary of project-specific terms and acronyms

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
