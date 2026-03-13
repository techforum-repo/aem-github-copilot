---
description: Create or update an OSGi Scheduler or Sling Job following AEMaaCS conventions
---

Create or update an OSGi Scheduler or Sling Job following the conventions already used in this repository.

Requirements:
- prefer `Runnable` with `@Component` and `SchedulerOptions` injection via `Scheduler` OSGi service for simple periodic tasks
- prefer `JobConsumer` with `JobManager` for reliable, distributed, or retryable background work in AEMaaCS
- never use `Thread.sleep()` inside scheduler or job execution (CQBP-75 — blocks Sling thread pool)
- never use admin `ResourceResolver` — use a service user if JCR access is needed (CQBP-72)
- make the schedule configurable via OSGi config (cron expression or period) — do not hardcode timing
- handle exceptions explicitly — an uncaught exception in a scheduler silently stops future executions
- use SLF4J parameterized logging only (CQBP-84)
- keep execution logic focused; delegate heavy logic to OSGi services
- suggest unit tests for the execution logic (not the scheduling itself)

Before generating code:
1. confirm whether a `Runnable` scheduler or `JobConsumer` is more appropriate and why
2. identify OSGi services and service user needs
3. state the expected schedule or trigger type
4. mention likely SonarCloud or Cloud Manager risks
5. note any AEMaaCS-specific constraints (e.g., leader-only execution on author)
