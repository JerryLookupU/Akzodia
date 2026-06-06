---
name: 14-petri-nets
description: Use when designing or repairing an auto-orchestrator workflow with concurrent agents, resource tokens, locks, queues, approvals, retries, handoffs, deadlock risk, bounded-capacity constraints, reachable-state questions, or a need to export/import formal process models through PNML-style Petri net structure.
source_files:
  - references/source-notes.md
---
# 14 Petri Nets

## Book-Derived Essence

- Core framework: Places hold tokens; transitions fire when enabled; reachability, liveness, boundedness, and invariants expose concurrency defects.
- Deep idea: Petri nets make concurrency concrete. They reveal where resources are consumed, produced, blocked, duplicated, or left unreachable.
- Discovery method: Map states/resources to places and events/actions to transitions, then test enabling conditions, token conservation, reachable markings, deadlocks, and unbounded growth.
- Boundary: Do not use Petri nets when the process has no concurrency, resource sharing, or state-space risk.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when orchestration correctness depends on how state and resources move through a concurrent workflow, not just on task ordering.

Strong triggers:
- Multiple agents, tools, jobs, or human approvals may run concurrently and contend for shared resources.
- A workflow can deadlock, starve a branch, leak a lock, overfill a queue, or consume a budget/token twice.
- The orchestrator needs to prove or inspect whether a desired state is reachable from the current state.
- Work items move through queues, buffers, gates, retries, joins, fan-outs, or compensation steps.
- A state machine is becoming too large because independent resources and control states combine into many global states.
- A formal interchange or tool-analysis artifact is needed, especially one compatible with PNML concepts: places, transitions, arcs, net types, markings, and extensions.

Prefer a plain dependency graph when tasks only need static ordering. Prefer a finite state machine when there is one small control state and no meaningful resource multiplicity.

## Activation And Execution Gate

Activate only when correctness depends on tokens, resources, concurrency, reachability, boundedness, liveness, deadlock freedom, or PNML-style formal interchange. Do not activate for a simple static dependency list, a pure history/definition question, or a lifecycle with one small control state and no resource multiplicity.

Before execution, identify the safety question, net boundary, initial marking, candidate places, candidate transitions, and at least one token/resource whose conservation or movement matters. If these are absent, ask for the missing runtime state or declare a minimal assumed marking before analysis. If the request only needs a direct bug fix, produce the Petri-net insight only as much as needed to justify the repair.

Standalone contract: this skill contains the required Petri-net concepts for orchestration work; `references/source-notes.md` is provenance only and is not required for normal execution. During normal execution, do not read external files, webpages, original books, source reports, external source folder, distilled source material, or out-of-directory material.

## Workflow

1. Define the net boundary.
   - Name the orchestrated system and the safety question: deadlock freedom, bounded queues, no duplicate resource use, liveness, reachability, or PNML interchange.
   - Choose the net type conservatively: Place/Transition net for ordinary orchestration; high-level or colored nets only when tokens need typed payloads; stochastic/timed variants only when timing or probability is part of the decision.
   - Keep one net focused on one coordination layer. Do not mix domain data modeling, UI flow, and infrastructure locks in the same first pass.

2. Map orchestration concepts to Petri-net primitives.
   - Places represent conditions, resource pools, queues, locks, budgets, permits, work states, or waiting rooms.
   - Tokens represent available resources, active work items, held locks, pending approvals, remaining retries, or outstanding obligations.
   - Transitions represent atomic events the orchestrator may fire: start task, acquire lock, finish tool call, branch, join, retry, compensate, release, escalate.
   - Directed arcs represent token consumption and production. Weight an arc when a transition consumes or produces more than one token.
   - Initial marking is the current token count for every place. Treat it as the workflow's explicit runtime state.

3. Specify firing rules before planning.
   - A transition is enabled only when every input place has enough tokens for its incoming arc weights and any guard condition is true.
   - Firing is atomic: consume all required input tokens, then produce all output tokens.
   - If two enabled transitions require the same scarce token, mark them as a conflict and add a policy: priority, scheduler choice, reservation, or user decision.
   - If two enabled transitions have disjoint consumed/produced places, mark them as concurrency candidates.

4. Analyze execution risk.
   - Reachability: list target markings that must be possible, such as `all_work_done` with all locks released.
   - Deadlock: look for reachable markings where no useful transition is enabled while obligations remain.
   - Liveness: for each essential transition, ask whether it can eventually fire again from every relevant reachable marking.
   - Boundedness: set maximum acceptable token counts for queues, retries, spawned agents, budgets, files in flight, or outstanding approvals.
   - Conservation: check whether important tokens are neither lost nor duplicated across every transition, such as locks, budget permits, task ownership, or approval rights.
   - Invariants: write simple place-sum rules when available, such as `free_worker + busy_worker = worker_capacity`.

