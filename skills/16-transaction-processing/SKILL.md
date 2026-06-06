---
name: 16-transaction-processing
description: Use when designing or repairing an auto-orchestrator that must coordinate durable state changes, external side effects, message publication, idempotency, retries, crash recovery, compensation, isolation, exactly-once claims, transactional outbox/inbox patterns, or commit boundaries across agents, tools, queues, and databases.
---

# Transaction Processing

## When To Use

Use this skill when an orchestration design can be correct in the happy path but wrong after a crash, retry, duplicate callback, concurrent update, partial commit, or side effect that cannot be rolled back.

Strong triggers:
- A workflow updates durable state and also calls tools, sends messages, charges money, writes files, starts agents, or emits events.
- The design claims "exactly once" execution, but the runtime actually provides at-least-once delivery, retries, duplicate callbacks, or manual replay.
- Multiple agents or workers can race to claim, modify, approve, cancel, publish, or finalize the same case.
- A step needs a clear transaction boundary: what is read, what is written, what is locked, what is committed, and what is visible afterward.
- The orchestrator needs transactional outbox, inbox/deduplication, saga compensation, escrow/reservation, two-phase commit avoidance, or crash recovery rules.
- A bug appears as duplicate downstream work, lost events, stale reads, inconsistent status, leaked reservations, double billing, or a job stuck between "committed" and "published."

Prefer a plain workflow-pattern skill when the main issue is routing shape. Prefer a Petri-net skill when the main issue is token/resource reachability. Use this skill when the hard part is making state transitions and side effects survive concurrency, failure, and replay.

## Workflow

1. Define the transaction scope.
   - Name the business invariant that must survive failure: one owner per case, one final answer, no double charge, all committed work eventually published, every reservation released, or no lost approval.
   - Separate durable state changes from external side effects. Databases can roll back; email, webhooks, LLM calls, file writes, payments, and user-visible messages usually cannot.
   - Mark each operation as read, write, lock/reserve, publish, external call, compensation, or observation.
   - Choose the smallest transaction boundary that preserves the invariant. Do not wrap long-running agent or tool work in a database transaction.

2. Classify consistency requirements.
   - Use strong consistency for claim/finalize decisions, unique ownership, balances, quotas, irreversible effects, and security boundaries.
   - Use eventual consistency for notifications, search indexes, analytics, non-critical cache refresh, and derived summaries.
   - State isolation expectations: read committed, repeatable read, serializable, optimistic version checks, lease-based ownership, or single-writer partitioning.
   - For every relaxed guarantee, write the visible anomaly the system accepts and the repair path that resolves it.

3. Design the atomic state transition.
   - Represent every important case state explicitly: pending, claimed, running, awaiting callback, committed, publishing, published, compensating, failed, canceled.
   - Use compare-and-set, unique constraints, version columns, leases, or serializable transactions for competing workers.
   - Commit idempotency keys with the state transition, not after it. A retry must find the prior decision before it can repeat the effect.
   - Store enough evidence to resume after a crash: request id, actor, attempt number, input hash, output reference, next action, deadlines, and compensation status.
   - Treat "commit result and schedule next work" as one atomic design problem.

4. Handle messages and external side effects.
   - If state update and message publication must not diverge, use a transactional outbox: commit the business row and an outbox row in one local transaction, then publish outbox rows asynchronously.
   - Make the publisher idempotent. It may crash after sending but before marking the row as sent, so consumers must deduplicate.
   - Add an inbox or processed-message table for at-least-once deliveries. Deduplicate by stable message id plus consumer identity.
   - Avoid distributed two-phase commit unless the participating systems actually support it and the operational cost is justified.
   - For non-rollbackable actions, move the action after the durable decision and attach a compensation or reconciliation path.

5. Design retries, recovery, and compensation.
   - Define which failures are retryable, terminal, compensatable, or require human review.
   - Use bounded retries with durable attempt records, backoff, and a final escalation state.
   - Make every retry safe under duplicate execution: same idempotency key, same message id, same output path, same reservation id, or same external reference.
   - For sagas, list each forward step, its committed evidence, its compensating step, and the order in which compensation runs.
   - Prefer semantic compensation over pretending rollback is possible. A refund, cancel, release, tombstone, or correction event is not the same as erasing history.

6. Specify runtime observability and tests.
   - Expose transaction ids, idempotency keys, state versions, outbox ids, message ids, worker ids, lease expirations, and compensation ids in logs/traces.
   - Test crash points: before commit, after commit before publish, after publish before marking sent, after external effect before state update, after compensation, and during concurrent cancellation.
   - Test duplicate delivery, replay, stale worker completion, lease expiry, and two workers racing to claim the same case.
   - Return an executable contract: transaction boundary, state transition table, idempotency rules, outbox/inbox schema, compensation table, and recovery loop.

## Failure Modes

- Treating "exactly once" as a property of queues or workers. Most systems need at-least-once delivery plus idempotent consumers and deduplication.
- Updating state and publishing a message in separate non-atomic steps without an outbox. Crashes create lost events or phantom events.
- Holding a database transaction open while an agent, LLM call, webhook, human approval, or remote tool runs.
- Writing idempotency records after the external effect. A crash then makes the retry indistinguishable from a new request.
- Assuming rollback can undo an external side effect. Payments, emails, webhooks, and user-visible outputs need compensation or reconciliation.
- Using locks without expiry, fencing tokens, or ownership checks. Stale workers can finish after a newer owner has taken over.
- Hiding critical state in memory, logs, or queue visibility timeouts instead of durable records.
- Mixing business finality with transport acknowledgement. A message being acknowledged does not prove the business transaction was committed.
- Letting retries create new ids, output paths, or downstream messages. This converts recovery into duplication.
- Ignoring isolation anomalies: lost update, dirty read, write skew, stale approval, and double claim.

## Boundaries

Transaction processing is a correctness discipline for durable state and side effects. It does not decide the best product flow, agent role split, UI design, or business priority.

ACID transactions are strongest inside one transactional resource. Cross-service orchestration usually needs sagas, outbox/inbox, idempotency, reconciliation, and explicit compensation instead of assuming one global rollback.

Do not use this skill to force serial execution everywhere. Serializing all work may preserve consistency but can destroy throughput, availability, or latency. Choose strong boundaries only around invariants that need them.

This skill complements, but does not replace, workflow routing and resource modeling. Use workflow patterns to define branch/join semantics, Petri nets to reason about token reachability, and transaction processing to make each durable transition and side effect recoverable.
