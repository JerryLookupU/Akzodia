---
name: 26-distributed-systems
description: Use when designing, reviewing, or debugging an auto-orchestrator that spans multiple workers, services, queues, tools, model providers, stores, regions, or tenants. Trigger for decisions about distributed boundaries, state ownership, replicated state, coordination, consistency, messaging, retries, idempotency, clocks, partial failure, failover, recovery, placement, and topology changes in orchestrator runtimes.
source_files:
  - references/source-notes.md
---
# 26 Distributed Systems

## Book-Derived Essence

- Core framework: Nodes, messages, clocks, replication, partitioning, consistency, coordination, and partial failure.
- Deep idea: The central lesson is that failure is normal and knowledge is local. Design must specify what each node can know and do when communication is delayed or broken.
- Discovery method: Map state ownership, message paths, clock assumptions, consistency needs, partition behavior, retry semantics, and recovery ownership.
- Boundary: Do not treat distributed work as a bigger single process; locality and partial failure change the problem.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an auto-orchestrator is no longer a single-process control loop:

- Runs are executed by multiple workers, agents, services, queues, sandboxes, or regions.
- State is split across planners, executors, tool gateways, model calls, event logs, caches, databases, or replay stores.
- The design must tolerate partial failure, latency variance, duplicate messages, stale reads, rate limits, partitions, worker death, or rolling deploys.
- You need to choose consistency, coordination, ownership, routing, sharding, replication, failover, or recovery rules.
- A feature seems correct locally but becomes ambiguous when steps can run concurrently or be retried on different nodes.

Do not trigger for general distributed-systems summaries, cloud vendor selection, or a single-process task runner unless the task crosses durable state, queues, remote dependencies, external side effects, or future multi-worker behavior.

## Standalone Contract

This skill must be executable from this file alone. Do not load or depend on external files, webpages, original books, source reports, external source folders, or source-pack material at runtime. `references/source-notes.md` is optional local provenance only and is not required for normal use.

The expected result is a distributed architecture decision: unit identities, process/data/trust boundaries, state ownership, coordination choices, communication semantics, failure responses, consistency rules, scaling/placement plan, and verification drills.

## Activation And Execution Gate

Activate only when all of these are true:
- The orchestrator spans or is being prepared to span multiple workers, services, stores, queues, regions, tenants, tools, or providers.
- Correctness depends on behavior across boundaries, not only local code structure.
- The user needs a design, review, or debug answer about ownership, consistency, messaging, partial failure, recovery, placement, or coordination.

Before proposing architecture, identify:
- Durable IDs for run, step, attempt, message, tool call, artifact, and tenant/API-user context.
- The authoritative writer for each mutable state item or the conflict-resolution rule.
- Which operations need strong coordination and which can be eventually consistent.

If these are unknown, ask for them or state assumptions before continuing.

## Workflow

1. Define the distributed unit of work.
   - Name the durable identity for each orchestrated run, step, tool call, message, artifact, and tenant/API-user context.
   - Decide which state is authoritative, which state is cached, and which state is only telemetry.
   - Make every external side effect traceable to a stable idempotency key or event id.

2. Draw process, data, and trust boundaries.
   - List each participant: intake API, scheduler, planner, worker, tool gateway, sandbox, model provider, queue, database, object store, notifier, and human handoff path.
   - Mark which participants can call each other synchronously, which communicate by message, and which only observe state.
   - Keep security and tenant isolation boundaries visible; distributed convenience must not erase isolation rules.

3. Assign state ownership before adding replicas.
   - For every mutable record, choose one writer or define the conflict-resolution rule.
   - Prefer append-only event logs for run history and recovery evidence; derive views for dashboards, queues, and UI state.
   - Treat caches, read models, and worker-local memory as disposable unless the design explicitly persists and reconciles them.

4. Choose coordination only where correctness requires it.
   - Use leases, locks, leader election, consensus-backed records, or compare-and-swap only for exclusive decisions such as claiming a step, committing final status, allocating scarce budget, or issuing a non-idempotent side effect.
   - Avoid global coordination for ordinary progress reporting, speculative planning, cache warming, low-value metrics, or recomputable outputs.
   - Include timeout, renewal, fencing token, and stale-owner behavior for every lease-like mechanism.

5. Make communication semantics explicit.
   - Specify delivery expectation: at-most-once, at-least-once, effectively-once through idempotency, or exactly-once only if the stack genuinely provides it end to end.
   - Define message ordering requirements per run, per step, and per tenant. Do not assume a global order.
   - Add deduplication, replay, poison-message handling, backpressure, and dead-letter policy where messages drive execution.