5. Repair the orchestration design.
   - Add release transitions for every acquire transition and compensation transitions for irreversible side effects.
   - Add join places when all branches must finish before continuing; add separate places when either branch may continue.
   - Add capacity places to bound queues or parallelism instead of relying on informal comments.
   - Split a transition if it hides a non-atomic operation, such as "run tool and commit result"; model start, success, failure, and cleanup separately.
   - Replace ambiguous shared state with explicit resource tokens, version tokens, or lock places.
   - When starvation is possible, add fairness, aging, priority rotation, or bounded retry transitions as scheduler policy outside the pure net.

6. Produce the orchestrator artifact.
   - Return a compact net table: places, transitions, input arcs, output arcs, guards, and initial marking.
   - Call out conflicts, concurrency candidates, invariants, bounded places, and deadlock-prone markings.
   - Convert the net into execution rules: when each transition is enabled, what state it consumes/produces, and what evidence confirms the firing.
   - If interchange matters, describe the PNML/PNTD expectations: net type, namespace, abstract syntax assumptions, concrete XML/RELAX-NG validation, and which extensions are non-standard.

## Output Format / Deliverables

Return a compact formal artifact:
- Scope: system boundary, safety question, chosen net type, and modeling assumptions.
- Net table: places with meanings and initial tokens; transitions with atomic event meanings; input arcs, output arcs, weights, and guards.
- Analysis: enabled transitions, conflicts, concurrency candidates, invariants, bounded places, reachable target markings, and deadlock-prone or starvation-prone markings.
- Repair plan: release/cleanup transitions, capacity places, joins, compensation transitions, fairness policy, and runtime enforcement requirements.
- Optional interchange note: PNML/PNTD net type, namespace, validation assumptions, and non-standard extensions.

## Failure / Recovery / Idempotency

If the initial marking is unknown, stop reachability claims and provide only a structural model plus the data needed to complete analysis. If the net grows too large, split coordination layers rather than mixing unrelated domains.

For repeated runs, preserve stable place and transition names when semantics are unchanged. Compare new markings, invariants, and deadlock findings against the prior model so repairs are incremental and auditable.

When a modeled execution reaches a bad marking, recover by identifying the missing release, compensation, capacity, guard, or scheduler policy; then update the net and the orchestrator rule together.

## Hard Rules

- Do not treat places as tasks or transitions as passive dependencies.
- Do not make reachability, deadlock, liveness, or boundedness claims without an initial marking and firing rules.
- Do not hide non-atomic tool work inside one transition when failure between start and finish matters.
- Do not rely on comments for capacity, locks, retries, or permits; model them as tokens or explicit guards.
- Do not claim PNML portability for custom net features without naming the extension and validation assumption.

## Failure Modes

- Treating places as tasks and transitions as dependencies. Places hold state or resources; transitions are atomic events that move tokens.
- Forgetting the initial marking. Without token counts, there is no executable state model.
- Hiding long-running work in one transition. Petri-net transitions should be atomic relative to the coordination problem.
- Modeling only the happy path. Failures, timeouts, cancellations, retries, and cleanup usually determine whether locks leak or deadlocks appear.
- Ignoring arc weights and capacity. Resource bugs often come from consuming or producing the wrong number of tokens.
- Calling everything concurrent because transitions are independently named. Concurrency requires disjoint or compatible token effects.
- Assuming PNML extension means tool portability. Custom PNTDs may be readable only by tools that understand that net type or namespace.
- Overbuilding a formal model when the workflow is small, linear, and has no resource multiplicity.

## Boundaries

Petri nets are a coordination and reachability model. They do not decide business priority, user value, tool quality, or semantic correctness of an agent's generated content.

Plain Place/Transition nets do not represent rich data-dependent logic well. Use high-level or colored nets for typed tokens, or keep data predicates as external guards with clear inputs and outputs.

Petri-net analysis can expose possible deadlocks and unreachable states, but it is not a substitute for runtime enforcement. The orchestrator still needs atomic state updates, durable persistence, idempotency keys, and lock discipline.

PNML is an interchange framework, not a guarantee that every tool supports every extension. If a model uses reset arcs, inhibitor arcs, stochastic annotations, modularity, or other custom features, state the net type and validation assumptions explicitly.

## Source Closure

This 14-petri-nets skill is self-contained for runtime use; its source basis is Petri net theory sources and local Petri-net entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
