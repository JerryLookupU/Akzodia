---
name: 29-checkpointing-and-rollback-recovery
description: Use when designing or reviewing auto-orchestrator recovery for long-running, stateful, or streaming runs that must resume after worker crashes, deploys, queue redelivery, tool timeouts, storage failures, or partial graph completion. Trigger for checkpoint interval, durable state snapshots, rollback point, replay source, exactly-once vs at-least-once recovery, final commit, retained checkpoints, and safe recovery of external side effects.
---

# Checkpointing and Rollback Recovery for Auto-Orchestrators

## When To Use

Use this skill when an orchestrator run needs a deliberate recovery contract:

- A planner, scheduler, worker, tool gateway, stream processor, or agent can fail mid-run and later resume.
- The run has state that cannot live only in process memory: plan graph, step cursor, budgets, tool outputs, artifacts, user/API context, leases, timers, or sink transactions.
- Recovery depends on replayable inputs, durable state storage, and a known rollback point.
- You need to choose checkpoint frequency, timeout, concurrency, retention, or storage for production workloads.
- Exactly-once behavior is promised, suspected, or required for external commits, billing, notifications, file writes, tickets, or user-visible state.
- Parts of the workflow can finish before the whole run, and finalization must still commit buffered outputs safely.

## Workflow

1. Define the recovery objective.
   - Name the unit that must recover: run, task graph, step, attempt, tenant session, stream job, or SQL statement.
   - State the recovery guarantee in plain terms: at-least-once replay, effectively-once through idempotency, or exactly-once only when source replay, state snapshot, and sink commit are coordinated end to end.
   - Decide the maximum acceptable lost progress, reprocessing window, recovery time, and duplicate side-effect risk.

2. Inventory checkpointed state.
   - List every stateful component: planner memory, DAG cursor, per-step status, queue offsets, timers, leases, budgets, tool-call results, artifact pointers, sink transactions, and human-handoff state.
   - Classify each item as authoritative checkpoint state, replayable input, derived cache, or external side effect.
   - Exclude disposable caches from the checkpoint, but make them rebuildable from the checkpoint plus replay source.

3. Verify prerequisites before enabling recovery.
   - Require a durable replay source for inputs or events, such as a persistent queue, log, database journal, or object store.
   - Require durable checkpoint storage reachable by all recovery workers, not a single coordinator heap or worker-local disk in production.
   - Check credentials, tenant isolation, encryption, retention, and access paths for every worker that may restore.

4. Choose the checkpoint boundary.
   - Capture enough information to restore state and input positions together: run id, step id, attempt id, event offset, source partition, artifact pointer, timer state, and pending transaction ids.
   - Put the boundary before irreversible external effects unless the effect is guarded by idempotency or a two-phase commit.
   - Treat the checkpoint as the rollback target: after failure, later in-memory progress is discarded or reconciled, not trusted.

5. Set checkpoint cadence and backpressure policy.
   - Shorter intervals reduce reprocessing and commit latency, but increase storage, CPU, network, and coordination overhead.
   - Add a timeout so a stuck checkpoint is aborted and surfaced instead of silently blocking recovery freshness.
   - Use a minimum pause between completed checkpoints when checkpointing starts consuming the capacity needed for useful work.
   - Keep concurrent checkpoints to one unless the workload has a clear reason and the recovery model can handle overlap.

6. Decide aligned, unaligned, and partial-graph behavior.
   - Use aligned checkpoints when normal flow is healthy and consistent barriers can progress without excessive delay.
   - Consider unaligned checkpoints under sustained backpressure when checkpoint barriers are delayed, accepting that in-flight buffers become part of recovery state.
   - For workflows with bounded branches or finished subtasks, define what final checkpoint proves: no buffered output remains, all commit pointers are durable, and finished branches do not lose shared offset state.

7. Protect external side effects.
   - For idempotent sinks, persist idempotency keys and completed effect ids in checkpointed or replayable state.
   - For non-idempotent sinks, require a commit protocol, pending transaction pointer, compensation path, or explicit human review before retry.
   - Delay final user-visible completion until the checkpoint containing required commit pointers has completed successfully.

8. Specify rollback and restore behavior.
   - On restart, restore from the latest valid checkpoint, reset input positions to the checkpointed offsets, rebuild derived views, and resume only uncommitted work.
   - If checkpoint restore fails, define whether to try an older retained checkpoint, pause for operator action, or fail the run.
   - Never assume a timeout cancelled remote work; reconcile by idempotency key, transaction id, or external status lookup.

9. Retain checkpoints deliberately.
   - Keep automatic internal checkpoints for normal failure recovery.
   - Retain externalized checkpoints when cancellation, migration, upgrade, or manual rollback may need a known restore point.
   - Separate planned-operation savepoints from automatic failure-recovery checkpoints when the platform provides both.

10. Test recovery as a first-class workflow.
   - Kill workers during checkpoint write, after source read, after tool call, before sink commit, and after final branch completion.
   - Inject slow storage, timed-out checkpoints, duplicate input delivery, stale leases, corrupted checkpoint metadata, and partial graph completion.
   - Verify invariants: one final status, no unauthorized tenant state, bounded replay, no budget overspend, no repeated unsafe side effect, and a clear operator trail.

## Failure Modes

- Enabling checkpoints without a replayable source, so restored state cannot be aligned with input position.
- Storing production checkpoints in coordinator memory, worker disk, or any location unavailable to recovery workers.
- Promising exactly-once behavior while external tools, APIs, notifications, or billing writes are retried without idempotency or commit pointers.
- Choosing very frequent checkpoints that keep the system busy checkpointing instead of making useful progress.
- Letting timed-out or failed checkpoints go unnoticed until the first real outage discovers there is no fresh recovery point.
- Running overlapping checkpoints or unaligned checkpoints without understanding extra state volume, barrier behavior, and restore semantics.
- Dropping state for finished branches before final commits, buffered outputs, offsets, or transaction pointers are durable.
- Treating checkpoint restore as cancellation proof for remote work that may still complete later.
- Retaining checkpoints forever without lifecycle, privacy, storage-cost, or tenant-isolation controls.

## Boundaries

- This skill designs checkpoint and rollback recovery behavior for auto-orchestrators; it is not a vendor-specific Flink tuning manual.
- Use an event-sourcing skill when the primary design question is append-only domain history rather than periodic state snapshots.
- Use an idempotency or transaction-processing skill when the main risk is a single non-repeatable external action.
- Use SRE or observability skills for alert thresholds, dashboards, incident process, and operational ownership after the recovery contract is designed.
- Do not add checkpointing to stateless, short-lived, easily restarted work unless replay cost, side effects, or user experience justify the added complexity.
- For source provenance and distilled rationale, read `references/source-notes.md`.
