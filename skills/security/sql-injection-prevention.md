---
description: Audit and prevent SQL injection with parameterized queries, ORM usage, input validation, and WAF rules
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert database security engineer. Your task is to audit the codebase for SQL injection vulnerabilities and implement comprehensive prevention measures.

## Steps

1. **Audit for SQL injection vulnerabilities**: Search the entire codebase for dangerous patterns:
   - String concatenation in SQL: `"SELECT * FROM users WHERE id = " + id`
   - Template literals in SQL: `` `SELECT * FROM ${table} WHERE name = '${name}'` ``
   - String formatting in SQL: `f"SELECT * FROM users WHERE name = '{name}'"` (Python)
   - `fmt.Sprintf("SELECT * FROM users WHERE id = %s", id)` (Go)
   - Any `query()`, `execute()`, `raw()` calls with non-parameterized strings
   - Dynamic table/column names from user input
   - `ORDER BY` and `LIMIT` clauses with user-controlled values

2. **Fix with parameterized queries** (language-specific):
   - **Node.js (pg)**: `client.query('SELECT * FROM users WHERE id = $1', [id])`
   - **Node.js (mysql2)**: `connection.execute('SELECT * FROM users WHERE id = ?', [id])`
   - **Python (psycopg2)**: `cursor.execute('SELECT * FROM users WHERE id = %s', (id,))`
   - **Python (SQLAlchemy)**: `session.execute(text('SELECT * FROM users WHERE id = :id'), {'id': id})`
   - **Go (database/sql)**: `db.Query("SELECT * FROM users WHERE id = $1", id)`
   - **Java (JDBC)**: `PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE id = ?"); ps.setInt(1, id);`
   - **C# (ADO.NET)**: Use `SqlParameter` with `SqlCommand`

3. **ORM best practices**:
   - Prefer ORM query builders over raw SQL (Sequelize, SQLAlchemy, GORM, Hibernate, Entity Framework)
   - When raw SQL is unavoidable, always use the ORM's parameterized raw query method
   - Avoid `sequelize.literal()`, `RawSQL()`, or equivalent without sanitized input
   - Review custom query scopes and model hooks for injection points
   - Use ORM's built-in escaping for LIKE patterns: escape `%` and `_` in search terms

4. **Handle dynamic query elements safely**:
   - **Column names**: Validate against an allowlist of actual column names, never interpolate directly
   - **Table names**: Use an enum or constant map, never accept from user input
   - **ORDER BY**: Map user input to predefined options: `{name: 'users.name', date: 'users.created_at'}`
   - **LIMIT/OFFSET**: Parse as integer, enforce maximum values
   - **IN clauses**: Generate correct number of placeholders: `WHERE id IN ($1, $2, $3)` with array spread
   - **Search/LIKE**: Parameterize the pattern: `WHERE name LIKE $1` with `'%' + sanitized + '%'` as param value

5. **Stored procedures and views**:
   - Use stored procedures for complex operations to add a security layer
   - Even with stored procedures, parameterize inputs (stored procedures are not inherently safe from injection)
   - Use database views to restrict visible columns and rows
   - Avoid `EXECUTE IMMEDIATE` or dynamic SQL inside stored procedures with user input

6. **Database-level hardening**:
   - Apply principle of least privilege: app DB user should only have SELECT/INSERT/UPDATE/DELETE on needed tables
   - Remove DROP, CREATE, ALTER, GRANT permissions from application user
   - Disable `xp_cmdshell`, `LOAD_FILE()`, `INTO OUTFILE` and other dangerous functions
   - Enable query logging to detect and alert on suspicious patterns
   - Set statement timeout to prevent DoS via slow queries

7. **WAF rules** (Web Application Firewall):
   - Deploy ModSecurity or cloud WAF (AWS WAF, Cloudflare) with SQL injection rule sets
   - Enable OWASP Core Rule Set (CRS) SQL injection detection
   - Configure in detection mode first, review logs, then switch to blocking
   - Add custom rules for application-specific patterns
   - WAF is defense-in-depth, never a substitute for parameterized queries

8. **Output**: Report all found vulnerabilities with file and line references, provide fixed code for each instance, add integration tests that attempt SQL injection payloads, and verify all fixes use proper parameterization.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
