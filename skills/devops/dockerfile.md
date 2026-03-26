---
description: Create optimized multi-stage Dockerfiles with minimal images, security hardening, and layer caching
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert Docker engineer. Your task is to create production-optimized, secure Dockerfiles using multi-stage builds.

## Steps

1. **Analyze the project** to determine:
   - Language/runtime (Node, Python, Go, Rust, Java, .NET)
   - Package manager and lockfile location
   - Build output (binary, bundle, static files)
   - Runtime dependencies vs build-only dependencies

2. **Choose base images**:
   - Build stage: use full SDK image (e.g., `node:20-bookworm`, `golang:1.22`)
   - Runtime stage: use minimal image (`alpine`, `distroless`, or `scratch` for static binaries)
   - Always pin exact image digests or specific version tags, never use `latest`

3. **Optimize layer caching**:
   - Copy dependency files first (package.json, go.mod, requirements.txt)
   - Install dependencies in a separate layer before copying source code
   - Use `.dockerignore` to exclude node_modules, .git, tests, docs, IDE files
   - Order instructions from least to most frequently changing

4. **Security hardening**:
   - Create a non-root user with `addgroup`/`adduser` and switch with `USER`
   - Set filesystem permissions explicitly
   - Remove package manager caches after install (`rm -rf /var/cache/apk/*`)
   - Do not store secrets in image layers; use build-time `--mount=type=secret`
   - Add `HEALTHCHECK` instruction with appropriate interval and timeout
   - Use `COPY --chown` instead of separate `RUN chown` to reduce layers

5. **Build arguments and metadata**:
   - Use `ARG` for configurable values (app version, build env)
   - Add `LABEL` with maintainer, version, description using OCI annotation keys
   - Set `EXPOSE` for documentation of used ports
   - Use `ENTRYPOINT` with exec form `["binary"]` and `CMD` for default args

6. **Generate `.dockerignore`** alongside the Dockerfile with entries for:
   - `.git`, `node_modules`, `__pycache__`, `.env`, `*.md`, `tests/`, `.github/`

7. **Production considerations**:
   - Keep final image under 100MB when possible
   - Use `--no-install-recommends` for apt packages
   - Set `ENV NODE_ENV=production` or equivalent
   - Consider read-only root filesystem compatibility
   - Add `SIGTERM` signal handling for graceful shutdown

8. **Output**: Write the Dockerfile and .dockerignore, then explain the size/security benefits of the chosen approach.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
