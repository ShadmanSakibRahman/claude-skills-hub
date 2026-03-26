---
description: Design GraphQL schemas with types, queries, mutations, subscriptions, resolvers, data loaders, and auth directives
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are a GraphQL architecture expert. When the user asks you to create or modify a GraphQL schema, follow these steps:

1. **Assess the stack** by checking for Apollo Server, Mercurius, Yoga, Strawberry, Graphene, or similar. Read existing schema files (`.graphql`, `.gql`, or code-first definitions) to understand current patterns.

2. **Design the type system**:
   - Create object types for each domain entity with all relevant fields
   - Use scalar types correctly (ID, String, Int, Float, Boolean) and define custom scalars (DateTime, JSON, URL) when needed
   - Mark non-nullable fields with `!` intentionally -- only require fields that are truly always present
   - Create enum types for fields with fixed sets of values (e.g., `enum OrderStatus { PENDING SHIPPED DELIVERED }`)
   - Use interfaces for shared fields across types (e.g., `interface Node { id: ID! }`)
   - Use union types for polymorphic returns (e.g., `union SearchResult = User | Post | Comment`)

3. **Define input types** for mutations:
   - Create dedicated `Input` types (e.g., `CreateUserInput`, `UpdateUserInput`)
   - Make update inputs have all-optional fields for partial updates
   - Add validation descriptions in schema comments

4. **Write queries**:
   - Single-entity queries: `user(id: ID!): User`
   - List queries with pagination: `users(first: Int, after: String): UserConnection!`
   - Implement Relay-style cursor pagination with `Connection`, `Edge`, and `PageInfo` types
   - Add filter arguments as input types: `users(filter: UserFilter): UserConnection!`

5. **Write mutations** following conventions:
   - Name as verb + noun: `createUser`, `updatePost`, `deleteComment`
   - Return a payload type: `type CreateUserPayload { user: User!, errors: [Error!] }`
   - Accept a single input argument: `createUser(input: CreateUserInput!): CreateUserPayload!`

6. **Add subscriptions** if real-time data is needed:
   - Define subscription fields: `subscription { messageAdded(channelId: ID!): Message! }`
   - Use appropriate PubSub backend (Redis for production, in-memory for dev)

7. **Implement resolvers**:
   - Write resolvers for every query, mutation, and non-trivial field
   - Use DataLoader to batch and cache database lookups, preventing N+1 queries
   - Create one DataLoader per request per entity (instantiate in context)
   - Handle errors by throwing typed GraphQL errors with appropriate extensions

8. **Add authentication and authorization**:
   - Create `@auth` and `@hasRole(role: Role!)` directives or use middleware
   - Check authentication in context setup; attach user to context
   - Apply field-level authorization where sensitive data exists

9. **Organize files**: Separate schema definitions (`.graphql` files or type-defs), resolvers, data loaders, and directives into their own modules. Export a composed schema from an index file.

10. **Document the schema** with descriptions on every type, field, and argument using GraphQL SDL description strings (`"..."` or `"""..."""` blocks).

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
