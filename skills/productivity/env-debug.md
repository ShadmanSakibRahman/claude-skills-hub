---
description: Debug environment and configuration issues including versions, PATH, env vars, database connections, and ports
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in debugging development environment and configuration issues. When asked to debug environment problems, follow these steps:

**Step 1: Gather System Information**
- Check the operating system and version.
- Check the shell being used (bash, zsh, PowerShell) and its configuration.
- Verify the PATH environment variable contains expected directories.
- Check available disk space and memory.
- Identify if running in a container, VM, or WSL environment.

**Step 2: Verify Runtime Versions**
- Check Node.js version (`node -v`) and compare with project requirements (`.nvmrc`, `engines` in `package.json`).
- Check npm/pnpm/yarn version and ensure compatibility.
- Check Python version (`python --version` or `python3 --version`) if applicable.
- Check Go version (`go version`), Ruby version (`ruby -v`), or other runtimes as needed.
- Verify version managers are configured correctly (nvm, pyenv, rbenv, asdf).
- If versions are wrong, provide commands to install or switch to the correct version.

**Step 3: Validate Environment Variables**
- Check if `.env` file exists and is properly formatted (no spaces around `=`, no trailing whitespace).
- Verify all required variables from `.env.example` are present in `.env`.
- Check for common issues: missing quotes around values with spaces, incorrect URL formats, expired API keys.
- Verify environment variables are actually loaded (print a safe subset to confirm).
- Check for variable naming conflicts between `.env.local`, `.env.development`, and `.env`.
- Ensure sensitive variables are not accidentally exposed to the client side.

**Step 4: Test Database Connections**
- Identify the database type and connection string from environment variables.
- Test the connection using the appropriate CLI tool:
  - PostgreSQL: `psql $DATABASE_URL -c "SELECT 1"`.
  - MySQL: `mysql -u $DB_USER -p$DB_PASSWORD -h $DB_HOST $DB_NAME -e "SELECT 1"`.
  - MongoDB: `mongosh $MONGODB_URI --eval "db.runCommand({ping: 1})"`.
  - Redis: `redis-cli -u $REDIS_URL ping`.
- Check if the database server is running and accepting connections.
- Verify the database exists and the user has proper permissions.
- Check if migrations are up to date by comparing schema state.

**Step 5: Check Port Availability**
- Identify the ports the application needs (typically 3000, 5432, 6379, etc.).
- Check if those ports are already in use: `lsof -i :PORT` or `netstat -tlnp | grep PORT`.
- If a port is occupied, identify the conflicting process and suggest killing it or using a different port.
- Check for firewall rules that might block connections.
- Verify that the application is binding to the correct host (0.0.0.0 vs 127.0.0.1 vs localhost).

**Step 6: Verify SSL and Network**
- Check if HTTPS certificates are valid and not expired (for local dev: mkcert or self-signed).
- Test external API connectivity: can the machine reach required external services?
- Check DNS resolution for any custom domains or service hostnames.
- Verify proxy settings if behind a corporate proxy (HTTP_PROXY, HTTPS_PROXY, NO_PROXY).
- Test webhook endpoints are reachable (ngrok, localtunnel for local development).

**Step 7: Dependency and Build Issues**
- Clear and reinstall node_modules: delete `node_modules` and lock file, run fresh install.
- Check for native module compilation issues (node-gyp, Python, build tools).
- Verify peer dependency compatibility.
- Clear build caches: `.next`, `.nuxt`, `dist`, `.cache`, `__pycache__`.
- Check for file permission issues on generated directories.
- Provide a summary of all issues found and their resolutions.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
