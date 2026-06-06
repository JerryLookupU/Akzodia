---
name: 22-event-sourcing
description: Use when designing or repairing an auto-orchestrator that needs an append-only durable event history, replayable agent/task state, audit trails, temporal debugging, projections/read models, optimistic concurrency on per-entity streams, snapshots, idempotent event handlers, schema evolution, or isolation of external side effects during replay.
---

# Event Sourcing

## When To Use

Use this skill when orchestration state must be explainable, replayable, and reconstructable from a durable sequence of facts rather than only stored as the latest mutable row or object.

Strong triggers:
- The orchestrator must answer "what happened, in what order, and why" for agents, tasks, approvals, tool calls, budget decisions, or recovery actions.
- A workflow needs deterministic replay for debugging, incident reconstruction, parallel testing, state rebuilds, or retroactive correction.
- Current task state, dashboards, queues, or agent memories can be derived from a history of commands accepted and events emitted.
- Multiple workers may append changes to the same job, session, resource, or aggregate, and conflicts must be detected without coarse database locks.
- Read models need to be rebuilt, changed, or specialized without changing the write-side execution history.
- Tool calls, notifications, payments, tickets, or other external side effects must not repeat during replay.
- The system needs append-only auditability, compensating events, snapshots, idempotent consumers, or event schema versioning.

Do not use this skill just because the system publishes messages. An event broker is not automatically an event store. Use event sourcing when the event stream is the authoritative state record or when replay and reconstruction are first-class requirements.

## Workflow

1. Decide whether event sourcing is justified.
   - Name the orchestration boundary: job, run, session, aggregate, resource ledger, agent memory, approval case, or domain entity.
   - State the return: audit, replay, temporal query, debugging, conflict reduction, scalable projections, or retroactive repair.
   - Reject event sourcing for simple CRUD, static reference data, short-lived prototypes, or workflows that require immediate strongly consistent query views and do not need history.
   - Apply it selectively. A payment ledger, task execution history, or approval pipeline may be event-sourced while user profiles and configuration remain CRUD.

2. Define the stream model and event contract.
   - Give each entity or orchestration aggregate its own ordered stream, such as `run:{runId}`, `task:{taskId}`, `resource:{name}`, or `approval:{caseId}`.
   - Design events as business or orchestration facts in past tense: `TaskClaimed`, `ToolCallStarted`, `ToolCallCompleted`, `ApprovalGranted`, `BudgetReserved`, `RunCanceled`.
   - Capture intent and cause, not only resulting state. Include command id, correlation id, causation id, actor, timestamp, version, sequence number, and enough payload to replay without hidden mutable context.
   - Keep events immutable after append. Correct mistakes with compensating events, upcasters, or explicit repair streams; do not silently rewrite history unless auditability is intentionally abandoned.

3. Separate commands from events.
   - Treat a command as a request that can be rejected: `StartTask`, `ReserveBudget`, `InvokeTool`, `CancelRun`.
   - Rehydrate the target aggregate from its stream or latest snapshot plus later events.
   - Run business/orchestration rules against the rehydrated state.
   - Append one or more resulting events only if invariants hold. Include the expected stream version so concurrent appends can be rejected and retried after rehydration.
   - Test write logic with `given past events -> when command -> expect new events or rejection`.

4. Build projections for reads.
   - Derive current state, dashboards, search indexes, queues, and UI read models by consuming event streams.
   - Make every projection handler idempotent. Track the last processed stream position or event id per projection and skip duplicates.
   - Design for eventual consistency. Define what users, agents, and schedulers see while projections lag behind the event store.
   - Rebuild projections from the event store when schemas, views, or query needs change.

5. Plan replay and snapshots.
   - Use full replay when streams are short or when exact reconstruction matters more than speed.
   - Add snapshots when rehydration cost becomes material. A snapshot is a cache of derived state, not the source of truth.
   - Record snapshot stream position, schema version, and aggregate type. Rehydrate by loading the latest valid snapshot and replaying later events.
   - Include replay modes: normal live processing, projection rebuild, temporal debugging, incident reproduction, and dry-run migration.

6. Isolate external interactions.
   - Route all external updates and queries through gateways controlled by the orchestrator.
   - Disable or simulate outbound side effects during replay unless the replay is explicitly intended to emit corrective actions.
   - Persist responses from external queries that affect event processing, or convert those responses into events, so replay uses the historical answer rather than a fresh value.
   - For at-least-once event delivery, make side-effect handlers idempotent with event ids, request ids, dedupe keys, or external idempotency keys.

7. Design evolution and correction paths.
   - Prefer additive event changes with tolerant deserialization.
   - Include event version metadata and use upcasters to transform old event shapes at read time.
   - Use compensating events for reversals, cancellations, corrections, and business-visible undo.
   - For historical bugs, decide whether to reprocess with fixed code, add compensating events, preserve old behavior for specific periods, or create a migration projection.
   - Keep personal data out of immutable events when deletion may be required. Store references to erasable records, or use encryption keys that can be destroyed.

8. Produce the orchestration artifact.
   - Output stream definitions, event schemas, command handlers, invariants, expected-version rules, and append failure behavior.
   - Output projection definitions with lag handling, idempotency keys, rebuild procedure, and duplicate-event tests.
   - Output replay rules that distinguish live execution from rebuild, temporal query, migration, and incident reproduction.
   - Output side-effect gateway rules, including what is suppressed, logged, replayed, compensated, or deduplicated.
   - Output schema evolution and correction policies before implementation begins.

## Failure Modes

- Treating a message broker topic as the system of record. Brokers distribute events; they often do not provide per-entity stream reads, expected-version appends, snapshots, or durable audit semantics.
- Recording state deltas without intent, such as `status changed to X`, when later audit or projection work needs to know the business reason.
- Letting handlers mutate current-state tables directly without a replayable event stream, then calling the resulting logs "event sourcing."
- Replaying events while external notifications, payments, tickets, emails, or tool calls fire again.
- Assuming event order from wall-clock timestamps alone. Per-stream sequence and optimistic concurrency are needed for correctness.
- Forgetting duplicate delivery. Projection drift and repeated side effects usually come from non-idempotent consumers.
- Building every read by replaying from the beginning. Use projections and snapshots when streams grow.
- Updating old events in place to solve schema problems, destroying audit value and making replay behavior unknowable.
- Hiding personal data in immutable events without a deletion or crypto-shredding strategy.
- Applying event sourcing everywhere. The pattern adds schema, replay, projection, consistency, testing, and operational complexity.

## Boundaries

Event sourcing is a persistence and reconstruction pattern, not a complete orchestration architecture. It pairs well with CQRS, workflow engines, actor systems, queues, idempotent receivers, compensating transactions, and observability, but it does not replace them.

Use this skill for durable histories and replayable state. Use transaction-processing patterns when the main risk is atomic commit. Use idempotency patterns when the main problem is duplicate command or message handling. Use process-mining or observability skills when the history already exists and the task is analysis rather than designing the event record.

The event store should be authoritative only for the boundary that needs replay and audit. Derived projections, caches, snapshots, and dashboards may be deleted and rebuilt; the stream history should not be casually changed.

Event sourcing deliberately accepts eventual consistency in read models and higher design complexity. If users or downstream agents cannot tolerate projection lag, or if the domain has no meaningful event history, choose a simpler state model.
