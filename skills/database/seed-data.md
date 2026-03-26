---
description: Generate realistic seed data with proper relationships, fake data factories, and deterministic seeding for dev/test environments
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in test data generation. Create realistic, relationship-aware seed data for development and testing environments.

Follow these steps precisely:

1. **Analyze the Schema**: Read the database schema, ORM models, or migration files to understand:
   - All tables/collections and their columns with data types.
   - Primary keys, foreign keys, and relationship cardinalities.
   - Required fields, unique constraints, and validation rules.
   - Enum values and allowed ranges.

2. **Design Factory Functions**: For each entity, create a factory that:
   - Uses a faker library appropriate to the project language (Faker.js, Faker for Python, Bogus for C#, etc.).
   - Generates realistic data matching the column type and semantic meaning (e.g., `faker.email()` for email columns, not random strings).
   - Respects unique constraints by using sequences or unique generators.
   - Supports trait/state variations (e.g., `createUser({role: 'admin'})`, `createOrder({status: 'shipped'})`).
   - Allows overriding any field for specific test scenarios.

3. **Handle Relationships**: Build data respecting foreign key dependencies:
   - Create parent records before children (users before orders, categories before products).
   - Use a dependency graph to determine insertion order.
   - Support creating complete object graphs (a user with orders, each with line items).
   - Handle many-to-many via junction tables with realistic associations.

4. **Ensure Deterministic Seeding**:
   - Set a fixed seed value for the random generator so runs are reproducible.
   - Document the seed value and how to change it.
   - Ensure the same seed always produces identical data.

5. **Create the Seed Script**: Write a runnable seed file that:
   - Clears existing data (with foreign key awareness, using TRUNCATE CASCADE or delete in reverse dependency order).
   - Inserts data in batches for performance (not one row at a time).
   - Reports progress (e.g., "Seeding 1000 users... done").
   - Handles errors gracefully with clear messages.
   - Can be run idempotently or with a fresh-start flag.

6. **Define Data Volumes**: Create tiered seeding:
   - **Minimal**: Just enough for basic development (5-10 records per table).
   - **Standard**: Realistic development set (50-200 records per table).
   - **Load Test**: Large dataset for performance testing (10,000+ records).

7. **Include Edge Cases**: Seed data should cover:
   - Null values in nullable fields, empty strings, maximum-length strings.
   - Boundary dates (past, future, timezone edge cases).
   - Special characters in text fields (unicode, emoji, HTML entities).
   - Records in every possible status/state.

Use the project's existing seeding conventions if present. Match the language and framework of the project.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
