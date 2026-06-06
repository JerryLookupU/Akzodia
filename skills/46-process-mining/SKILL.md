---
name: 46-process-mining
description: Use when designing, auditing, or improving an auto-orchestrator from event traces, execution logs, task histories, run graphs, or observed workflow behavior; especially when you need to discover the actual process, compare it with the intended orchestration model, find bottlenecks or variants, or turn historical runs into predictive operational support.
---

# Process Mining

## When To Use

Use this skill when the orchestrator problem is grounded in observed executions rather than only a desired workflow diagram:

- You have logs, traces, spans, event streams, queue histories, agent step records, tickets, or task run metadata.
- You need to infer what process actually happens, not what the design claims should happen.
- You need to compare expected orchestration against real execution and explain deviations.
- You need to improve routing, retries, escalation, handoff, batching, or intervention policies using historical behavior.
- You need operational support: predict late runs, detect stuck cases, recommend next actions, or flag drift.

## Workflow

1. Define the case, activity, and timestamp contract.
   - Case: the unit whose lifecycle is being orchestrated, such as a user request, order, incident, research job, or agent task.
   - Activity: the named state transition or work step, such as classify, retrieve, call tool, validate, retry, escalate, approve, or deliver.
   - Timestamp: the event ordering basis. Record start/end timestamps when duration, wait time, or concurrency matter.
   - Add resources and attributes when they affect decisions: agent id, tool name, tenant, priority, error code, data source, cost, token use, approval state, queue, or model.

2. Build an event log fit for mining.
   - Require at minimum `case_id`, `activity`, and `timestamp`.
   - Preserve ordering, repeated activities, skipped activities, cancellations, retries, and failures instead of flattening them away.
   - Separate lifecycle events when useful: scheduled, started, completed, failed, retried, timed out, cancelled.
   - Check data quality before interpreting results: missing timestamps, duplicated events, clock skew, inconsistent activity names, partial cases, merged cases, and hidden manual steps.

3. Discover the real process.
   - Produce a compact process model from traces: common paths, loops, parallel branches, optional steps, and endings.
   - Segment variants before overgeneralizing: successful vs failed, short vs long, automated vs human-intervened, high-cost vs low-cost, tenant or product differences.
   - Treat discovered models as evidence maps, not policy. A frequent path may still be undesirable.

4. Check conformance against the intended orchestrator.
   - Compare the discovered traces with the designed workflow, state machine, runbook, BPMN/Petri-net-style model, or policy specification.
   - Identify deviations: missing required steps, unexpected jumps, illegal retries, bypassed approvals, duplicate work, stranded cases, and dead paths.
   - Explain each deviation as one of: valid exception, data artifact, policy violation, stale design, or implementation defect.

5. Mine performance, organization, and decision perspectives.
   - Performance: cycle time, wait time, service time, queue buildup, bottlenecks, rework, SLA breach points.
   - Organization/resource: handoffs, overloaded agents, tool hotspots, ownership ambiguity, manual intervention patterns.
   - Decision: which attributes predict branch choice, retry, escalation, failure, or long duration.

6. Convert findings into orchestrator changes.
   - For bottlenecks: add capacity, parallelize, prefetch, split queues, or move checks earlier.
   - For rework loops: add better validation gates, idempotency, clearer failure classes, or bounded retry policies.
   - For conformance violations: update policy, tighten guards, add audit events, or align implementation with the intended model.
   - For high-variance paths: introduce routing rules, specialized subflows, or human-review thresholds.
   - For operational support: add predictions and interventions only when the event log has stable leading indicators.

7. Close the loop.
   - Instrument any missing events before making strong claims.
   - Re-run mining after changes using the same case/activity/timestamp contract.
   - Track whether the changed orchestrator improved the target metric without increasing hidden rework, risk, or manual load.

## Failure Modes

- Mining vague logs where `activity` names are free-text, inconsistent, or too coarse to represent decisions.
- Treating the discovered dominant path as the desired process without checking policy, compliance, or user outcomes.
- Ignoring incomplete cases, clock skew, retries, or parallel work, which can produce false bottlenecks and impossible paths.
- Collapsing exceptions into happy-path averages and missing the variants that create most cost or risk.
- Using process mining when there is no event log or when the real issue is a missing goal, unclear policy, or absent orchestration design.
- Adding prediction or automation from historical logs that encode outdated policy, manual workarounds, or biased routing.

## Boundaries

Process mining helps when historical event data can reveal actual process behavior. It does not replace requirements analysis, causal experimentation, formal verification, or domain judgment.

Use workflow modeling, statecharts, Petri nets, or BPM methods first when the system has no executions yet. Use observability practices first when logs cannot be trusted. Use process mining after the event log can support case-level reconstruction and before making claims about actual throughput, conformance, variants, or operational interventions.
