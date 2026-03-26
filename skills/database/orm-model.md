---
description: Create ORM models for Prisma, Sequelize, TypeORM, SQLAlchemy, or Django with relationships, validations, and hooks
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in ORM design and implementation. Create well-structured ORM models that leverage framework features for type safety, validation, and query efficiency.

Follow these steps precisely:

1. **Detect the ORM Framework**: Scan the project for:
   - `prisma/schema.prisma` (Prisma) - look for existing model patterns.
   - `sequelize` in package.json (Sequelize) - check for model definition style (class-based or define).
   - `typeorm` in package.json (TypeORM) - check for decorator style (Active Record vs Data Mapper).
   - `sqlalchemy` in requirements (SQLAlchemy) - check for declarative vs classical mapping.
   - `django` in requirements (Django ORM) - check for app structure and model conventions.

2. **Define the Model Structure**:
   - Map each database column to the appropriate ORM field type.
   - Set primary keys (auto-increment, UUID, or composite).
   - Define nullable/required fields matching the schema constraints.
   - Add default values, including dynamic defaults (timestamps, UUIDs).
   - Include column-level comments and table-level documentation.

3. **Configure Relationships**:
   - **One-to-One**: Define on both sides with proper back-references.
   - **One-to-Many**: Parent has collection, child has foreign key reference.
   - **Many-to-Many**: Use junction/through tables with optional extra columns.
   - **Self-Referencing**: Tree structures, parent-child within same table.
   - Set cascade options (delete, update) matching business requirements.
   - Configure eager vs lazy loading defaults.

4. **Add Validations**:
   - Field-level: length, format (email, URL), range, enum membership.
   - Model-level: cross-field validations, conditional requirements.
   - Custom validators with clear error messages.
   - Unique constraints (single and composite).

5. **Implement Hooks/Signals**:
   - Before create: hash passwords, generate slugs, set defaults.
   - Before update: update timestamps, validate state transitions.
   - After create/update: trigger notifications, update caches.
   - Before delete: check dependencies, soft-delete logic.

6. **Define Scopes and Query Helpers**:
   - Named scopes for common filters (active, recent, by-status).
   - Default scope (e.g., exclude soft-deleted records).
   - Custom query methods for complex domain-specific queries.
   - Pagination helpers.

7. **Add Indexes**: Define indexes in the model:
   - Single-column indexes for frequently queried fields.
   - Composite indexes for multi-column lookups.
   - Unique indexes for business-rule uniqueness.
   - Full-text indexes for search fields where supported.

8. **Type Safety**: Ensure the model provides:
   - TypeScript interfaces/types for the model (if applicable).
   - Proper typing for relationship accessors.
   - Typed query results.

Follow existing project conventions for file location, naming, and export style. Include necessary imports.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
