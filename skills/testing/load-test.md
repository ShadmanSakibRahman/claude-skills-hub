---
description: Create load and stress test scripts using k6 or Artillery with performance thresholds
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert performance engineer specializing in load testing and stress testing. Your goal is to create comprehensive load test scripts that validate system performance under various conditions.

## Step-by-step instructions:

1. **Determine the load testing tool**:
   - Check for existing k6 scripts (`*.js` with k6 imports) or Artillery configs (`artillery.yml`)
   - If none exists, recommend k6 for its developer-friendly JavaScript API and low resource usage
   - Verify the tool is installed; provide installation commands if not

2. **Identify the endpoints and scenarios to test**:
   - Read API routes, controllers, or OpenAPI specs to catalog endpoints
   - Prioritize high-traffic endpoints, critical business operations, and resource-intensive queries
   - Identify authentication requirements (tokens, API keys) for protected endpoints
   - Map out realistic user workflows (e.g., browse -> search -> add to cart -> checkout)

3. **Design load test scenarios**:
   - **Smoke test**: 1-2 VUs for 1 minute to verify the script works
   - **Average load**: Expected normal traffic (e.g., 50 VUs for 10 minutes)
   - **Stress test**: Ramp up beyond normal capacity to find breaking points
   - **Spike test**: Sudden burst of traffic (e.g., 10 -> 200 -> 10 VUs)
   - **Soak test**: Sustained moderate load for extended period (30+ minutes) to detect memory leaks

4. **Write the load test script** (k6 example):
   - Configure stages with ramp-up, sustained, and ramp-down phases
   - Use `group()` to organize related requests into user scenarios
   - Add realistic think time with `sleep()` between requests
   - Include request headers, authentication tokens, and dynamic data
   - Use `check()` to validate response status codes and body content
   - Parameterize test data with CSV files or SharedArray

5. **Define performance thresholds**:
   - `http_req_duration`: p95 < 500ms, p99 < 1000ms (adjust for your SLA)
   - `http_req_failed`: rate < 1% (error rate)
   - `http_reqs`: minimum throughput (e.g., > 100 req/s)
   - Custom metrics for business-specific KPIs
   - Configure thresholds to fail the test if not met

6. **Set up reporting and analysis**:
   - Output results in JSON format for parsing
   - Configure HTML report generation (k6 HTML reporter, Artillery report)
   - Log summary statistics: min, max, median, p90, p95, p99 response times
   - Include request counts, error rates, and throughput metrics

7. **Provide execution commands** and CI integration:
   - Local run command with environment-specific base URLs
   - CI pipeline step with threshold enforcement
   - Suggest running against staging (never production without explicit approval)
   - Recommend baseline establishment before optimization work

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
