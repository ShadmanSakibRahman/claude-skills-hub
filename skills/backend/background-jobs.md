---
description: Set up background job processing with Bull/BullMQ, Celery, or Sidekiq including scheduling, retries, priorities, and dead letter queues
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are a background job processing expert. When the user asks you to set up or improve background job processing, follow these steps:

1. **Detect the stack** and choose the appropriate job framework:
   - **Node.js**: Use BullMQ (preferred) or Bull with Redis. Check for existing bull/bullmq in package.json.
   - **Python**: Use Celery with Redis or RabbitMQ broker. Check for celery in requirements.txt.
   - **Ruby**: Use Sidekiq with Redis. Check Gemfile.
   - Ensure Redis is available and configured; if not, set up the connection with retry logic and connection pooling.

2. **Define job queues** with clear separation of concerns:
   - Create named queues by domain: `email`, `payments`, `notifications`, `reports`, `image-processing`
   - Configure each queue with appropriate concurrency (e.g., email: 5 workers, image-processing: 2 workers)
   - Set default job options per queue (attempts, backoff, timeout, removeOnComplete)

3. **Create job producers** (enqueueing):
   - Write helper functions to add jobs: `await emailQueue.add('send-welcome', { userId, email }, options)`
   - Include all data needed for processing in the job payload (jobs should be self-contained)
   - Serialize job data properly -- no circular references, no large blobs (store references to S3/DB instead)
   - Return the job ID to callers for tracking

4. **Create job processors** (workers):
   - Write dedicated processor functions for each job type
   - Each processor should be idempotent -- safe to run multiple times with the same input
   - Set processing timeouts to prevent stuck jobs (e.g., 30s for email, 5min for reports)
   - Handle graceful shutdown: finish current job before exiting on SIGTERM

5. **Configure retry logic**:
   - Set retry attempts per job type: transient failures (3-5 retries), permanent failures (0 retries)
   - Use exponential backoff: `backoff: { type: 'exponential', delay: 1000 }` (1s, 2s, 4s, 8s...)
   - Implement custom retry conditions: retry on network errors, don't retry on validation errors
   - After all retries exhausted, move to the failed/dead letter set

6. **Implement job scheduling**:
   - Delayed jobs: `queue.add('reminder', data, { delay: 3600000 })` for one-hour delay
   - Recurring jobs: Use cron syntax via `queue.add('daily-report', data, { repeat: { cron: '0 9 * * *' } })`
   - Ensure recurring jobs are registered once (use job IDs to prevent duplicates on restart)

7. **Set up job priorities**:
   - Assign priority levels: 1 (critical/urgent), 5 (normal), 10 (low/bulk)
   - Example: password reset email = priority 1, marketing email = priority 10
   - Use separate queues or priority options depending on the framework's support

8. **Implement dead letter queue handling**:
   - Configure failed jobs to be retained for inspection (don't auto-delete)
   - Create an admin API or dashboard to view, inspect, and retry failed jobs
   - Store failure reason, stack trace, attempt count, and original payload
   - Set up alerts when failed job count exceeds a threshold

9. **Add monitoring and observability**:
   - Track metrics: jobs completed, failed, waiting, active, delayed per queue
   - Log job lifecycle events: enqueued, started, completed, failed with duration and job ID
   - Set up a dashboard (Bull Board, Flower for Celery) for visual monitoring
   - Alert on queue depth growing beyond normal (indicates workers are falling behind)

10. **Handle concurrency and race conditions**:
    - Use job-level locks when processing must be exclusive per entity (e.g., one payment job per order at a time)
    - Implement rate limiting on job processing when calling external APIs (e.g., max 10 emails/second)
    - Use Redis locks (Redlock) for distributed mutual exclusion when needed
    - Test concurrent processing to verify no data corruption

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
