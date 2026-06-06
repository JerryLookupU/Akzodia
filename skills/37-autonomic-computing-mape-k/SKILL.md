---
name: 37-autonomic-computing-mape-k
description: Use when designing, auditing, or repairing an auto-orchestrator that should manage itself through a closed control loop: monitoring runtime state, analyzing symptoms and goals, planning changes, executing actions through tools/effectors, and maintaining shared knowledge. Trigger for self-healing, self-optimization, self-configuration, self-protection, adaptive policy control, or MAPE-K loop design in agent runtimes.
source_files:
  - references/source-notes.md
---
# 37 Autonomic Computing / MAPE-K

## Book-Derived Essence

- Core framework: Monitor, Analy

ze, Plan, Execute over shared Knowledge, bounded by goals and policies.
- Deep idea: MAPE-K is not a vague loop; it separates telemetry, diagnosis, decision, action, and knowledge so self-management can be audited.
- Discovery method: Check whether each loop stage has inputs, outputs, ownership, policy, and evidence; missing knowledge or ungoverned execution breaks autonomy.
- Boundary: Do not call a system autonomic if it only alerts humans and cannot execute governed adaptation.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestrator needs explicit self-management rather than one-shot planning:

- The runtime must detect failures, degradation, drift, budget pressure, unsafe behavior, queue buildup, or missing context and respond without waiting for a human operator.
- You need to design a Monitor-Analyze-Plan-Execute loop over agents, tools, tasks, memory, policies, and user goals.
- A workflow has ad hoc retries, alerts, escalations, or tuning rules that should become a coherent control loop.
- You need to separate telemetry, diagnosis, decision policy, action execution, and knowledge state so each part can be tested.
- The orchestrator must support self-healing, self-optimization, self-configuration, or self-protection while respecting high-level administrator or user objectives.
- Multiple agents or managers may act on the same resources and need coordination through shared state, goals, constraints, and effectors.

## Non-Triggers

- Do not trigger for dashboards, logging, tracing, or alerting unless the telemetry feeds autonomous Analyze, Plan, and Execute decisions.
- Do not trigger for generic autonomic-computing history, biological autonomic nervous-system explanations, or lecture summaries.
- Do not trigger when the user only needs a one-shot plan, manual runbook, or simple retry rule with no closed feedback loop.
- Do not trigger for multiagent negotiation, voting, auctions, or communication protocols unless the interaction is part of self-management control over runtime resources.

## Standalone Runtime Contract

This SKILL.md contains the full runtime procedure. Do not read external webpages, original books, source reports, external source snapshots, distilled source material, or files outside this skill directory to execute the skill. `references/source-notes.md` is provenance-only: use it only when the user explicitly asks to audit source lineage, not as an execution dependency.

## Activation And Execution Gate

Before applying this skill, state the activation decision in one sentence. Proceed only if all gate conditions are true:

- There is a managed runtime or orchestrator with resources that can be sensed or controlled.
- The task requires a closed loop containing Monitor, Analyze, Plan, Execute, and shared Knowledge, not merely observation or advice.
- At least one objective, constraint, sensor, and possible effector can be named from the prompt or obtained with a clarifying question.

If any gate condition is missing, ask up to three targeted questions or route to the boundary guidance instead of inventing a MAPE-K design.

## Workflow

1. Define the managed system and the high-level objectives.
   - Name the resources under control: agents, worker pools, tools, prompts, memory indexes, queues, budgets, model routes, sandboxes, external APIs, user sessions, or deployments.
   - Write objectives as policies the loop can evaluate: success criteria, SLOs, budget ceilings, latency targets, safety constraints, evidence requirements, privacy rules, or human approval boundaries.
   - Identify the effectors available to the orchestrator: retry, reroute, pause, cancel, escalate, change model, change retrieval depth, request clarification, roll back, checkpoint, quarantine a tool, or update a policy.

2. Build the knowledge base before wiring the loop.
   - Store current goals, system topology, resource ownership, task state, dependency graph, policy constraints, run history, known incidents, tool contracts, cost models, and action playbooks.
   - Mark which knowledge is static configuration, which is learned from telemetry, and which must be confirmed by a human or trusted system.
   - Include provenance and freshness for telemetry-derived facts so stale observations do not drive fresh actions.

3. Design Monitor as structured sensing, not generic logging.
   - For each objective, define the sensor that can observe progress or violation: metrics, traces, event streams, evaluator scores, user feedback, tool return codes, queue depth, token spend, policy violations, or state transitions.
   - Convert raw events into normalized state facts that Analyze can consume.
   - Add coverage checks for blind spots: missing spans, uninstrumented tools, silent retries, evaluator timeouts, dropped events, and unknown resource states.

4. Design Analyze as diagnosis and prediction.
   - Compare observed state against goals, invariants, baselines, and expected task progress.
   - Classify the condition: healthy, degraded, failing, unsafe, overloaded, drifting, under-specified, blocked, or unknown.
   - Attribute likely causes with evidence: bad retrieval, tool outage, ambiguous user intent, exhausted budget, flaky evaluator, policy conflict, malformed context, load spike, or dependency failure.
   - Estimate urgency, confidence, blast radius, and reversibility before allowing Plan to act.

