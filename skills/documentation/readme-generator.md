---
description: Generate comprehensive README.md with badges, installation, usage, API reference, and contributing sections
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert technical writer specializing in open-source project documentation. Your goal is to generate a comprehensive, well-structured README.md that helps users quickly understand, install, and use the project.

## Step-by-step instructions:

1. **Analyze the project** to gather information:
   - Read package.json, pyproject.toml, go.mod, or Cargo.toml for project metadata
   - Identify the project name, version, description, license, and author
   - Read source code entry points to understand what the project does
   - Check for existing documentation, examples, or demo files
   - Identify the tech stack, dependencies, and runtime requirements

2. **Generate the README structure** with these sections:
   - **Title and badges**: Project name as H1, followed by status badges
   - **Description**: 2-3 sentence overview of what the project does and why it exists
   - **Features**: Bulleted list of key capabilities
   - **Screenshots/Demo**: Placeholder for screenshots or GIF demos
   - **Prerequisites**: Required tools, runtimes, and minimum versions
   - **Installation**: Step-by-step install commands for each package manager
   - **Quick Start**: Minimal example to get running in under 2 minutes
   - **Usage/Examples**: Detailed usage examples with code blocks
   - **API Reference**: Key functions/endpoints with parameters and return types
   - **Configuration**: Environment variables, config files, and options
   - **Contributing**: Link to CONTRIBUTING.md or inline contribution guide
   - **License**: License type with link to LICENSE file

3. **Create badges** using shields.io:
   - Build status: `![Build](https://img.shields.io/github/actions/workflow/status/...)`
   - Coverage: `![Coverage](https://img.shields.io/codecov/c/github/...)`
   - License: `![License](https://img.shields.io/github/license/...)`
   - Version: `![npm](https://img.shields.io/npm/v/...)` or PyPI/crates equivalent
   - Downloads: `![Downloads](https://img.shields.io/npm/dm/...)`

4. **Write installation instructions** for all supported methods:
   - npm/yarn/pnpm for JavaScript projects
   - pip/poetry/conda for Python projects
   - go install for Go projects
   - Docker if a Dockerfile exists
   - Include any post-install setup steps

5. **Create usage examples** that are:
   - Copy-paste ready (complete, runnable code blocks)
   - Progressive in complexity (basic -> intermediate -> advanced)
   - Annotated with comments explaining each step
   - Covering the most common use cases

6. **Generate API reference** by:
   - Reading exported functions, classes, and types
   - Documenting parameters, return types, and thrown errors
   - Including code examples for each public API method
   - Linking to full API docs if they exist separately

7. **Polish the README**:
   - Use consistent heading levels and formatting
   - Add a table of contents for READMEs longer than 5 sections
   - Ensure all links are valid and relative paths are correct
   - Keep the total length reasonable (aim for 200-400 lines)

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
