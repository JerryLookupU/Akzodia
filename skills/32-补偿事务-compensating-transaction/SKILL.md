---
name: 32-补偿事务-compensating-transaction
description: Use when designing or reviewing long-running auto-orchestrator workflows, sagas, distributed business transactions, multi-service tool chains, or agent runs that need domain-specific compensation after partial success. Trigger for compensating transactions, saga orchestration, choreography, rollback alternatives, point of no return, pivot transaction, irreversible steps, cancellation, retry-before-compensate decisions, failed compensation recovery, or cross-service consistency without 2PC.
source_files:
  - references/source-notes.md
---
# 32 补偿事务 / Compensating Transaction

## Book-Derived Essence

- Core framework: Saga boundary, local transactions, compensable/pivot/retryable steps, orchestration/choreography, and semantic undo.
- Deep idea: Compensation is not inverse ACID rollback; it is domain repair that brings the business situation back to an acceptable state.
- Discovery method: Classify each step as compensable, pivot, retryable, or irreversible; record forward action, compensation, idempotency key, timeout, and manual review path.
- Boundary: Do not use compensation where stronger validation, reservation, or atomicity is required before an irreversible action.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when a workflow can partially succeed across services, tools, data stores, or human/business actions and a later failure must be handled explicitly:

- A run has multiple committed local steps and cannot rely on one database transaction to roll everything back.
- A task action needs a paired `compensate_action`, cancellation action, refund, release, revoke, delete, or state repair step.
- A workflow crosses owned boundaries: service databases, queues, SaaS APIs, payment systems, ticketing systems, deployment systems, file stores, or human approvals.
- The design needs to choose between retrying forward, taking an alternative path, pausing for review, or compensating completed work.
- A step is irreversible, legally binding, externally visible, expensive to undo, or only partially undoable.
- The orchestrator must recover when compensation itself fails, times out, duplicates, or resumes after crash.
- The team is debating choreography versus an explicit saga orchestrator for cross-service consistency.

## Do Not Trigger

- Do not use this skill for a single ACID transaction that can fully cover the effect boundary.
- Do not use it for duplicate-message suppression alone; use idempotent receiver guidance.
- Do not use it for stateless reads, pure computation, or workflows where retrying forward is always safe and sufficient.
- Do not use it as generic microservices advice unless the request needs compensation, cancellation, pivot, or saga recovery semantics.

## Standalone Contract

This skill is self-contained. Do not browse, open, or depend on external source files, source reports, original books, websites, or cross-skill distilled text during normal execution. `references/source-notes.md` is optional provenance only, not required runtime knowledge. A compliant answer must define the saga boundary, local transactions, step classification, compensation semantics, coordination style, retry/alternative/compensation policy, persisted saga state, idempotency rules, isolation controls, and unhappy-path tests.

## Activation and Execution Gate

Proceed only if all of these are true:

1. The request contains a multi-step workflow with at least one committed local effect before later failure is possible.
2. A single transaction cannot cover all relevant effects.
3. The user needs a valid final state after failure, cancellation, timeout, or partial success.

If any condition is false, state the mismatch and route to idempotency, transaction processing, or simpler retry/error-handling guidance.

## Workflow

1. Define the saga boundary and consistency promise.
   - Name the business operation, run, or workflow instance that needs eventual consistency.
   - List the participating services, tools, queues, data stores, artifacts, and humans.
   - State the acceptable final states: completed, rejected, compensated, partially compensated with manual review, canceled, or terminal failure.
   - Confirm why a single local transaction, strong distributed transaction, or simple retry loop is insufficient.

2. Decompose the workflow into local transactions.
   - For each step, record: owner, command, local atomic state change, emitted event/reply, input id, output id, timeout, and durability point.
   - Keep each local transaction within one service or resource boundary when possible.
   - Require reliable state change plus message publication through an outbox, event sourcing, durable command log, or equivalent mechanism.
   - Treat the saga log as operational state, not debug logging.

3. Classify each step.
   - `compensable`: can be undone by a domain-specific action, such as cancel reservation, release hold, refund, revoke grant, close ticket, delete artifact, or restore previous policy.
   - `pivot`: the point of no return or commitment boundary where prior compensation no longer defines the recovery strategy.
   - `retryable`: must eventually complete after the pivot and must be idempotent.
   - `irreversible`: cannot be safely undone; move it late, guard it with validations, or require human approval.

4. Design compensation semantics before implementation.
   - Write the compensation action for every compensable step at the same time as the forward action.
   - Define what compensation means in business terms; do not assume it restores the exact original database state.
   - Account for concurrent changes: compensation must not overwrite legitimate work that happened after the forward step.
   - Decide whether compensation order is reverse, priority-based, dependency-based, or parallel.
   - Include partial refunds, substitute resources, customer choice, or manual review when domain rules make simple rollback wrong.

5. Choose coordination style.
   - Use orchestration when the workflow is complex, needs explicit state, has many branches, needs centralized recovery, or must be inspectable by operators.
   - Use choreography only for simple flows with few participants and low risk of cyclic dependencies or hidden command/event coupling.
   - For auto-orchestrators, prefer an explicit saga state machine unless the existing domain architecture already has mature event choreography.
   - Make every participant command/reply contract explicit even when the transport is event-driven.

