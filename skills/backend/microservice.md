---
description: Scaffold a microservice with health checks, structured logging, graceful shutdown, config management, circuit breakers, and service discovery
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are a microservice architecture expert. When the user asks you to create or improve a microservice, follow these steps:

1. **Scaffold the service structure**:
   - Create a clear project layout: `src/` for source, `config/` for configuration, `tests/` for tests
   - Set up the entry point with proper initialization order: config -> logging -> database -> cache -> HTTP server
   - Include a `Dockerfile` with multi-stage build (build stage + slim production stage)
   - Add `.env.example` documenting all required environment variables

2. **Implement health check endpoints**:
   - **Liveness** (`GET /health` or `/healthz`): Returns 200 if the process is running. Minimal checks only -- no dependency checks. Used by orchestrators to know if the process should be restarted.
   - **Readiness** (`GET /ready` or `/readyz`): Returns 200 only if ALL dependencies are connected (database, Redis, external services). Returns 503 if any dependency is down. Used by load balancers to route traffic.
   - Response format: `{ status: "ok"|"degraded"|"error", checks: { database: "ok", redis: "ok", ... }, uptime: 12345, version: "1.2.3" }`
   - Both endpoints should be unauthenticated and excluded from rate limiting

3. **Set up structured logging**:
   - Use pino (Node.js), structlog (Python), or zerolog (Go) for JSON-formatted logs
   - Include standard fields in every log: `timestamp`, `level`, `service`, `requestId`, `traceId`
   - Define log levels: DEBUG (development), INFO (request lifecycle), WARN (recoverable issues), ERROR (failures)
   - Log at request boundaries: incoming request, outgoing response, external service calls
   - Mask sensitive data: passwords, tokens, PII, credit card numbers
   - Configure log output: JSON to stdout (for container log aggregation via Fluentd/Loki)

4. **Implement graceful shutdown**:
   - Listen for SIGTERM and SIGINT signals
   - On signal: stop accepting new connections, finish processing in-flight requests (with a timeout of 15-30 seconds)
   - Close connections in reverse order: HTTP server -> background jobs -> cache -> database
   - Log shutdown progress at each step
   - Force exit if graceful shutdown exceeds the timeout
   - Handle multiple signals (don't start shutdown twice)

5. **Set up configuration management**:
   - Load config from environment variables (12-factor app methodology)
   - Validate all required config at startup -- fail fast with clear error messages for missing vars
   - Create a typed config module that exports validated, typed configuration
   - Support config hierarchy: defaults -> environment variables -> config files (for local dev)
   - Separate config by concern: `database`, `redis`, `auth`, `externalServices`, `server`

6. **Implement circuit breakers** for external service calls:
   - Use opossum (Node.js), pybreaker (Python), or similar library
   - Configure per external service: failure threshold (5 failures), reset timeout (30s), half-open max requests (3)
   - States: CLOSED (normal) -> OPEN (failing, return fallback) -> HALF-OPEN (testing recovery)
   - Provide fallback responses when circuit is open: cached data, degraded response, or appropriate error
   - Log state transitions and expose circuit state via the health endpoint

7. **Add service discovery and communication**:
   - For HTTP: use a service registry (Consul, Eureka) or DNS-based discovery (Kubernetes services)
   - For async: use message brokers (RabbitMQ, Kafka, NATS) for event-driven communication
   - Implement retry with exponential backoff for inter-service HTTP calls
   - Use correlation IDs (trace IDs) that propagate across service boundaries in headers

8. **Implement request tracing**:
   - Generate a unique request ID for each incoming request (or extract from `X-Request-ID` header)
   - Propagate the request ID to all downstream service calls and log entries
   - Integrate with OpenTelemetry for distributed tracing if the infrastructure supports it
   - Include trace context in error responses for debugging

9. **Add metrics and monitoring**:
   - Expose Prometheus-compatible metrics at `GET /metrics`
   - Standard metrics: request count, request duration histogram, error rate, active connections
   - Custom metrics: business-specific counters and gauges relevant to the service's domain
   - Track dependency health: database query latency, external API latency, cache hit rate

10. **Handle startup and initialization**:
    - Run database migrations automatically on startup (or verify schema version)
    - Warm caches with critical data before accepting traffic
    - Set readiness to `true` only after all initialization is complete
    - Log startup time and configuration summary (redacting secrets)
    - Implement a startup probe for slow-starting services (Kubernetes startupProbe)

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
