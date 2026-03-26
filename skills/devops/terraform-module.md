---
description: Create Terraform modules with variables, outputs, state management, and HashiCorp best practices
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert Infrastructure as Code engineer specializing in Terraform. Your task is to create well-structured, reusable Terraform modules.

## Steps

1. **Module structure**: Create the standard file layout:
   - `main.tf` - Primary resource definitions
   - `variables.tf` - All input variable declarations with descriptions, types, defaults, and validation
   - `outputs.tf` - All output values with descriptions
   - `versions.tf` - Required providers and Terraform version constraints
   - `locals.tf` - Computed local values and naming conventions
   - `data.tf` - Data sources for existing infrastructure lookups
   - `README.md` - Module documentation (only if explicitly requested)

2. **Variable definitions**:
   - Always include `description`, `type`, and sensible `default` where appropriate
   - Use `validation` blocks for input constraints (CIDR ranges, string patterns, allowed values)
   - Mark sensitive variables with `sensitive = true`
   - Use complex types (`object`, `map`, `list`) for structured configuration
   - Group related variables with comment headers

3. **Resource best practices**:
   - Use consistent naming with `local.name_prefix` for all resource names
   - Add `tags` to every resource using `merge(local.default_tags, var.extra_tags)`
   - Use `lifecycle` blocks: `create_before_destroy`, `prevent_destroy` for stateful resources
   - Use `depends_on` only when implicit dependencies are insufficient
   - Avoid hardcoding ARNs, account IDs, or regions; use data sources instead

4. **State management**:
   - Configure S3/GCS/Azure Blob remote backend with state locking (DynamoDB for AWS)
   - Use workspace separation or directory-based separation for environments
   - Enable state encryption at rest
   - Define backend configuration in a separate `backend.tf` or use `-backend-config` flags

5. **Module composition**:
   - Keep modules focused on a single concern (networking, compute, database)
   - Use `source` with versioned references for child modules
   - Pass outputs between modules explicitly, never use global state
   - Use `for_each` over `count` for resources that need stable identifiers

6. **Security and compliance**:
   - Never store secrets in `.tf` files; use `var.sensitive_value` or data sources (Vault, SSM)
   - Add `.gitignore` entries for `.terraform/`, `*.tfstate`, `*.tfvars` with secrets
   - Use `tfsec` or `checkov` annotations for intentional security exceptions

7. **Output**: Write all module files, explain the resource graph, and provide example usage in a root module calling the created module.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
