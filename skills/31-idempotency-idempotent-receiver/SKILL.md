---
name: 31-idempotency-idempotent-receiver
description: Use when designing or reviewing auto-orchestrator steps, message consumers, retry loops, tool gateways, webhooks, queues, resumable runs, or recovery paths that may process the same command/event more than once. Trigger for duplicate delivery, at-least-once execution, idempotency keys, deduplication tables, repeat-safe side effects, retry safety, redelivery, timeout reconciliation, or "exactly once" claims backed by receiver behavior.
source_files:
  - references/source-notes.md
---
# 31 Idempotency / Idempotent Receiver

## Book-Derived Essence

- Core framework: Stable operation identity + duplicate detection + state-specific response + side-effect reconciliation.
- Deep idea: Idempotency is not “do it twice safely” in the abstract; it is a contract for what repeated messages mean at each state boundary.
- Discovery method: Find retry boundaries, idempotency keys, durable duplicate store, external side effects, retention windows, and response behavior for completed/failed/in-flight states.
- Boundary: Do not claim idempotency when side effects happen before the duplicate record is durable.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when duplicate execution is possible and correctness depends on making the receiver safe:

- A queue, webhook, scheduler, agent step, tool call, callback, or replay source can deliver the same work item more than once.
- A run uses at-least-once retries, crash recovery, checkpoint restore, queue redelivery, client retry, or timeout retry.
- The action has visible side effects: payment, billing, notification, ticket creation, file write, deployment, database mutation, external API call, or final run status.
- A design claims "exactly once" but the receiver has no durable duplicate detection, semantic idempotency, or effect reconciliation.
- You need to choose idempotency key shape, dedupe storage, retention, result replay, or duplicate response behavior.
- You are composing auto-orchestrator recovery with queues, checkpoints, sagas, compensating transactions, or external tools.

## Do Not Trigger

- Do not use this skill for a purely mathematical explanation of idempotent functions.
- Do not use it for read-only, stateless, or safely recomputable work with no side effect or audit need.
- Do not use it as the primary guide for multi-step business rollback; use saga or compensating-transaction design instead.
- Do not use it for generic retry tuning unless duplicate receiver effects are part of the risk.

## Standalone Contract

This skill is self-contained. Do not browse, open, or depend on external source files, source reports, original books, websites, or cross-skill distilled text during normal execution. `references/source-notes.md` is optional provenance only, not required runtime knowledge. A compliant answer must identify the duplicate boundary, idempotency identity, durable duplicate store, state-specific duplicate behavior, side-effect reconciliation path, retention window, and duplicate-path tests.

## Activation and Execution Gate

Proceed only if all of these are true:

1. The request involves a receiver, sink, tool adapter, workflow step, callback, or finalizer that may observe the same work more than once.
2. Repeating the work can create a different business, user-visible, external, durable, or audited effect.
3. The answer can name the intended operation identity separately from retry attempt identity.

If any condition is false, state why this skill is not the right fit and route to the relevant boundary guidance.

## Workflow

1. Define the duplicate boundary.
   - Name the receiver that must be safe: message endpoint, worker step, tool adapter, webhook handler, run finalizer, sink writer, or human-handoff callback.
   - State what counts as "same work": same command intent, same event id, same run-step-attempt, same external request, same artifact commit, or same business operation.
   - Separate duplicate delivery from duplicate intent: two retries of one command should collapse, while two legitimate user orders should not.

2. Classify the operation's natural idempotency.
   - Safe by semantics: setting status to a target value, upserting by stable id, replacing an artifact by content hash, or acknowledging an already-completed step.
   - Unsafe by default: incrementing counters, appending messages, charging money, sending notifications, creating tickets, allocating scarce resources, or calling opaque APIs.
   - If semantics are unsafe, require explicit deduplication or a transaction/compensation design before allowing automatic retry.

3. Choose the idempotency identity.
   - Prefer a stable business key for the intended effect, such as `tenant_id + operation_id`, `run_id + step_id + effect_type`, `order_id + charge_kind`, or `message_id`.
   - Include tenant and authorization scope in the key so one tenant cannot suppress another tenant's effect.
   - Avoid attempt numbers, timestamps, random retry ids, or worker-local ids as the primary key; they distinguish duplicates instead of collapsing them.
   - Version the key when the effect semantics change in an incompatible way.

4. Persist duplicate knowledge before or atomically with the effect.
   - Store an idempotency record in durable shared storage, not process memory.
   - Track at least: key, operation kind, input fingerprint, status, result pointer or response, external transaction id, timestamps, owner/lease, and error class.
   - Use a unique constraint, conditional write, compare-and-set, or transaction to ensure only one worker wins the first execution.
   - If storage and side effect cannot be atomic, persist a pending state and reconcile by external transaction id before retrying.

