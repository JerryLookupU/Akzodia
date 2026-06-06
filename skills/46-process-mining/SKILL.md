---
name: 46-process-mining
description: Use when designing, auditing, or improving an auto-orchestrator from event traces, execution logs, task histories, run graphs, or observed workflow behavior; especially when you need to discover the actual process, compare it with the intended orchestration model, find bottlenecks or variants, or turn historical runs into predictive operational support.
source_files:
  - references/source-notes.md
---
# 46 Process Mining

## Book-Derived Essence

- Core framework: Event log quality, process discovery, conformance checking, performance/resource mining, and improvement loop.
- Deep idea: The essence is evidence-based process repair: actual traces reveal the process model people really execute.
- Discovery method: Validate event schema, discover variants, compare to intended model, locate bottlenecks and deviations, then translate findings into model or instrumentation changes.
- Boundary: Do not infer process truth from logs that omit manual work, queue waits, or failed attempts.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestrator problem is grounded in observed executions rather than only a desired workflow diagram:

- You have logs, traces, spans, event streams, queue histories, agent step records, tickets, or task run metadata.
- You need to infer what process actually happens, not what the design claims should happen.
- You need to compare expected orchestration against real execution and explain deviations.
- You need to improve routing, retries, escalation, handoff, batching, or intervention policies using historical behavior.
- You need operational support: predict late runs, detect stuck cases, recommend next actions, or flag drift.

## Standalone Contract

This `SKILL.md` contains the complete runtime procedure. Do not rely on external books, webpages, source reports, source snapshots, original source paths, or parent-directory materials to execute it. `references/source-notes.md` is provenance-only and may be read only for source trace audits.

Required task inputs are an event source or trace description, case identity, activity vocabulary, timestamp semantics, intended workflow or policy if conformance is requested, target improvement question, and data-quality constraints. If these are missing, ask for the smallest missing item needed to decide whether mining is valid.

## Activation And Execution Gate

Trigger only when historical executions, event logs, traces, spans, run graphs, tickets, or task histories are central evidence for discovering, checking, improving, or operationally supporting an orchestrator process.

Do not trigger for brand-new workflow design with no executions, classroom summaries, formal verification, product analytics without process reconstruction, or one-off log debugging that will not mine case-level behavior.

Before executing the workflow, verify all gate conditions:

- There is observed execution data or a plan to create an event log.
- The data can identify cases, activities, and ordering over time, or the task is explicitly to repair that instrumentation.
- The desired output concerns discovery, conformance, enhancement, bottlenecks, variants, drift, prediction, or intervention.

If the gate fails, state the mismatch and recommend requirements analysis, observability instrumentation, formal verification, or workflow modeling before process mining.

## Workflow

Execute the steps in order. Do not interpret mined patterns before the event-log contract and data-quality checks are explicit.

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

## Output Format And Deliverables

Return a process-mining design or audit with these sections:

- `event_log_contract`: case id, activity, timestamp, lifecycle fields, resources, attributes, ordering semantics, and quality checks.
- `data_quality`: missing data, duplicate events, clock skew, inconsistent names, partial cases, hidden manual work, and readiness verdict.
- `discovery`: common paths, variants, loops, parallel branches, endings, and segment definitions.
- `conformance`: intended model or policy, deviations, classifications, severity, and evidence.
- `enhancement`: bottlenecks, rework loops, handoffs, resource hotspots, decision predictors, and operational-support candidates.
- `orchestrator_changes`: routing, retry, validation, escalation, instrumentation, prediction, or intervention changes with expected metric impact.
- `recheck_plan`: how to rerun mining after changes using the same contract.

For audits, separate facts from interpretations and mark every recommendation with the trace evidence that supports it.

## Failure Modes

- Mining vague logs where `activity` names are free-text, inconsistent, or too coarse to represent decisions.
- Treating the discovered dominant path as the desired process without checking policy, compliance, or user outcomes.
- Ignoring incomplete cases, clock skew, retries, or parallel work, which can produce false bottlenecks and impossible paths.
- Collapsing exceptions into happy-path averages and missing the variants that create most cost or risk.
- Using process mining when there is no event log or when the real issue is a missing goal, unclear policy, or absent orchestration design.
- Adding prediction or automation from historical logs that encode outdated policy, manual workarounds, or biased routing.

## Failure, Recovery, And Idempotency

- If the event log lacks `case_id`, `activity`, or `timestamp`, stop interpretation and return an instrumentation repair plan.
- If data quality is weak but partially usable, constrain conclusions to supported segments and label unsupported claims explicitly.
- If the discovered path conflicts with policy, classify it before recommending changes: valid exception, data artifact, policy violation, stale design, or implementation defect.
- If prediction candidates rely on unstable or biased historical behavior, recommend monitoring or controlled validation before automation.
- Re-running this skill should preserve the case/activity/timestamp contract so before/after comparisons remain valid; change the contract only with a migration note.
- If a mining step cannot be completed, continue with instrumentation and validation recommendations rather than inventing process evidence.

## Boundaries

Process mining helps when historical event data can reveal actual process behavior. It does not replace requirements analysis, causal experimentation, formal verification, or domain judgment.

Use workflow modeling, statecharts, Petri nets, or BPM methods first when the system has no executions yet. Use observability practices first when logs cannot be trusted. Use process mining after the event log can support case-level reconstruction and before making claims about actual throughput, conformance, variants, or operational interventions.

## Hard Rules

- Do not make throughput, conformance, variant, or bottleneck claims without a case/activity/timestamp basis.
- Do not treat the dominant discovered path as desired policy without checking outcomes and constraints.
- Do not flatten retries, cancellations, failures, skipped steps, or repeated activities when they affect interpretation.
- Do not automate predictive interventions from biased, stale, or unvalidated traces.
- Keep runtime execution self-contained in this `SKILL.md`; provenance notes are not required to perform the workflow.

## Source Closure

This 46-process-mining skill is self-contained for runtime use; its source basis is Process Mining sources and local process-mining entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
