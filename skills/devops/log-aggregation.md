---
description: Set up centralized logging with ELK Stack or Loki+Grafana including structured logging and alerting
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert observability engineer specializing in log aggregation and analysis. Your task is to set up centralized logging infrastructure for production systems.

## Steps

1. **Choose the logging stack** based on requirements:
   - **ELK Stack** (Elasticsearch + Logstash + Kibana): Full-text search, complex queries, large-scale
   - **Loki + Grafana**: Lightweight, label-based, cost-effective, integrates with Prometheus
   - **EFK** (Elasticsearch + Fluentd + Kibana): Kubernetes-native alternative to ELK

2. **Structured logging in applications**:
   - Configure JSON-formatted log output with consistent fields: `timestamp`, `level`, `message`, `service`, `trace_id`, `request_id`
   - Use structured logging libraries: Winston (Node.js), structlog (Python), zap (Go), Serilog (.NET)
   - Include contextual fields: user_id, endpoint, duration_ms, status_code, error_stack
   - Set appropriate log levels: ERROR for failures, WARN for degradation, INFO for business events, DEBUG for development
   - Never log sensitive data (passwords, tokens, PII); redact or mask such fields

3. **ELK Stack setup**:
   - **Elasticsearch**: Configure cluster with dedicated master, data, and ingest nodes; set heap size to 50% of RAM (max 32GB); configure index lifecycle management (ILM) for rollover and retention
   - **Logstash**: Create pipeline configs with input (beats, syslog), filter (grok, mutate, date), and output (elasticsearch) sections; parse unstructured logs into fields
   - **Filebeat/Fluentbit**: Deploy as log shippers on each host or as DaemonSet in K8s; configure multiline log handling; add metadata (hostname, container, pod)
   - **Kibana**: Set up index patterns, saved searches, and dashboards

4. **Loki + Grafana setup**:
   - Deploy Loki with appropriate storage backend (filesystem for small, S3/GCS for production)
   - Configure Promtail or Grafana Agent as log collector
   - Design label strategy: keep cardinality low (service, environment, level only)
   - Use LogQL for querying: `{service="api"} |= "error" | json | duration > 1s`
   - Configure chunk and retention settings in `loki-config.yaml`

5. **Log rotation and retention**:
   - Set retention policies: 7 days hot, 30 days warm, 90 days cold storage
   - Configure index lifecycle management or compaction schedules
   - Set up log rotation on disk: `logrotate` with size-based and time-based rotation
   - Archive older logs to object storage for compliance

6. **Alerting on log patterns**:
   - Alert on error rate spikes: >10 errors/min for a service
   - Alert on specific patterns: "OutOfMemoryError", "Connection refused", "FATAL"
   - Alert on absence: no logs from a service for >5 minutes (service may be down)
   - Route alerts through Alertmanager or Grafana alerting to Slack/PagerDuty

7. **Output**: Write all configuration files (docker-compose for the stack, shipper configs, pipeline configs, dashboard definitions) and explain the data flow from application to dashboard.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
