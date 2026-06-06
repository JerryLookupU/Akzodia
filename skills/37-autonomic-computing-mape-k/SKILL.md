---
name: 37-autonomic-computing-mape-k
description: Use when designing, auditing, or repairing an auto-orchestrator that should manage itself through a closed control loop: monitoring runtime state, analyzing symptoms and goals, planning changes, executing actions through tools/effectors, and maintaining shared knowledge. Trigger for self-healing, self-optimization, self-configuration, self-protection, adaptive policy control, or MAPE-K loop design in agent runtimes.
---

# Autonomic Computing MAPE-K for Auto-Orchestrators

## When To Use

Use this skill when an orchestrator needs explicit self-management rather than one-shot planning:

- The runtime must detect failures, degradation, drift, budget pressure, unsafe behavior, queue buildup, or missing context and respond without waiting for a human operator.
- You need to design a Monitor-Analyze-Plan-Execute loop over agents, tools, tasks, memory, policies, and user goals.
- A workflow has ad hoc retries, alerts, escalations, or tuning rules that should become a coherent control loop.
- You need to separate telemetry, diagnosis, decision policy, action execution, and knowledge state so each part can be tested.
- The orchestrator must support self-healing, self-optimization, self-configuration, or self-protection while respecting high-level administrator or user objectives.
- Multiple agents or managers may act on the same resources and need coordination through shared state, goals, constraints, and effectors.

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

## Boundaries

- This skill is for auto-orchestrator control-loop design; it is not a generic summary of autonomic computing history.
- Use cybernetics when the main task is general feedback-control reasoning rather than an implementable MAPE-K architecture.
- Use monitoring and observability when the task is only telemetry, dashboards, traces, or alerting with no autonomous decision loop.
- Use model checking when the core question is proving safety properties across all reachable states.
- Use scheduling or queueing theory when the dominant problem is resource allocation, throughput, or waiting time under load.
- Use actor-model or multiagent-system skills when the main challenge is independent agent communication rather than self-management control.
- Do not use MAPE-K to automate actions whose objectives, permissions, sensors, or rollback paths are not defined.
- For provenance, supplemented metadata, and source interpretation, read `references/source-notes.md`.
