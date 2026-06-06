---
name: 13-business-process-management
description: Use when designing or repairing an auto-orchestrator that must manage a recurring business or agent process across the full lifecycle: identify process boundaries, model BPMN-like control flow, assign roles and handoffs, automate executable steps, monitor runtime events, analyze bottlenecks or exceptions, and redesign the process from evidence.
source_files:
  - references/source-notes.md
---
# 13 Business Process Management

## Book-Derived Essence

- Core framework: Process discovery -> modeling -> execution -> monitoring -> improvement with roles, handoffs, and performance measures.
- Deep idea: BPM treats a process as a repeatable operational asset, not an isolated plan. Ownership, handoff, exception handling, and measurement are part of the process itself.
- Discovery method: Follow a case instance through actors, activities, decisions, artifacts, exceptions, metrics, and improvement loops; then compare designed flow with actual work.
- Boundary: Do not use BPM for a one-time project plan or static taxonomy with no recurring instances.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestration problem is not just "finish this task once" but "operate, observe, and improve a repeatable process."

Strong triggers:
- A workflow spans multiple agents, tools, queues, approvals, users, teams, or systems and needs explicit ownership at each handoff.
- The process has recurring instances, such as lead qualification, incident response, claims handling, release management, onboarding, procurement, or data pipeline recovery.
- The orchestrator needs a process model that can drive execution, not just a static diagram.
- Runtime behavior matters: cycle time, waiting time, rework, escalations, exceptions, SLA misses, queue buildup, or compliance evidence.
- A user asks for modeling, simulation, automation, monitoring, optimization, or redesign of an operational workflow.
- BPMN terms appear: process, participant, pool, lane, event, task, gateway, message flow, sequence flow, subprocess, exception, escalation, timer, compensation, or process mining.

Prefer a simple checklist for one-off work with no repeated instances, no handoffs, and no need to learn from runtime data.

## Activation And Execution Gate

Activate only when the user needs to design, repair, monitor, or improve a repeatable operational process. Do not activate for a one-off checklist, a pure terminology question, or a static project plan with no runtime instances.

Before execution, confirm the work has at least one process boundary and one managed instance type. If the prompt lacks a start event, end state, instance key, owner/handoff, or process objective, ask for the missing item or state an explicit assumption before building the model. If the request is only educational, answer briefly without producing a process redesign.

Standalone contract: this skill must provide enough BPM lifecycle guidance to work without reading `references/source-notes.md`; references are optional provenance, not required runtime context. During normal execution, do not read external files, webpages, original books, source reports, external source folder, distilled source material, or out-of-directory material.

## Workflow

1. Frame the process as a managed lifecycle.
   - Name the process, the customer or beneficiary, the triggering event, and the desired outcome.
   - Set process boundaries: start event, end states, included work, excluded work, upstream inputs, and downstream outputs.
   - Define the process instance key, such as ticket id, order id, case id, customer id, run id, or document id.
   - State the performance goals: completion rate, cycle time, cost, quality, compliance, user effort, risk, or recovery time.

2. Discover the as-is process.
   - Extract actual steps from logs, tickets, traces, chat history, runbooks, API calls, database state, and user interviews.
   - Separate value-adding work from waiting, routing, inspection, correction, and rework.
   - Record variants instead of forcing premature uniformity: happy path, urgent path, exception path, manual fallback, and already-complete path.
   - Identify roles for every action: responsible executor, approver, consulted party, informed party, and owning system.
   - Mark evidence for each observed step so the model is grounded in runtime behavior, not just policy documents.

3. Build an executable process model.
   - Represent the process with BPMN-like primitives: start/end events, tasks, subprocesses, gateways, timers, messages, errors, compensation, pools, and lanes.
   - Use sequence flow for order within one participant; use message flow or explicit event contracts across participants.
   - Convert decision points into gateways with named conditions. Avoid vague branches such as "handle issue" without a testable condition.
   - Define each task as `input -> action -> output -> owner -> system -> success evidence`.
   - Make subprocesses for reusable or complex activities, such as validation, approval, exception triage, rollback, or user notification.

4. Add execution contracts for the orchestrator.
   - For each automated task, specify tool/API, required permissions, preconditions, idempotency key, timeout, retry policy, and side effects.
   - For each human task, specify queue, assignee rule, due date, escalation path, response schema, and what the orchestrator may do while waiting.
   - For each event, specify the detector: webhook, polling query, log pattern, scheduled timer, user message, state transition, or external callback.
   - For each gateway, specify the exact data fields used and where stale or missing data is rechecked.
   - For each exception boundary, specify recovery: retry, compensate, escalate, pause for approval, route to manual handling, or terminate cleanly.

