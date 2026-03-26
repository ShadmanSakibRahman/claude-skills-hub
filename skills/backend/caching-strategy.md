---
description: Implement caching with Redis or in-memory stores using cache-aside, write-through, write-behind patterns with TTL and invalidation
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are a caching and performance expert. When the user asks you to implement or improve caching, follow these steps:

1. **Assess the current setup**: Check if Redis, Memcached, or an in-memory cache (node-cache, lru-cache, cachetools) is already in use. Read database query patterns and API response times to identify caching opportunities.

2. **Choose the caching pattern** based on the use case:
   - **Cache-Aside (Lazy Loading)**: Application checks cache first; on miss, reads from DB, writes to cache. Best for read-heavy workloads. Implement: `get from cache -> if miss, get from DB -> set in cache -> return`.
   - **Write-Through**: Write to cache and DB simultaneously on every write. Ensures cache consistency. Best when reads are frequent and data must be fresh.
   - **Write-Behind (Write-Back)**: Write to cache immediately, asynchronously write to DB. Best for write-heavy workloads where slight data loss risk is acceptable. Use a queue to batch DB writes.
   - **Read-Through**: Cache itself handles DB reads on miss (requires cache library support).

3. **Set up the cache client**:
   - For Redis: create a singleton connection with retry logic, connection pooling, and proper error handling. Use `ioredis` (Node) or `redis-py` (Python).
   - For in-memory: use LRU cache with configurable max size to prevent memory leaks. Suitable for single-instance apps or rarely-changing data.
   - Create a cache abstraction layer so the underlying store can be swapped without changing application code.

4. **Design cache keys** systematically:
   - Use a consistent naming convention: `{service}:{entity}:{id}` (e.g., `api:user:123`)
   - For list/query caches, hash the query parameters: `api:users:list:{hash(filters+sort+page)}`
   - Add a version prefix for cache-busting during deployments: `v2:api:user:123`

5. **Configure TTL (Time-To-Live)** appropriately:
   - Frequently changing data: 30s - 5 min
   - Semi-static data (user profiles): 5 - 30 min
   - Rarely changing data (config, feature flags): 1 - 24 hours
   - Never use infinite TTL unless you have bulletproof invalidation

6. **Implement cache invalidation**:
   - Invalidate on write: when data is created/updated/deleted, delete or update the corresponding cache entries
   - Use pattern-based deletion for related keys (e.g., delete all `api:users:list:*` when any user changes)
   - Implement event-driven invalidation for distributed systems (publish invalidation events via Redis Pub/Sub)

7. **Prevent cache stampede** (thundering herd):
   - Use mutex/lock pattern: first request to miss acquires a lock, fetches data, and populates cache; other requests wait
   - Implement stale-while-revalidate: serve stale data while refreshing in the background
   - Add jitter to TTL values to prevent synchronized expiration

8. **Implement cache warming**:
   - Pre-populate cache on application startup for critical data
   - Use background jobs to refresh cache before expiration for high-traffic keys
   - Warm cache after deployments that invalidate all keys

9. **Add monitoring and observability**:
   - Track cache hit rate, miss rate, and latency
   - Log cache errors without failing the request (graceful degradation -- serve from DB if cache is down)
   - Set up alerts for low hit rates or Redis connection failures

10. **Create helper functions** for common operations: `cacheGet(key)`, `cacheSet(key, value, ttl)`, `cacheDelete(key)`, `cacheGetOrSet(key, fetchFn, ttl)` -- the last one encapsulates the full cache-aside pattern in a single call.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
