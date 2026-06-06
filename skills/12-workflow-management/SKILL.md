---
name: 12-workflow-management
description: Use when designing, evaluating, or repairing an auto-orchestrator workflow that needs explicit control-flow routing: sequence, parallel split/join, conditional branching, OR-joins, first-winner joins, cancellation, deferred choice, milestones, dynamic fan-out, multiple-instance synchronization, or tool/agent capability checks for workflow expressiveness.
source_files:
  - references/source-notes.md
---
# 12 Workflow Management

## Book-Derived Essence

- Core framework: Tokens move through sequence, split, join, choice, cancellation, milestone, and multiple-instance patterns.
- Deep idea: Workflow theory’s essence is control-flow semantics. The question is not “what are the steps?” but “what exactly enables, disables, joins, races, or cancels work?”
- Discovery method: Identify the case, token meaning, branch cardinality, join rule, cancellation rule, loop exit, and runtime state exposure. Ambiguous joins are where deadlocks and duplicates hide.
- Boundary: Do not use workflow patterns for a simple linear task list with static dependencies.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestration problem is not just "what tasks exist?" but "how should execution tokens move, wait, race, cancel, and terminate?"

Strong triggers:
- An agent workflow needs parallel branches, joins, conditional routing, retries, loops, cancellation, or early termination.
- A plan fans out to an unknown number of agents, files, tools, reviewers, shards, tickets, or subtasks and later needs to know when to continue.
- The workflow has races: user action versus timeout, first successful tool result versus slower alternatives, audit versus normal processing, or cancel versus continue.
- A routing bug appears as duplicated downstream work, deadlock at a join, lost branch completion, stale enabled task, or a process that never terminates.
- You need to compare orchestration runtimes, queue systems, state machines, agent frameworks, or workflow engines by their actual control-flow expressiveness rather than vendor labels.
- You are translating an informal process diagram into executable orchestrator semantics.

Prefer a simpler checklist or dependency graph when all tasks are linear, every dependency is static, and no branch can be optional, repeated, racing, canceled, or dynamically created.

## Standalone Contract

This skill is self-contained for designing or auditing control-flow routing semantics in auto-orchestrators. `references/source-notes.md` records provenance and pattern rationale only.

Runtime dependency rule: do not open or depend on external files, webpages, original books, source reports, source snapshots, external source folders, or files outside this skill directory. Use `SKILL.md` as the executable contract; local `references/`, `assets/`, or `examples/` may be used only when present and only as optional in-skill support.

Activation gate: use this skill only when the request involves execution-token movement, branching, joining, racing, cancellation, loops, dynamic fan-out, milestones, deferred choice, or runtime expressiveness checks. Do not activate for task discovery, WBS, database schema selection, or simple linear dependency lists.

Execution gate: before choosing patterns, identify the case instance, atomic activities, active token/thread meaning, expected branch cardinality, join expectations, cancellation semantics, and target runtime support. If the runtime cannot expose needed state, specify compensating state variables and tests before relying on the design.

## Workflow

1. Define the workflow case and token model.
   - Name the case instance: request, job, run, conversation, issue, document, deployment, or incident.
   - Identify activities that are atomic from the orchestrator's perspective: tool call, agent delegation, file edit, review, approval, test, publish, rollback.
   - Decide what counts as a token or active thread: queued work item, running agent, awaited event, timer, spawned subprocess, or pending approval.
   - Record whether the runtime exposes explicit state between activities. If not, state-based patterns will need extra guards, locks, cancellation APIs, or queue bookkeeping.

2. Map the basic control flow first.
   - Use `sequence` for strict "after completion" ordering.
   - Use `parallel split` when one branch intentionally creates several concurrent threads.
   - Use `synchronization` only when each incoming branch is expected exactly once.
   - Use `exclusive choice` when exactly one branch is selected by control data or a decision step.
   - Use `simple merge` only when alternative incoming branches cannot run in parallel.
   - Verify each join has a stated expectation: how many signals it waits for, whether duplicate signals are possible, and what happens to late signals.

3. Choose advanced branching and merge semantics deliberately.
   - Use `multi-choice` when zero, one, or many branches may be selected from a set. Define the predicate for each branch and whether "none selected" is legal.
   - Pair multi-choice with `synchronizing merge` when downstream work must run exactly once after all actually selected branches finish.
   - Use `multi-merge` when every incoming branch activation should trigger the downstream activity. Expect duplicate downstream executions by design.
   - Use `discriminator` or `n-out-of-m join` when the first branch, or the first n branches, should release downstream work while remaining branches are drained or ignored.
   - For every advanced merge, add a trace table of expected completions: selected branches, completion order, downstream activations, ignored late events, and reset behavior in loops.

4. Model loops and termination separately from happy-path routing.
   - Decide whether loops are structured with one entry/exit or arbitrary cycles are needed for natural repair/retry behavior.
   - Prefer explicit loop state for retries, redo, and backtracking: attempt count, last failure, retryable flag, branch still active.
   - Use implicit termination when a case should finish when no active activities or enabled activities remain.
   - Use explicit final nodes only when reaching that node should cancel or ignore all remaining active work.
   - Test termination with optional branches, skipped branches, dynamic instances, and cancellation paths.

5. Handle multiple instances as a separate design problem.
   - Classify fan-out cardinality:
     - Design-time known: fixed number of parallel copies, such as three approvals.
     - Runtime known before launch: number discovered before spawning, such as files in a batch.
     - Runtime unknown while running: new instances can appear while existing ones run, such as late evidence, deliveries, or subtasks discovered by agents.
     - No synchronization needed: spawned work is fire-and-forget relative to the main case.
   - For synchronized fan-out, track `spawned_count`, `completed_count`, `failed_count`, and `closed_to_new_instances`.
   - Continue only when the selected completion rule is true: all spawned complete, quorum reached, first success, all required classes represented, or explicit cancellation.
   - Avoid hiding synchronization in arbitrary scripts unless the workflow artifact also documents the counter, lock, event, and idempotency semantics.