6. Decide retry, alternative path, compensation, and human-review policy.
   - Retry transient failures before compensation when forward progress is safe and cheaper than undo.
   - Try an alternative path when domain rules prefer completion, such as substituting a provider or resource.
   - Trigger compensation when a nontransient failure, exhausted retry budget, cancellation request, or violated business rule makes forward progress invalid.
   - Pause for human review when the decision is high impact, ambiguous, legally sensitive, financially material, or hard to automate safely.

7. Persist enough state to resume both directions.
   - Store saga id, tenant, operation type, current state, completed steps, compensation records, pivot status, idempotency keys, correlation ids, external transaction ids, retry counters, deadlines, and audit trail.
   - Checkpoint state after each durable forward step and after each compensation step.
   - Make compensation records durable before or atomically with declaring a forward step complete.
   - Preserve failure reasons and operator context for dead-letter or manual-recovery paths.

8. Make forward and compensation commands idempotent.
   - Use stable operation keys for each forward command and each compensation command.
   - Duplicate forward commands must not create duplicate effects.
   - Duplicate compensation commands must not overcompensate, such as issuing two refunds or releasing more inventory than reserved.
   - Reconcile timed-out external calls by status lookup or transaction id before retrying or compensating.

9. Address saga isolation anomalies.
   - Look for dirty reads, lost updates, fuzzy reads, stale decisions, and two sagas compensating against the same resource.
   - Add semantic locks, pending states, version checks, reread-before-write, commutative updates, ordering logs, quotas, or risk-based locks where needed.
   - Expose pending or reserved states to readers so they do not treat unfinished saga work as final truth.
   - Keep high-risk irreversible work behind stronger validation or stronger consistency mechanisms.

10. Test the unhappy paths directly.
   - Fail after each forward step and verify the chosen compensation chain.
   - Crash after recording a step, after executing a step, after emitting a message, and during compensation.
   - Deliver duplicate forward and compensation messages concurrently and sequentially.
   - Simulate compensation failure, dead-letter movement, timeout ambiguity, human review, cancellation after partial success, and retry exhaustion.
   - Verify final state, audit trail, operator alert, no duplicate side effects, no tenant cross-talk, and clear user-visible status.

## Output Format / Deliverables

Return a saga contract with:

- `saga_boundary`: operation, participants, consistency promise, and acceptable final states.
- `step_table`: step owner, forward action, durability point, emitted message, timeout, and classification.
- `compensation_plan`: compensation action, ordering, idempotency key, concurrency guard, and manual-review fallback.
- `pivot_and_retry_policy`: pivot step, retry-before-compensate rules, alternative paths, and cancellation policy.
- `state_model`: durable saga fields, correlation ids, external transaction ids, and operator-visible statuses.
- `tests`: failure-after-each-step, duplicate forward/compensation, crash recovery, timeout ambiguity, and isolation-anomaly checks.

## Failure, Recovery, and Idempotency

- Re-running this skill should update the same saga contract by stable saga id and step ids, not create conflicting recovery semantics.
- If a step has no safe compensation, classify it as pivot or irreversible and move it later, guard it, or require human approval.
- If compensation fails, the workflow must enter retryable compensation, manual review, or terminal partial-compensation state with audit context.
- Forward and compensation commands must each have stable idempotency keys to prevent duplicate provisioning, refunds, releases, deletes, or notifications.

## Failure Modes

- Treating compensation as automatic database rollback instead of domain-specific forward repair.
- Designing forward actions first and discovering later that one step has no safe compensation.
- Putting irreversible or legally binding steps before critical validations and reversible reservations.
- Triggering compensation for every transient error instead of retrying or using a safe alternative path.
- Assuming compensation always runs in exact reverse order when dependencies or business risk require another order.
- Losing the compensation plan because the orchestrator records it only in memory or after the forward effect escapes.
- Allowing duplicate compensation commands to create extra refunds, releases, deletes, or notifications.
- Hiding saga progress in logs without a queryable state model, making recovery and customer support guesswork.
- Choosing choreography for a complex flow until event dependencies become cyclic, opaque, and difficult to test.
- Ignoring isolation anomalies between concurrent sagas that touch the same resources.
- Ending in "failed" without a compensated, retryable, or manually recoverable state.

## Boundaries

- This skill designs saga and compensating-transaction behavior for auto-orchestrator workflows; it is not a general microservices migration guide.
- Use idempotency receiver guidance when the main problem is duplicate delivery or retry-safe consumers.
- Use checkpointing and rollback recovery when the main problem is restoring in-memory or stream state after worker failure.
- Use transaction-processing patterns when one atomic transaction can cover the full effect boundary.
- Use workflow/statechart modeling when the main deliverable is a formal state machine rather than compensation semantics.
- Do not add saga complexity to a stateless read, a single local ACID write, or a workflow where retrying forward is always safe and sufficient.
- If the system cannot tolerate temporary inconsistency or cannot reliably reach a valid compensated state, choose stronger consistency, reduce the workflow scope, or require explicit human operation.
- Optional provenance trace is recorded in `references/source-notes.md`; do not load it during normal runtime execution.

## Hard Rules

- Define compensation semantics before treating any forward step as production-ready.
- Do not call compensation a rollback unless it really restores the protected business invariant.
- Do not place irreversible work before required validations and reversible reservations without an explicit pivot decision.
- Persist saga progress and compensation records durably; logs alone are not a saga state model.
- Every duplicate forward or compensation command must be safe to replay.

## Source Closure

This 32-补偿事务-compensating-transaction skill is self-contained for runtime use; its source basis is Saga and Compensating Transaction pattern sources; local recovery entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