5. Instrument the process before optimizing it.
   - Emit process-instance events for start, task-ready, task-started, task-completed, waiting, exception, escalation, compensation, cancellation, and end.
   - Attach correlation ids so events from agents, tools, and users join back to one process instance.
   - Track cycle time, processing time, waiting time, queue length, branch frequency, rework loops, failure causes, and SLA breaches.
   - Preserve audit evidence for irreversible actions, approvals, policy decisions, and externally visible outputs.
   - Define dashboards or queries that answer: where do instances wait, where do they fail, and which variants dominate volume?

6. Analyze and redesign.
   - Find bottlenecks by comparing waiting time, handoff count, queue depth, rework, and exception frequency across variants.
   - Challenge every gateway, approval, and handoff: remove, automate, parallelize, batch, split by risk, or move earlier only when evidence supports it.
   - Redesign with explicit tradeoffs: faster cycle time may increase automation risk; stricter compliance may add waiting; more parallelism may increase conflict.
   - Preserve control points for high-risk actions: approvals, dual control, human review, rollback, or compensation.
   - Produce a to-be model plus a migration plan: pilot scope, feature flags, fallback path, measurement period, and rollback criteria.

7. Close the BPM loop.
   - Compare as-is and to-be models by expected impact on goals.
   - Update runbooks, workflow code, monitoring, user-facing messages, and ownership records together.
   - Run a small batch of real or replayed process instances through the new model.
   - Review telemetry against the original hypothesis before declaring the redesign successful.
   - Schedule periodic process review when volume, policy, tools, or user expectations change.

## Output Format / Deliverables

Return the smallest set of artifacts needed for the user's stage:
- Process framing: name, trigger, beneficiary, boundaries, instance key, goals, and excluded scope.
- As-is model: steps, roles, handoffs, evidence, variants, waits, exceptions, and current pain points.
- To-be execution model: BPMN-like flow with events, tasks, gateways, lanes/pools, subprocesses, timers, escalations, compensation, and manual fallback.
- Orchestrator contract: task inputs/outputs, owners, systems, permissions, idempotency keys, retries, timeouts, side effects, and event detectors.
- Measurement plan: correlation ids, runtime events, metrics, dashboards or queries, pilot criteria, rollback criteria, and review cadence.

## Failure / Recovery / Idempotency

If evidence is incomplete, start with discovery and instrumentation instead of pretending the process is known. If only policy documents exist, label the model as policy-derived until real instances validate it.

For incremental revisions, preserve stable process names, instance keys, event names, role names, and task ids unless the user explicitly approves a migration. Re-running the skill should update the model from new evidence, not erase prior variants, exceptions, or audit requirements.

When redesign fails or creates regressions, recover by reverting to the previous process version, routing active instances through the documented fallback path, and comparing telemetry against the original hypothesis before retrying automation.

## Hard Rules

- Do not optimize or automate before the process boundary, instance key, owners, and evidence source are explicit.
- Do not model only the happy path when exceptions, waiting, cancellation, escalation, or manual fallback can occur.
- Do not use gateways without testable branch conditions.
- Do not treat a diagram as executable unless tasks, events, owners, evidence, idempotency, and recovery are specified.
- Do not remove approvals, controls, or compliance evidence without naming the risk tradeoff and replacement control.

## Failure Modes

- Drawing BPMN as decoration. A process model must define executable ownership, events, conditions, evidence, and exception paths.
- Modeling only the happy path. Real processes need timers, errors, rework, cancellation, escalation, and manual fallback.
- Confusing task automation with process management. BPM also covers discovery, analysis, redesign, monitoring, governance, and continuous improvement.
- Omitting the process instance key, which makes runtime events impossible to correlate.
- Using gateways without testable conditions, leading to hidden agent judgment and inconsistent routing.
- Ignoring human work. Approvals, review queues, waiting states, due dates, and escalations need first-class representation.
- Optimizing from opinion instead of logs or observed cases.
- Automating a broken process too early, preserving waste at machine speed.
- Treating all variants as exceptions. High-volume variants usually deserve explicit model paths.
- Failing to define compensation for irreversible or externally visible actions.

## Boundaries

Business Process Management is strongest for repeatable operational workflows with observable instances and measurable outcomes. It is weaker for open-ended research, creative exploration, or one-time project plans where the useful path is discovered while doing the work.

BPMN-style notation is useful for coordination and execution semantics, but it is not a substitute for domain policy, access control, legal review, or safety approval. Encode those as process constraints and evidence requirements.

Do not over-model tiny flows. If there is one actor, three steps, no branching, and no need for monitoring, use a checklist or simple state machine.

BPM should be paired with other orchestration methods when needed: use dependency graphs for resource ordering, HTN planning for reusable procedural decompositions, event-driven architecture for integration boundaries, and process mining when event logs are rich enough to infer behavior automatically.

## Source Closure

This 13-business-process-management skill is self-contained for runtime use; its source basis is Business Process Management lifecycle sources and local BPM entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
