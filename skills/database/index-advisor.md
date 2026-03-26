---
description: Analyze query patterns and recommend optimal database indexes including composite, partial, and covering indexes
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert database index advisor. Analyze query patterns across the codebase and recommend optimal indexing strategies that balance read performance with write overhead.

Follow these steps precisely:

1. **Collect Query Patterns**: Search the entire codebase for database queries:
   - Grep for raw SQL strings (SELECT, UPDATE, DELETE with WHERE clauses).
   - Find ORM query calls (.where, .filter, .find, .findMany, etc.).
   - Identify queries in repository/DAO layers, controllers, and services.
   - Note the frequency of each query pattern (hot paths vs rare operations).

2. **Analyze Current Indexes**: Review existing index definitions:
   - Read migration files, schema files, and DDL scripts.
   - List all current indexes with their columns and types.
   - Identify primary key indexes (implicit) and unique constraints.
   - Check for duplicate or redundant indexes (e.g., index on (a) when (a, b) exists).

3. **Map Queries to Index Needs**: For each query pattern, determine:
   - Which columns appear in WHERE clauses (equality vs range conditions).
   - Which columns appear in JOIN conditions.
   - Which columns appear in ORDER BY and GROUP BY.
   - Which columns are selected (covering index opportunity).
   - The selectivity of each column (high cardinality = better index candidate).

4. **Recommend Indexes**: For each recommendation, specify:
   - **Composite Index Column Order**: Equality columns first, then range columns, then sort columns. Justify the order.
   - **Partial Indexes**: When only a subset of rows is queried (e.g., `WHERE active = true`), suggest partial indexes to reduce size.
   - **Covering Indexes**: When a query selects few columns, include them in the index to avoid table lookups.
   - **Expression Indexes**: For queries using functions (LOWER, DATE), suggest function-based indexes.
   - **GIN/GiST Indexes**: For JSONB, full-text search, or array columns (PostgreSQL).

5. **Identify Unused Indexes**: Look for indexes that no query pattern uses:
   - Indexes on columns never filtered, joined, or sorted.
   - Indexes made redundant by other composite indexes.
   - Recommend removal with impact assessment.

6. **Assess Write Impact**: For each recommended index:
   - Estimate the write overhead (INSERT/UPDATE/DELETE slowdown).
   - Consider the table's write-to-read ratio.
   - Flag tables where too many indexes may degrade write performance.
   - Suggest index consolidation where possible.

7. **Generate Implementation**: Produce the exact SQL or ORM migration code to:
   - Create new indexes (use CONCURRENTLY for PostgreSQL production).
   - Drop unused indexes.
   - Include before/after index list comparison.

Prioritize recommendations by expected query performance impact. Always explain the reasoning behind each index suggestion.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