6. Make state-based choices explicit.
   - Use `deferred choice` when the environment decides which branch starts first: timeout versus response, user approval path versus manager path, first available resource, first tool callback.
   - Implement deferred choice with an atomic race: enable alternatives, let one winner claim the case, then withdraw the losers before they can start.
   - Use `interleaved parallel routing` when several activities may run in any order but not concurrently because they share mutable state.
   - Implement interleaving with a case-level mutex, resource lock, or explicit state place, not with true parallel execution.
   - Use `milestone` when an activity is enabled only while the case is in a phase, such as "after questionnaire sent and before archive" or "before invoice printed."
   - Milestones must support both enabling and withdrawal. A Boolean flag alone is insufficient if already-enabled work cannot be canceled.

7. Design cancellation as first-class routing.
   - Distinguish `cancel activity` from `cancel case`.
   - For activity cancellation, define whether it removes only queued work, also interrupts running work, or marks late results as ignored.
   - For case cancellation, enumerate all descendant instances, timers, callbacks, locks, reservations, and spawned subprocesses that must be withdrawn.
   - Make cancellation idempotent and race-aware: a cancel that arrives after completion must not resurrect or double-finalize the case.

8. Evaluate runtime support before committing to the design.
   - Mark each needed pattern as direct, indirect, or unsupported in the target orchestrator.
   - Treat "can be done with code, triggers, or hidden database updates" as indirect support, not direct workflow support.
   - If a critical pattern is unsupported, either simplify the business process, add a small explicit routing service, choose a different runtime, or document the compensating mechanism and its verification tests.
   - Prioritize tests around joins, dynamic fan-out, cancellation, deferred choice, and milestones; these are where silent semantic mismatches usually surface.

## Failure Modes

- Using a simple AND-join after optional branches. This can deadlock because the join waits for branches that were never selected.
- Using a simple merge after parallel branches. This can run downstream work multiple times or drop duplicate activations depending on runtime semantics.
- Treating multi-choice as exclusive choice. Optional work disappears when more than one branch should have run.
- Treating discriminator as a normal merge. Late branch completions can retrigger downstream work unless they are drained, ignored, and reset correctly.
- Hiding routing semantics in tool code, database triggers, or ad hoc queue consumers. The process diagram then stops describing the real process.
- Forgetting reset semantics in loops. Joins and discriminators must know which cycle each incoming signal belongs to.
- Assuming spawned child workflows remain related to the parent. API-created subprocesses often need explicit parent id, cancellation, status aggregation, and audit propagation.
- Using true parallelism for activities that share mutable state. Use interleaving, locks, or serialized updates.
- Modeling a milestone as a stale Boolean check without withdrawal. Work enabled before the milestone expires may still run.
- Confusing explicit termination with implicit termination. A final node may abort active branches when the intended rule was "finish when nothing remains."

## Output Format

Return a workflow-control artifact with:

- `Case And Activities`: case identity, atomic activities, tokens/threads, and visible state.
- `Control-Flow Map`: sequence, splits, joins, choices, merges, loops, fan-out, and termination rule.
- `Join And Race Contracts`: expected signals, duplicate handling, late events, reset behavior, and winner withdrawal.
- `Multiple-Instance State`: spawned/completed/failed counts, closed-to-new flag, quorum or completion rule.
- `Cancellation Contract`: activity versus case cancellation, descendants, timers, callbacks, locks, and late-result handling.
- `Runtime Support Matrix`: direct, indirect, unsupported patterns, compensating mechanisms, and required tests.

## Failure, Recovery, And Idempotency

When a join, race, or cancellation bug appears, reconstruct the token trace first: selected branches, spawned instances, completions, late signals, withdrawals, and downstream activations. Repair by changing the explicit pattern contract or state variables, not by hiding semantics in ad hoc code.

Repeated runs should keep case IDs, branch IDs, spawned-instance IDs, and cycle/reset markers stable. Cancellation and finalization must be idempotent: duplicate or late signals must not resurrect, double-run, or double-finalize a case.

## Hard Rules

- Every join must state how many signals it waits for and what happens to duplicates, skipped branches, and late signals.
- Do not use an AND-join after optional branches unless the join waits only for actually selected branches.
- Do not model a milestone as a Boolean flag if already-enabled work cannot be withdrawn.
- Treat custom scripts, triggers, or hidden database updates as indirect support that requires explicit state, atomicity, observability, and tests.

## Boundaries

This skill covers static control-flow and routing semantics for orchestration. It does not by itself solve resource allocation, human organization modeling, transaction isolation, compensation logic, exception taxonomies, cost optimization, or task decomposition.

Run planning or decomposition work before this workflow-pattern pass when the main problem is discovering what tasks exist. Use this skill once the task set is roughly known and the risk is execution ordering, synchronization, racing, cancellation, or termination.

Do not overfit to the original paper's commercial workflow-engine comparison. Use the pattern catalog as a diagnostic lens for modern agent frameworks, queues, state machines, BPMN tools, DAG schedulers, serverless orchestrators, and local runtime contracts.

When the target runtime lacks direct support for a needed pattern, do not assume the pattern is impossible. But treat indirect implementations as engineering debt: specify state variables, atomicity, idempotency, observability, and tests before relying on them.

## Source Closure

This 12-workflow-management skill is self-contained for runtime use; its source basis is Workflow Patterns research and local workflow-management entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
