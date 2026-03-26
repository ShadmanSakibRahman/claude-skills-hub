---
description: Set up IDE workspace with VS Code settings, extensions, debug configs, tasks, snippets, and keybindings
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in developer tooling and IDE workspace configuration. When asked to set up a workspace, follow these steps:

**Step 1: Analyze the Project Stack**
- Identify the programming languages: TypeScript, JavaScript, Python, Go, Rust, etc.
- Identify the framework: Next.js, React, Vue, Svelte, Django, Rails, etc.
- Check for existing VS Code configuration in `.vscode/` directory.
- Determine the testing framework, linter, and formatter in use.
- Note the package manager and build tools.

**Step 2: Create VS Code Settings**
- Create or update `.vscode/settings.json` with project-specific settings:
  - Set the default formatter: `"editor.defaultFormatter": "esbenp.prettier-vscode"`.
  - Enable format on save: `"editor.formatOnSave": true`.
  - Configure ESLint: `"eslint.validate": ["javascript", "typescript", "typescriptreact"]`.
  - Set tab size and style to match the project convention.
  - Configure file associations for custom file types.
  - Hide clutter: exclude `node_modules`, `dist`, `.next`, `__pycache__` from the file explorer.
  - Set search exclusions to skip build artifacts and dependencies.
  - Enable bracket pair colorization and guides.
  - Configure TypeScript SDK to use the workspace version.

**Step 3: Recommend Extensions**
- Create `.vscode/extensions.json` with recommended extensions:
  - **Universal**: ESLint, Prettier, GitLens, Error Lens, GitHub Copilot.
  - **TypeScript/JavaScript**: Pretty TypeScript Errors, Import Cost, Auto Rename Tag.
  - **React**: ES7+ React snippets, Tailwind CSS IntelliSense.
  - **Vue**: Volar (Vue Language Features).
  - **Python**: Python, Pylance, Black Formatter.
  - **Go**: Go (official extension by Google).
  - **Docker**: Docker, Dev Containers.
  - **Database**: SQLTools with appropriate driver.
  - **Testing**: Vitest extension or Jest Runner.
- Include both the extension ID and a comment explaining why each is recommended.

**Step 4: Configure Debug Configurations**
- Create `.vscode/launch.json` with debug configs for:
  - **Server-side**: Attach to Node.js/Python debugger, set environment variables, specify entry point.
  - **Client-side**: Chrome/Edge debugger with source map support and URL.
  - **Full-stack**: Compound launch config that starts both server and client debuggers.
  - **Tests**: Debug individual test files with the testing framework.
  - **Scripts**: Debug build scripts and CLI tools.
- Set proper `sourceMapPathOverrides` for framework-specific debugging.
- Configure `skipFiles` to avoid stepping into node_modules.

**Step 5: Set Up Task Runners**
- Create `.vscode/tasks.json` with common development tasks:
  - `dev`: Start the development server.
  - `build`: Build for production.
  - `test`: Run the test suite.
  - `lint`: Run the linter.
  - `db:migrate`: Run database migrations.
  - `db:seed`: Seed the database.
  - `docker:up`: Start Docker Compose services.
- Use problem matchers to parse output and show errors in the Problems panel.
- Set the default build task for `Ctrl+Shift+B`.

**Step 6: Create Code Snippets**
- Create `.vscode/project.code-snippets` with project-specific snippets:
  - Component boilerplate: typed React/Vue/Svelte component template.
  - API route/endpoint template with error handling.
  - Test file template with describe/it blocks.
  - Custom hook/composable template.
  - Database model/schema template.
- Use tab stops (`$1`, `$2`) and placeholders (`${1:ComponentName}`) for quick editing.
- Name snippets with a project prefix for easy discovery (e.g., `proj-component`).

**Step 7: Configure Keybindings and Final Touches**
- Suggest useful keybindings in a `.vscode/keybindings.json` or document them:
  - Quick test runner: run current test file.
  - Toggle terminal: quick access to integrated terminal.
  - Navigate between related files (component, test, style).
- Create a multi-root workspace file (`.code-workspace`) for monorepo projects.
- Add workspace-level Git settings if needed (e.g., default branch name).
- Verify all configurations work by opening the project and testing each feature.
- Document the workspace setup in a brief section so new developers can get started quickly.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
