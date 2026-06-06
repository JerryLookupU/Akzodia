---
name: 15-statecharts-automata
description: Use when designing, reviewing, or debugging auto-orchestrator task lifecycles as explicit state machines/statecharts, especially when states, events, retries, blocking, cancellation, concurrency, guards, or transition determinism must be specified.
source_files:
  - references/source-notes.md
---
# 15 Statecharts / Automata

## Book-Derived Essence

- Core framework: States + events + guards + actions + hierarchy + orthogonal regions + history. Behavior is legal transition structure.
- Deep idea: Statecharts compress complex reactive behavior by separating mode, event, guard, and action, while hierarchy prevents state explosion.
- Discovery method: Name stable modes, events that can arrive, guards that make them valid, side effects of transitions, parallel regions, terminal states, and illegal-event handling.
- Boundary: Do not build a state machine when behavior is purely data transformation with no persistent mode.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestration design has behavior that depends on current state plus incoming events:

- Defining lifecycle states such as `pending`, `ready`, `running`, `blocked`, `retrying`, `failed`, `succeeded`, and `cancelled`.
- Converting informal workflow rules into transitions with triggers, guards, and actions.
- Modeling parallel regions, such as task execution, budget tracking, approval policy, timeout handling, and cancellation handling.
- Avoiding state explosion by grouping common behavior under superstates.
- Auditing ambiguous behavior: duplicate transitions, missing defaults, impossible states, deadlocks, nondeterminism, or unclear retry/cancel precedence.

Do not activate for a stateless validation rule, a simple straight-line procedure, or a pure literature summary unless the user asks to apply state-machine semantics to an orchestrator.

## Activation And Execution Gate

Activate only when behavior depends on current state plus events, guards, actions, retries, blocking, cancellation, concurrency, history, or terminal-state correctness.

Before execution, identify the controlled entity, the state boundary, the event sources, terminal states, and at least one ambiguity or lifecycle requirement. If the prompt lacks events or legal transitions, ask for them or state a minimal event catalog before producing a table. If a simple status enum is enough, recommend that instead of a full statechart.

Standalone contract: this skill includes the required statechart/automata concepts for orchestration; `references/source-notes.md` is optional provenance and should not be needed to execute the workflow. During normal execution, do not read external files, webpages, original books, source reports, external source folder, distilled source material, or out-of-directory material.

## Workflow

1. Name the controlled entity and its boundary.
   - Identify the thing with state: task, run, agent session, tool call, approval request, queue item, or plan step.
   - Separate control state from data fields. State answers "what transitions are legal now"; data fields supply guards and action parameters.

2. Draft the flat automaton first.
   - List atomic states.
   - List external events, internal events, time events, and terminal events.
   - For every transition use this shape: `source -- event [guard] / action --> target`.
   - Prefer explicit events over hidden boolean polling. Examples: `worker_started`, `tool_returned`, `budget_exceeded`, `approval_denied`, `timeout_elapsed`.

3. Introduce hierarchy to remove repeated transitions.
   - Cluster states that share behavior into a superstate.
   - Put common exits on the superstate. Example: `active -- cancel_requested / stop_work --> cancelling` covers `ready`, `running`, `blocked`, and `retrying`.
   - Use default entry for first entry into a compound state. Use history entry only when re-entering should restore the last active substate.

4. Introduce orthogonal regions only for genuinely concurrent concerns.
   - Split a state into AND regions when the system is simultaneously in one state from each region.
   - Good orchestrator regions: execution lifecycle, budget lifecycle, approval lifecycle, cancellation lifecycle, and telemetry lifecycle.
   - Connect regions with events/actions, not shared mutation. A transition in one region may emit an event consumed by another region.

5. Specify guards, actions, and activities.
   - Guards are predicates checked at the event instant: `[attempts < maxAttempts]`, `[hasRunnableDependencies]`.
   - Actions are instantaneous effects: `/ enqueue_task`, `/ emit_retry_scheduled`, `/ persist_failure`.
   - Activities take time and must have start/stop control: `start(tool_call)`, `stop(tool_call)`, `active(tool_call)`.

