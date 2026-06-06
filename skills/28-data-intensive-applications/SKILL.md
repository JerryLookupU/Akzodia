---
name: 28-data-intensive-applications
description: Use when designing, reviewing, or debugging the data architecture of an auto-orchestrator: durable run state, event logs, workflow history, queues, task indexes, caches, search/read models, analytics, replication, partitioning, schema evolution, transactions, stream processing, batch recovery, consistency, and data-system tradeoffs for reliable, scalable, maintainable orchestration.
source_files:
  - references/source-notes.md
---
# 28 Data-Intensive Applications

## Book-Derived Essence

- Core framework: Data model, storage, encoding, replication, partitioning, consistency, transactions, streams, and derived views.
- Deep idea: The most useful frame is “source of truth versus derived view.” Data architecture fails when rebuildable projections are treated as authority.
- Discovery method: Classify records as authoritative, event history, derived view, cache, blob, telemetry, or worker state; then trace invariants, replay, migration, and stale-read tolerance.
- Boundary: Do not choose databases by preference before access patterns, invariants, and evolution paths are known.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestrator's correctness depends on data behavior, not only control flow:

- Runs, steps, tool calls, artifacts, approvals, budgets, or API-user context need durable storage and replayable history.
- You must choose between event logs, relational records, document stores, queues, caches, object stores, indexes, warehouses, or streaming pipelines.
- Product requirements mention reliability, scalability, maintainability, auditability, recovery, multi-tenant isolation, or long-running workflows.
- The design needs replication, partitioning, schema migration, backfill, replay, deduplication, or derived read models.
- A failure could leave conflicting statuses, lost events, repeated external side effects, stale dashboards, or unrecoverable runs.

Do not trigger for general CAP/consensus lectures, frontend components, incident-response process, or a narrow infrastructure task that does not require data architecture tradeoffs.

## Standalone Contract

This skill must provide data-architecture guidance without requiring original source access. Do not load or depend on external files, webpages, original books, source reports, external source folders, or source-pack material at runtime. `references/source-notes.md` is optional local provenance only and is not required for execution.

The expected result is a data architecture decision: data roles, source of truth, reconstruction path, consistency choices, write/commit boundaries, storage model, partitioning/replication, schema evolution, processing model, observability, and failure tests.

## Activation And Execution Gate

Activate only when all of these are true:
- Orchestrator correctness, recovery, auditability, or scale depends on data storage or data movement.
- The task asks for design, review, or debugging of authoritative state, history, queues, caches, indexes, streams, transactions, schema evolution, or partitioning.
- The user needs tradeoffs tied to invariants, not just a vendor/tool recommendation.

Before choosing technologies, identify:
- Authoritative records, append-only events, derived views, caches, blobs, indexes, metrics, and temporary worker state.
- The reconstruction path for every derived view.
- Which invariants require strong consistency or transactional boundaries.

If these are missing, classify the data first and defer technology selection.

## Workflow

1. Classify the data by role before choosing technology.
   - Separate authoritative records, append-only events, derived views, caches, blobs, search indexes, metrics, and temporary worker state.
   - Name the durable identity for each run, step, attempt, tool call, message, artifact, budget decision, and tenant/API-user boundary.
   - Treat worker-local memory and caches as disposable unless explicitly persisted and reconciled.

2. Define the source of truth and reconstruction path.
   - Decide which store answers "what happened?" and which store answers "what is the current status?"
   - Prefer an append-only history for audit, replay, recovery, and process mining; derive current status and UI views from it when feasible.
   - Specify how to rebuild every derived view from authoritative data after data loss, deploy bugs, or schema changes.

3. Set consistency by invariant, not by preference.
   - Require strong consistency or transactional boundaries for final run status, step claims, budget spending, tenant isolation, authorization, and non-repeatable side effects.
   - Allow eventual consistency for dashboards, progress summaries, search, recommendations, analytics, and notifications that can tolerate lag.
   - Document stale-read behavior in the API/UI so downstream agents do not mistake lagging views for authoritative state.

4. Design write paths around idempotency and atomicity.
   - Give every retried command and external side effect an idempotency key tied to run id, step id, attempt id, and tool call id.
   - Commit state changes and emitted messages through a clear boundary such as a transaction, outbox, log append, or compare-and-swap.
   - Avoid dual writes without a repair path; if two systems must change, define ordering, retry, reconciliation, and compensating action.

5. Choose storage models from access patterns.
   - Use relational or transactional stores when invariants, joins, constraints, and concurrent status updates dominate.
   - Use logs or event streams when ordering, replay, audit, fan-out, and rebuildable projections dominate.
   - Use search/document/index stores for query flexibility, not as the only authority for workflow correctness.
   - Use object stores for large artifacts and persist checksums, ownership, lifecycle, and references in authoritative metadata.

