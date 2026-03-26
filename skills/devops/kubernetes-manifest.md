---
description: Generate Kubernetes manifests with Deployments, Services, Ingress, autoscaling, and resource limits
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert Kubernetes engineer. Your task is to generate production-grade K8s manifests following best practices.

## Steps

1. **Gather requirements**: Determine the application name, container image, port, replicas, environment variables, and resource needs from the project context.

2. **Create Deployment manifest**:
   - Set `apiVersion: apps/v1` with proper `metadata.labels` and `selector.matchLabels`
   - Configure `strategy.rollingUpdate` with `maxSurge: 1` and `maxUnavailable: 0` for zero-downtime deploys
   - Define `containers` with `resources.requests` and `resources.limits` for CPU and memory
   - Add `livenessProbe` and `readinessProbe` with appropriate HTTP/TCP/exec checks
   - Set `securityContext`: `runAsNonRoot: true`, `readOnlyRootFilesystem: true`, `allowPrivilegeEscalation: false`
   - Add `topologySpreadConstraints` or `affinity` for high availability across nodes

3. **Create Service manifest**:
   - Use `ClusterIP` for internal services, `LoadBalancer` for external-facing services
   - Match selector labels to Deployment pod labels exactly
   - Define named ports for clarity

4. **Create Ingress manifest**:
   - Configure `ingressClassName` (nginx, traefik, or cloud-specific)
   - Add TLS section referencing a `kubernetes.io/tls` Secret
   - Set `annotations` for rate limiting, CORS, and SSL redirect
   - Define host-based and path-based routing rules

5. **Create supporting resources**:
   - **ConfigMap**: For non-sensitive configuration, mounted as env vars or volume
   - **Secret**: For sensitive data (use `stringData` for readability, note it encodes to base64)
   - **HorizontalPodAutoscaler**: Target CPU 70%, memory 80%, with min/max replicas
   - **PodDisruptionBudget**: Set `minAvailable` or `maxUnavailable` to ensure availability during node drains

6. **Best practices**:
   - Use namespaces to isolate environments
   - Add `app.kubernetes.io/*` standard labels (name, version, component, part-of)
   - Set `imagePullPolicy: IfNotPresent` for tagged images, `Always` for latest
   - Use `terminationGracePeriodSeconds` aligned with app shutdown time
   - Add `preStop` lifecycle hook for graceful connection draining

7. **Output**: Write each manifest as a separate YAML file or a single multi-document YAML separated by `---`. Validate all label selectors match and resource names are consistent.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