6. Define transition priority and determinism.
   - For every atomic configuration, an event should select zero or one intended transition unless nondeterminism is explicitly part of the design.
   - Resolve conflicts between descendant and ancestor transitions. State the precedence rule, usually "more specific state wins" unless the runtime has a different convention.
   - Define simultaneous event handling: batching, ordering, or microstep closure until no generated internal events remain.

7. Check completeness.
   - For each nonterminal state, list accepted events and ignored events.
   - For each terminal state, confirm no transition escapes except an explicit reset/reopen path.
   - Confirm every compound state has a default entry or all incoming transitions target a substate.
   - Confirm retry, timeout, cancellation, and failure paths leave no running activity behind.

8. Produce an implementable contract.
   - Include a state table, event catalog, guard catalog, action catalog, and transition table.
   - Add invariants, for example: "a task cannot be both `running` and `blocked`"; "a cancelled run cannot emit success"; "tool activity is stopped before entering any terminal state".
   - Add tests that cover each transition, ancestor-level common exits, parallel-region synchronization, and conflict cases.

## Output Format / Deliverables

Return the artifacts needed to implement or audit the lifecycle:
- Boundary: controlled entity, state/data separation, terminal states, and assumptions.
- Catalogs: states, events, guards, actions, activities, and generated internal events.
- Transition table: `source -- event [guard] / action --> target`, including ignored events where that matters.
- Statechart structure: superstates, default/history entries, orthogonal regions, priority rule, and simultaneous-event handling.
- Verification set: invariants, unreachable/impossible states, nondeterminism checks, activity cleanup rules, and transition tests.

## Failure / Recovery / Idempotency

If events are missing, do not infer a complete transition system; return a partial model and the event questions needed to close it. If parallel regions create unclear synchronization, collapse to a smaller lifecycle and add events between regions later.

For repeated revisions, preserve stable state and event names unless their semantics change. Treat new states and transitions as migrations that need compatibility notes for persisted runs.

When an implementation enters an illegal or unknown state, recover by defining a quarantine/reconcile transition, stopping active external work, emitting audit evidence, and returning only through an explicit reset, reopen, or compensation path.

## Hard Rules

- Do not derive lifecycle state from multiple independent booleans when illegal combinations matter.
- Do not allow the same event from the same atomic configuration to select multiple transitions unless nondeterminism is intentional and documented.
- Do not enter a compound state without a default substate or an explicit target substate.
- Do not enter terminal states while timers, subscriptions, or tool activities remain uncontrolled.
- Do not model ordinary data values as states unless they change legal transitions.

## Failure Modes

- Flat-state explosion: every combination of execution, approval, budget, and cancellation is represented as a separate state. Use orthogonal regions instead.
- Boolean soup: state is inferred from many flags, producing illegal combinations. Promote lifecycle flags into one explicit state or region.
- Ambiguous transitions: the same event is legal from both a substate and an ancestor without a stated priority.
- Missing default/history semantics: entering a compound state does not say which substate becomes active.
- Unstopped activities: terminal states are reached while external work, timers, or subscriptions remain active.
- Over-broadcasting: internal events create accidental cycles or cross-region coupling. Keep event names scoped and document generated events.
- Modeling everything as a state: use data fields for values that do not change legal transitions.

## Boundaries

This skill is for discrete-event control behavior. It does not replace scheduling policy, dependency graph design, resource allocation, formal verification tools, or distributed consensus design.

Do not use statecharts when a simple straight-line procedure or stateless validation rule is enough. Do use them when the orchestrator must be resumable, inspectable, testable, and correct under retries, concurrent regions, or asynchronous events.

Source provenance is recorded in `references/source-notes.md`; do not read it for normal execution.

## Source Closure

This 15-statecharts-automata skill is self-contained for runtime use; its source basis is Statecharts and automata sources; local state-machine entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