5. Design Plan as policy-constrained action selection.
   - Generate candidate actions tied to diagnosed causes, not symptoms alone.
   - Score candidates against objectives, cost, latency, safety, reversibility, confidence, and coordination risk.
   - Require a no-op option when evidence is weak, and a human-escalation option when the action is high impact or outside policy.
   - Attach preconditions, expected effects, rollback path, success checks, and action lease or lock requirements to each selected plan.

6. Design Execute as controlled effectors.
   - Apply the plan through explicit effectors with idempotency keys, timeouts, audit events, and permission checks.
   - Use leases, resource locks, or version checks when concurrent managers can modify the same task, tool, or policy.
   - Record every action, input state, decision rationale, and observed result back into knowledge.
   - Verify post-action state through Monitor instead of assuming execution succeeded.

7. Close the loop and tune its cadence.
   - Choose loop timing by risk: event-driven for safety and outages, periodic for optimization, and manual review for irreversible changes.
   - Add dampening to avoid oscillation: cooldowns, hysteresis, backoff, action budgets, and limits on repeated remediations.
   - Define convergence and stop conditions: restored SLO, safe terminal state, human handoff, budget exhausted, confidence too low, or repeated failed remediation.

8. Validate the autonomic design.
   - Run scenario tests for self-healing, self-optimization, self-configuration, and self-protection.
   - Inject missing telemetry, wrong diagnosis, failed effectors, concurrent actions, stale knowledge, and policy conflicts.
   - Check whether the loop preserves high-level goals under stress rather than merely taking action.
   - Promote only loops with inspectable decisions, bounded authority, rollback or containment, and measurable improvement over manual or static policies.

## Failure Modes

- Treating MAPE-K as labels around ordinary logging, alerts, and retries without a real closed feedback loop.
- Monitoring everything but failing to define which state facts drive decisions.
- Planning actions from symptoms without diagnosis, confidence, preconditions, or rollback.
- Allowing Execute to mutate resources without idempotency, permissions, leases, or audit records.
- Storing knowledge as unversioned memory, causing stale facts or old policies to control current actions.
- Optimizing local metrics while violating user goals, safety constraints, budget limits, or global system health.
- Creating multiple autonomic managers that fight over the same resources and produce oscillation.
- Letting the loop take irreversible or high-blast-radius actions without human approval.
- Assuming self-management means full autonomy; mature autonomic systems still expose goals, policy, inspection, and override.

## Output Format And Deliverables

Return the design or audit in this order unless the user requests another format:

1. Activation decision and scope.
2. Managed resources, objectives, sensors, effectors, and shared knowledge.
3. MAPE-K table: Monitor facts, Analyze diagnoses, Plan choices, Execute controls, Knowledge records.
4. Safety controls: permissions, leases, idempotency keys, rollback or containment, and human approval boundaries.
5. Validation plan with stress scenarios, success metrics, stop conditions, and remaining risks.

## Failure, Recovery, And Idempotency

- Treat proposed Execute actions as designs until the user explicitly asks to implement them.
- Make runtime actions repeat-safe with idempotency keys, version checks, leases, bounded retries, and audit records.
- If telemetry, objectives, permissions, or rollback paths are unknown, mark the loop provisional and require instrumentation or policy definition before automation.
- On partial failure, preserve the last known state, action attempt, observed result, and recovery choice in Knowledge before retrying or escalating.
- Re-running this skill should refine or annotate the same loop design, not create a competing manager for the same resources.

## Boundaries

- This skill is for auto-orchestrator control-loop design; it is not a generic summary of autonomic computing history.
- Use cybernetics when the main task is general feedback-control reasoning rather than an implementable MAPE-K architecture.
- Use monitoring and observability when the task is only telemetry, dashboards, traces, or alerting with no autonomous decision loop.
- Use model checking when the core question is proving safety properties across all reachable states.
- Use scheduling or queueing theory when the dominant problem is resource allocation, throughput, or waiting time under load.
- Use actor-model or multiagent-system skills when the main challenge is independent agent communication rather than self-management control.
- Do not use MAPE-K to automate actions whose objectives, permissions, sensors, or rollback paths are not defined.

## Hard Rules

- Never automate irreversible, unsafe, policy-changing, or high-blast-radius actions without an explicit approval boundary.
- Every effector must have preconditions, permission checks, timeout behavior, success checks, and rollback or containment.
- Monitor output must become decision-ready state facts; raw logs alone do not satisfy the Monitor step.
- Analyze must include confidence and evidence; Plan must include a no-op or escalate option when evidence is weak.
- Provenance files are not runtime inputs. `references/source-notes.md` may only be cited as source trace when provenance is requested.

## Source Closure

This 37-autonomic-computing-mape-k skill is self-contained for runtime use; its source basis is Autonomic Computing and MAPE-K sources; local autonomic-computing entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
