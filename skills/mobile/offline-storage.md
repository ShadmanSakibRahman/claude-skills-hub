---
description: Implement offline-first data storage with sync strategies, conflict resolution, and optimistic UI updates
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in offline-first mobile architecture. When implementing offline storage and sync, follow these steps:

1. **Choose the storage solution** based on the project's framework and data complexity:
   - **React Native**: `@react-native-async-storage/async-storage` for simple key-value data. `react-native-sqlite-storage` or `expo-sqlite` for relational data. WatermelonDB for large datasets needing performance.
   - **Flutter**: `hive` or `hive_flutter` for fast key-value/object storage. `isar` for complex queries and full-text search. `sqflite` for traditional SQL.

2. **Design the local data schema**:
   - Mirror the server-side models but add offline metadata fields: `localId`, `syncStatus` (synced/pending/conflict), `lastModified`, `isDeleted` (soft delete).
   - Create a pending operations queue table/box to track create/update/delete operations.
   - Index fields that you query or sort by frequently.

3. **Implement the data access layer**:
   - Create repository classes that abstract storage details from the rest of the app.
   - Expose methods like `getAll()`, `getById()`, `save()`, `delete()` that work with local storage first.
   - Return local data immediately, then sync in the background.
   - Use streams or reactive queries (WatermelonDB/Isar) to auto-update UI when data changes.

4. **Build the sync engine**:
   - Track a `lastSyncTimestamp` per entity type to request only changed records from the server.
   - On sync: pull server changes first, then push local pending operations.
   - Batch API calls to reduce network overhead — send multiple operations in one request.
   - Implement exponential backoff for failed sync attempts.
   - Listen for connectivity changes (`NetInfo` in RN, `connectivity_plus` in Flutter) to trigger sync when back online.

5. **Handle conflict resolution**:
   - **Last-write-wins**: Compare `lastModified` timestamps — simplest but may lose data.
   - **Server-wins**: Always accept server version — safe but may frustrate users.
   - **Client-wins**: Always accept local version — risky for shared data.
   - **Manual merge**: Flag conflicts and present both versions to the user for resolution.
   - Choose a strategy per entity type based on business requirements. Document the choice.

6. **Implement optimistic UI updates**:
   - Apply changes to local storage and update UI immediately, before the network request.
   - Show a subtle sync indicator (not a blocking spinner) while syncing.
   - If the server rejects the change, revert the local state and show an error message.
   - Queue the operation for retry if the failure is due to network issues.

7. **Handle edge cases**:
   - Large datasets: paginate local queries and use lazy loading.
   - Storage limits: implement a cache eviction policy (LRU) for non-critical data.
   - App killed during sync: resume from the pending operations queue on next launch.
   - Schema migrations: version your local database and write migration scripts.
   - Encryption: use `react-native-keychain` or `flutter_secure_storage` for sensitive data.

8. **Test the offline flow**:
   - Test with airplane mode on: create, update, delete records, then reconnect and verify sync.
   - Simulate slow networks and mid-request failures.
   - Test conflict scenarios with two devices modifying the same record.

Ensure the sync mechanism is idempotent — running it multiple times produces the same result.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