6. Design for partial failure instead of total failure.
   - Enumerate failures by boundary: worker crash, queue delay, database failover, model outage, tool timeout, sandbox leak prevention, network partition, rate-limit exhaustion, and deploy mismatch.
   - For each failure, choose retry, compensation, fallback, skip, pause, human handoff, or fail-fast behavior.
   - Bound retries with budgets and jitter; ensure recovery does not multiply cost or repeat unsafe side effects.

7. Set consistency according to user-visible risk.
   - Strongly coordinate safety, billing, budget, ownership claims, final run status, and non-repeatable external actions.
   - Allow eventual consistency for dashboards, search indexes, progress summaries, derived analytics, and non-critical recommendations.
   - Show stale or pending status honestly when reads may lag writes.

8. Make time and ordering robust.
   - Use monotonic clocks for durations and deadlines; avoid wall-clock assumptions for causal order.
   - Persist causal links between events: parent run, step id, attempt id, message id, tool call id, and predecessor ids.
   - Treat timeouts as failure detectors, not proof that remote work stopped.

9. Plan scaling and placement deliberately.
   - Decide partition keys: tenant, run id, workflow type, tool class, region, priority, or resource profile.
   - Keep hot partitions, noisy tenants, and slow tools from starving unrelated work.
   - Separate control-plane capacity from execution capacity when orchestration decisions must remain available during worker saturation.

10. Verify with failure drills.
   - Test duplicate delivery, lost acknowledgements, delayed messages, stale leases, worker death mid-step, database failover, provider timeout, and replay from the event log.
   - Check invariants after every drill: one final status, no unauthorized cross-tenant read, no budget overspend, no repeated non-idempotent action, and recoverable run history.
   - Capture the resulting assumptions in runbooks, diagrams, tests, and telemetry.

## Output Format

Return:
- `scope`: participants, boundaries, and distributed unit of work.
- `state`: authoritative records, caches, telemetry, ownership, and idempotency keys.
- `coordination`: leases, locks, CAS, leader/consensus use, fencing, and timeout behavior.
- `messaging`: delivery, ordering, dedupe, replay, poison handling, backpressure, and DLQ policy.
- `failure_model`: boundary-specific failures and selected retry, compensation, fallback, pause, or fail-fast behavior.
- `consistency`: strong vs eventual consistency decisions and user-visible stale-read rules.
- `scale_and_placement`: partition keys, hot-spot controls, tenant isolation, and capacity separation.
- `verification`: failure drills, invariants, telemetry, and unresolved tradeoffs.

## Failure, Recovery, And Idempotency

If design facts are missing, preserve momentum by listing explicit assumptions and marking which decisions cannot be finalized. If a proposed mechanism fails an invariant, revise the ownership, commit, or coordination boundary before adding retries.

Repeated reviews should be idempotent: keep stable IDs and decision names, append new tradeoffs instead of renaming old ones, and preserve prior failure assumptions unless they are explicitly retired.

## Failure Modes

- Treating a distributed orchestrator as a local call graph, then discovering that retries, queues, and deploys reorder reality.
- Storing authoritative run state in worker memory or caches that disappear during crash, scale-down, or rebalance.
- Assuming exactly-once execution without end-to-end idempotency, deduplication, and durable commit boundaries.
- Letting multiple services write the same mutable record without a single owner or conflict-resolution rule.
- Using locks or leaders without fencing tokens, expiry behavior, or stale-owner protection.
- Retrying tool calls or external actions without budget limits, compensation rules, or non-repeatable side-effect guards.
- Hiding eventual consistency from users, operators, or downstream components that make strong-consistency assumptions.
- Designing one global queue or partition key that allows a slow tool, region, or tenant to block unrelated runs.
- Treating timeout as cancellation proof when the remote operation may still commit later.

## Boundaries

- This skill designs distributed-system behavior for auto-orchestrator runtimes; it is not a general textbook summary or a vendor-specific cloud architecture guide.
- Use a reliability/SRE skill when the main task is SLOs, alerting, or incident process rather than distributed correctness.
- Use a transaction-processing, event-sourcing, actor-model, workflow, or queueing skill when that narrower mechanism is the dominant design question.
- Do not introduce distribution for its own sake. A single-process or single-writer design is often the better answer until scale, isolation, availability, or fault tolerance requires distribution.
- Optional provenance and source trace live in `references/source-notes.md`; do not load it for routine execution.

## Hard Rules

- Do not assume exactly-once behavior without end-to-end idempotency, deduplication, and durable commit boundaries.
- Do not let more than one service write the same mutable state without a named owner or conflict rule.
- Do not use leases or locks without expiry, renewal, fencing token, and stale-owner behavior.
- Do not hide eventual consistency where downstream agents or users need authoritative state.

## Source Closure

This 26-distributed-systems skill is self-contained for runtime use; its source basis is Distributed systems sources and local distributed-systems entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