5. Define duplicate behavior for each state.
   - `completed`: return the stored result or acknowledge success without repeating the side effect.
   - `pending/running`: wait, poll, take over only after a lease expires, or return a retryable conflict.
   - `failed-retryable`: retry with the same key after checking whether the external effect actually happened.
   - `failed-terminal`: return the stored terminal failure unless a human or policy explicitly clears it.
   - `fingerprint mismatch`: reject as key reuse with different intent; do not silently dedupe.

6. Make side effects repeat-safe.
   - Pass the idempotency key to downstream APIs that support it.
   - For downstream systems without idempotency support, keep an outbox, external transaction pointer, lookup/reconciliation path, or compensating transaction.
   - For notifications and append-only artifacts, dedupe by message/effect id at the sink or make the append include a stable unique id.
   - For finalization, commit one final status and one user-visible completion event per run.

7. Set retention and replay windows.
   - Keep idempotency records at least as long as the maximum redelivery, replay, client retry, checkpoint restore, or webhook retry window.
   - Retain high-risk effects longer than low-value internal messages.
   - Garbage-collect with tenant isolation, audit needs, privacy requirements, and external dispute windows in mind.
   - Expired dedupe records must be treated as a conscious risk, not as proof that duplicates are impossible.

8. Integrate with orchestrator recovery.
   - Store idempotency keys in checkpointed or replayable state so recovered workers reuse the same keys.
   - Do not infer that a timed-out tool call failed; reconcile by key, external transaction id, or status lookup.
   - When a queue redelivers after worker crash, the next worker must observe the same idempotency record before producing a second effect.
   - Make retries use the same operation key and a new attempt id only for observability.

9. Test duplicate paths directly.
   - Send the same message twice concurrently and sequentially.
   - Crash after claiming the idempotency key, after the external call, and before recording completion.
   - Redeliver after checkpoint restore, lease expiry, client timeout, and partial downstream outage.
   - Verify one business effect, stable stored result, clear conflict on mismatched payloads, no tenant cross-talk, and auditable duplicate handling.

## Output Format / Deliverables

Return a concise idempotent-receiver contract with:

- `receiver_boundary`: receiver name, side effect, and what counts as the same work.
- `idempotency_key`: fields included, fields excluded, tenant/auth scope, and versioning rule.
- `dedupe_record`: durable fields, uniqueness/conditional-write mechanism, and retention window.
- `state_behavior`: behavior for completed, pending/running, retryable failure, terminal failure, and fingerprint mismatch.
- `downstream_reconciliation`: how external APIs, timeouts, and non-idempotent sinks are handled.
- `tests`: duplicate, crash, timeout, tenant isolation, and mismatched-payload checks.

## Failure, Recovery, and Idempotency

- Re-running this skill should refine the same receiver contract; preserve stable operation keys unless the effect semantics change.
- If key choice, side-effect boundary, or downstream reconciliation is unknown, stop and ask for that information before prescribing automatic retry.
- For partial designs, mark unresolved states explicitly as `requires_reconciliation`, `requires_human_review`, or `unsupported_retry`.
- Never treat a timeout as proof of failure; require lookup or reconciliation before repeating the effect.

## Failure Modes

- Using in-memory dedupe, worker-local caches, or short-lived locks as the only duplicate defense.
- Creating a new idempotency key per retry or per attempt, which guarantees retries can repeat the effect.
- Treating message broker "exactly once" features as enough while the receiver still performs non-idempotent external side effects.
- Deduping only by payload hash when two legitimate operations can share the same payload.
- Deduping only by message id when the same business command can be republished with a new transport id.
- Marking an operation complete before the side effect is actually durable, or after it completes without storing the result needed for duplicate responses.
- Retrying a timed-out external call without checking whether it later succeeded.
- Letting idempotency records expire before all plausible redelivery and recovery paths are closed.
- Ignoring payload mismatch for a reused key, causing one request to receive another request's result.
- Forgetting tenant, actor, or permission scope in the dedupe key.

## Boundaries

- This skill designs idempotent receiver behavior for auto-orchestrator duplicate safety; it is not a complete messaging architecture guide.
- Use checkpointing and rollback recovery when the main problem is restoring long-running state after failure.
- Use saga or compensating transaction design when the main problem is undoing or reconciling a multi-step business transaction.
- Use transaction-processing patterns when a single database transaction can cover the full effect boundary.
- Idempotency reduces duplicate side effects; it does not guarantee global exactly-once execution across arbitrary external systems.
- Do not add heavy dedupe infrastructure to purely read-only, stateless, or trivially recomputable work unless retry volume or audit requirements justify it.
- Optional provenance trace is recorded in `references/source-notes.md`; do not load it during normal runtime execution.

## Hard Rules

- Use a stable operation key for the intended effect, not an attempt id, timestamp, or worker-local id.
- Persist duplicate knowledge in durable shared storage before or atomically with the effect whenever possible.
- Reject key reuse with a different input fingerprint.
- Include tenant and authorization scope in the key or record.
- Define duplicate behavior for every stored state before enabling automatic retry.

## Source Closure

This 31-idempotency-idempotent-receiver skill is self-contained for runtime use; its source basis is Idempotent Receiver pattern sources and local idempotency entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
