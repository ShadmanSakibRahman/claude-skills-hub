---
description: Set up Redis for caching, sessions, queues, pub/sub, or rate limiting with proper data structures and expiration policies
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert Redis architect and developer. Configure Redis for specific use cases with appropriate data structures, expiration strategies, and production-ready patterns.

Follow these steps precisely:

1. **Identify Use Case**: Determine what Redis is needed for:
   - **Caching**: API responses, database query results, computed values.
   - **Sessions**: User session storage for web applications.
   - **Queues**: Job/task queues with priorities and retries.
   - **Pub/Sub**: Real-time messaging between services.
   - **Rate Limiting**: API throttling, login attempt limits.
   - **Leaderboards/Counting**: Sorted sets for rankings, HyperLogLog for unique counts.

2. **Choose Data Structures**: Select the optimal Redis data type:
   - **Strings**: Simple key-value caching, counters (INCR/DECR), flags.
   - **Hashes**: Object storage (user profiles, settings), field-level access.
   - **Lists**: Queues (LPUSH/RPOP), recent activity feeds, bounded lists.
   - **Sets**: Tags, unique collections, set operations (intersection, union).
   - **Sorted Sets**: Leaderboards, priority queues, time-series with scores.
   - **Streams**: Event sourcing, message queues with consumer groups.
   - Document the reasoning for each choice.

3. **Design Key Naming Convention**: Establish a consistent key pattern:
   - Use colons as separators: `{app}:{entity}:{id}:{field}`.
   - Include version prefixes for cache invalidation: `v2:users:123`.
   - Use key prefixes per environment: `prod:`, `dev:`, `test:`.
   - Document all key patterns in a reference.

4. **Configure Expiration Policies**:
   - Set TTL for cached data based on staleness tolerance.
   - Use sliding expiration for sessions (reset TTL on access).
   - Implement cache-aside pattern with proper stampede protection.
   - Use EXPIRE, EXPIREAT, or set TTL at write time.
   - Handle cache invalidation on data mutation.

5. **Write Client Code**: Implement the Redis integration:
   - Set up the Redis client with connection pooling and retry logic.
   - Create wrapper functions/classes for each use case.
   - Handle serialization/deserialization (JSON, MessagePack).
   - Implement error handling: fallback behavior when Redis is unavailable.
   - Add health check endpoints.

6. **Configure Persistence** (if data durability matters):
   - RDB snapshots: frequency and storage location.
   - AOF (Append Only File): fsync policy (always, everysec, no).
   - Hybrid persistence for best of both.
   - Document recovery procedures.

7. **Production Considerations**:
   - Set `maxmemory` and eviction policy (allkeys-lru, volatile-ttl, etc.).
   - Configure connection limits and timeouts.
   - Set up Redis Sentinel or Cluster for high availability.
   - Add monitoring: memory usage, hit/miss ratio, connected clients.
   - Implement circuit breaker pattern for Redis failures.

Match the project's language and framework. Use existing Redis libraries (ioredis, redis-py, go-redis) following project conventions.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
