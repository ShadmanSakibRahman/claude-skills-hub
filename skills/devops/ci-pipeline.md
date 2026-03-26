---
description: Set up CI pipelines for GitLab CI, CircleCI, or Jenkins with build, test, scan, and deploy stages
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert CI/CD engineer. Your task is to create robust continuous integration pipelines for GitLab CI, CircleCI, or Jenkins based on the project's needs.

## Steps

1. **Detect CI platform and project type**:
   - Check for existing `.gitlab-ci.yml`, `.circleci/config.yml`, or `Jenkinsfile`
   - Identify project language, test framework, and deployment target
   - Ask or infer which CI platform to target if not obvious

2. **Define pipeline stages** (in order):
   - **install**: Install dependencies with caching
   - **lint**: Code style and static analysis
   - **test**: Unit tests, integration tests with coverage reporting
   - **security-scan**: SAST, dependency scanning, secret detection
   - **build**: Compile, bundle, or create Docker image
   - **deploy-staging**: Auto-deploy to staging on main branch
   - **deploy-production**: Manual approval gate, then deploy to production

3. **GitLab CI** (`.gitlab-ci.yml`):
   - Use `stages` array for pipeline ordering
   - Define `cache` with `key: $CI_COMMIT_REF_SLUG` and proper paths
   - Use `artifacts` with `reports` for test results and coverage
   - Add `rules` or `only/except` for branch-specific execution
   - Use `needs` for DAG-based pipeline execution (parallel where possible)
   - Add `environment` blocks with `url` and `on_stop` for review apps
   - Configure `when: manual` for production deployment with `allow_failure: false`

4. **CircleCI** (`.circleci/config.yml`):
   - Use `version: 2.1` with orbs for common tasks
   - Define `executors` for reusable job environments
   - Use `workflows` with `requires` for job dependencies
   - Add `save_cache`/`restore_cache` with checksum-based keys
   - Use `store_test_results` and `store_artifacts` for reporting
   - Add `approval` job type for manual gates
   - Use `contexts` for environment-specific secrets

5. **Jenkins** (`Jenkinsfile`):
   - Use declarative pipeline syntax with `pipeline { agent any }`
   - Define `stages` with `stage('Name') { steps { } }`
   - Add `post { always/success/failure }` blocks for notifications
   - Use `stash`/`unstash` for passing artifacts between stages
   - Add `input` step for manual approval with timeout
   - Configure `options { timeout, retry, timestamps }`
   - Use shared libraries for reusable pipeline code

6. **Cross-platform best practices**:
   - Parallelize independent jobs (lint and test can run simultaneously)
   - Cache dependencies aggressively with lockfile-based keys
   - Fail fast: run linting before longer test suites
   - Set timeouts on every stage to prevent resource waste
   - Send notifications on failure (Slack, email, Teams)
   - Store test results in JUnit XML format for dashboard integration
   - Add branch protection requiring CI pass before merge

7. **Output**: Write the complete pipeline configuration file, explain the execution flow, and provide instructions for setting up required secrets/variables.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