6. Plan replication and partitioning explicitly.
   - Pick partition keys such as tenant, run id, workflow type, region, priority, or tool class based on fairness, locality, and blast radius.
   - Prevent a hot tenant, tool, or run family from starving unrelated work.
   - For replicated reads, decide which operations may read from followers and which must read the leader or quorum-backed state.

7. Make schema evolution and backfills routine.
   - Use additive migrations, versioned event schemas, tolerant readers, and explicit compatibility windows.
   - Design workers to handle old and new records during rolling deploys.
   - Backfill derived state from authoritative history with checkpoints, rate limits, validation queries, and rollback criteria.

8. Combine batch and stream processing for recovery.
   - Use streams for near-real-time progress, alerts, and derived projections.
   - Use batch jobs to recompute, verify, repair, compact, and audit state after bugs or outages.
   - Keep stream processors restartable with offsets/checkpoints and make reprocessing idempotent.

9. Define data observability and integrity checks.
   - Track lag, queue depth, dropped messages, duplicate suppression, projection freshness, reconciliation failures, migration progress, and storage error rates.
   - Add invariant checks: one final status per run, no cross-tenant reads, no orphaned artifacts, no budget overspend, no unclaimed executable step.
   - Keep enough event and mutation context to explain user-visible decisions after the fact.

10. Test data failure scenarios.
   - Exercise duplicate commands, lost acknowledgements, partial commits, stale replicas, delayed streams, projection rebuilds, schema mismatch, backfill interruption, and database failover.
   - Verify the same invariants after each drill: recoverable history, correct final status, bounded spend, tenant isolation, and no repeated non-idempotent side effects.
   - Record accepted tradeoffs so future agents know which staleness, loss, or latency risks are intentional.

## Output Format

Return:
- `data_roles`: authoritative records, events, views, caches, blobs, indexes, metrics, and disposable state.
- `source_of_truth`: current-status source, history source, and reconstruction process.
- `consistency`: invariant-by-invariant consistency choices and stale-read behavior.
- `write_path`: idempotency keys, atomic commit boundary, outbox/log/CAS/transaction use, and repair path.
- `storage_model`: selected stores tied to access patterns and rejected options.
- `replication_partitioning`: partition keys, read routing, hot-spot controls, and blast radius.
- `schema_processing`: migration, event versioning, backfill, stream/batch recovery, and rollback criteria.
- `observability_tests`: integrity checks, lag/freshness metrics, failure drills, and accepted tradeoffs.

## Failure, Recovery, And Idempotency

If data roles are unclear, stop and classify them before naming a database, queue, or stream. If a dual write is present, define a transaction, outbox, replay log, reconciliation job, or compensation path before accepting it.

Repeated reviews should be idempotent: preserve stable entity IDs, event names, schema versions, migration IDs, and backfill checkpoints so repair and audit trails remain comparable.

## Failure Modes

- Selecting a database or queue before classifying authoritative state, derived state, and disposable state.
- Treating a cache, search index, dashboard table, or worker memory as the source of truth for run correctness.
- Using eventual consistency for budget, authorization, final status, tenant isolation, or non-repeatable side effects.
- Writing to two systems without a transaction, outbox, replay log, reconciliation job, or compensating action.
- Assuming a stream processor will never replay, skip, reorder, or duplicate events.
- Designing partition keys that create hot tenants, hot workflow types, or global queues that block unrelated runs.
- Migrating schemas without tolerant readers, versioned events, or a rollback/backfill plan.
- Losing auditability by overwriting status records without retaining causality, attempts, tool calls, and emitted events.
- Letting derived read models drift without freshness metrics, rebuild procedures, or invariant checks.

## Boundaries

- This skill is for auto-orchestrator data architecture and data-system tradeoffs; it is not a generic summary of *Designing Data-Intensive Applications*.
- Use a distributed-systems skill when the central problem is process topology, clocks, consensus, or partial failure across nodes.
- Use event-sourcing, transaction-processing, queueing, monitoring, or checkpointing skills when the request is narrowly about one of those mechanisms.
- Do not overbuild a data platform when a single transactional store plus a small event log satisfies the invariants and scale.
- Optional provenance and source trace live in `references/source-notes.md`; do not load it for routine execution.

## Hard Rules

- Do not treat caches, search indexes, dashboards, or worker memory as the authority for workflow correctness.
- Do not use eventual consistency for budget, authorization, final status, tenant isolation, or non-repeatable side effects.
- Do not allow dual writes without a transaction, outbox, replay, reconciliation, or compensation plan.
- Do not migrate event or workflow schemas without tolerant readers, versioning, validation, and rollback/backfill criteria.

## Source Closure

This 28-data-intensive-applications skill is self-contained for runtime use; its source basis is Designing Data-Intensive Applications source notes and local data-systems entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
