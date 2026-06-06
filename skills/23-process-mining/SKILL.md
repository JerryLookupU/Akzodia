---
name: 23-process-mining
description: Use when designing or improving an auto-orchestrator from execution event logs: discover actual task flows, compare observed traces with intended plans, detect bottlenecks, rework, deviations, and failure patterns, then turn runtime evidence into better workflow templates, conformance checks, monitoring, and recovery rules.
source_files:
  - references/source-notes.md
---
# 23 Process Mining

## Book-Derived Essence

- Core framework: Event log -> discovery -> conformance -> enhancement. The real process is reconstructed from traces.
- Deep idea: Process mining prevents process theater: it compares designed flow with observed behavior and exposes variants, bottlenecks, and deviations.
- Discovery method: Validate case id, activity, timestamp, actor, and lifecycle fields; discover variants, align them to the model, then mine performance and resource perspectives.
- Boundary: Do not mine logs that lack stable case identity or trustworthy timestamps without first repairing instrumentation.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestrator has event logs, traces, tickets, audit records, tool-call histories, or replayable runs and the design question is: "What process is actually happening?"

Strong triggers:
- You need to infer real task paths from logs instead of relying on declared workflow diagrams or anecdotes.
- You need to compare observed execution with a planned process, policy, runbook, BPMN model, state machine, or task template.
- You need evidence for bottlenecks, repeated failures, hidden handoffs, retries, rework loops, skipped steps, or unexpected variants.
- You are designing telemetry for future process mining: event ids, trace ids, activity names, timestamps, actors, tool calls, states, outcomes, and artifact references.
- You want to convert successful or frequent traces into reusable orchestration templates.
- You need runtime support signals such as predicted delay, likely failure point, next best action, or case escalation.

Prefer ordinary observability when the user only needs current health metrics or logs for one incident. Prefer BPM when the process model is being designed from policy and stakeholder intent before enough event data exists.

## Activation Gate

Activate only when the task uses event logs, traces, audit records, tickets, tool-call histories, or replayable runs to discover actual process behavior, check conformance, mine performance/reliability signals, or design instrumentation for future mining. Do not activate for policy-only process design, a single stack trace, generic education, or live health monitoring without process reconstruction.

Before executing, identify the mining question, process instance key, event fields available, analysis population/window, and intended model if conformance is requested. If a stable case id or activity semantics are missing, gate execution on an event-quality finding before producing process conclusions.

## Standalone Contract

This skill must be usable from this `SKILL.md` alone. `references/source-notes.md` is provenance/source trace only; do not load it or any external source file for runtime execution. Answers must provide enough event-log, conformance, and improvement detail for another agent to audit the findings independently.

## Output Format

Return an evidence-first process-mining report with:
- Activation decision: why Process Mining is active and which nearby skills were ruled out.
- Data contract: case id, activity, timestamp, lifecycle/outcome, included/excluded cases, quality caveats, and sanitization notes.
- Discovered behavior: variants, counts, success rates, latency/rework/failure measures, and representative trace ids or evidence links.
- Conformance and bottlenecks: deviations, severity, frequency, impact, uncertainty, and whether each is defect, useful variant, or unknown.
- Design feedback: workflow template changes, guards, retries, monitoring, instrumentation gaps, and validation checks for the next release.

## Failure, Recovery, and Idempotency

If event quality is insufficient, return an instrumentation and quarantine plan instead of over-interpreting traces. If causality is uncertain, label findings as correlation and propose replay, sampling, controlled rollout, or domain review. On re-run, keep activity normalization, case filters, variant ids, and comparison windows stable unless the user changes the analysis scope.

## Hard Rules

- Do not mine across cases without a stable process instance key or an explicit limited fallback.
- Do not treat free-text log lines as activities until names and lifecycle semantics are normalized.
- Do not call every deviation a defect; classify useful variants and uncertain cases separately.
- Do not expose sensitive trace data beyond the minimum needed evidence.

## Workflow

1. Define the mining question.
   - Choose one primary question: discover actual flow, check conformance, find bottlenecks, identify variants, explain failures, or generate reusable templates.
   - Name the process instance key: `trace_id`, task id, case id, run id, workflow id, ticket id, customer id, or artifact id.
   - State the expected model if one exists: planned steps, allowed ordering, required approvals, timeout rules, recovery paths, and terminal states.
   - Set the analysis window and population: all runs, failed runs, high-latency runs, high-value users, specific tools, or a release period.

2. Build a process-mining event log.
   - Require at minimum: `case_id`, `activity`, `timestamp`, and `lifecycle` or outcome.
   - Add orchestrator-specific fields when available: `event_id`, `agent_id`, `tool_name`, `input_ref`, `output_ref`, `state_snapshot`, `decision_reason`, `retry_count`, `error_class`, `cost`, and `model_version`.
   - Normalize activity names so the same action is not split across aliases such as `fetch_url`, `web_fetch`, and `download_page`.
   - Preserve raw evidence links so any discovered path can be replayed or audited.
   - Reject or quarantine traces with missing case ids, impossible timestamps, duplicate event ids, or ambiguous activity boundaries.

3. Discover the actual process.
   - Sort each case into a trace of activities with timestamps and outcomes.
   - Group traces into variants by ordered activities and by meaningful attributes such as actor, tool, customer segment, route, or failure class.
   - Identify the dominant happy path, high-volume alternate paths, exception paths, and rare but expensive paths.
   - Create a compact model: start events, activities, gateways, loops, handoffs, waiting states, exceptions, compensations, and end states.
   - Keep discovered variants separate until there is evidence that they are semantically the same process.

4. Check conformance against the intended model.
   - For each trace, compare observed steps with required, optional, forbidden, and ordered steps.
   - Classify deviations: skipped guard, unauthorized tool, extra review, missing approval, late retry, out-of-order action, premature completion, or unhandled exception.
   - Distinguish productive deviations from defects. Some variants reveal a better path; others reveal policy or implementation failure.
   - Emit conformance findings as testable rules the orchestrator can enforce or monitor.
   - When conformance is uncertain, return to event semantics before changing the workflow.

5. Mine performance and reliability signals.
   - Measure cycle time, processing time, waiting time, queue time, handoff delay, retry delay, and time-to-recovery by activity and variant.
   - Locate bottlenecks by combining duration, volume, failure rate, rework frequency, and downstream impact.
   - Detect rework loops, retry storms, repeated tool failures, approval stalls, user-wait states, and low-value checks.
   - Compare failed traces to successful traces to isolate discriminating activities, missing evidence, unstable inputs, or risky branches.
   - Produce prioritized improvement candidates with the exact log evidence that supports them.

6. Feed findings back into orchestrator design.
   - Convert frequent successful variants into reusable workflow templates or HTN methods.
   - Convert frequent failures into preflight checks, guards, fallback paths, retry policies, compensation rules, or escalation triggers.
   - Convert bottlenecks into scheduling, batching, parallelization, cache, ownership, or tool-selection changes.
   - Add missing instrumentation where the log could not answer a design question.
   - Define follow-up conformance checks so the next release proves whether the redesign changed real behavior.

7. Report in an evidence-first format.
   - Include the mined question, data window, included cases, excluded cases, and event quality caveats.
   - Show top variants with counts, success rates, median and tail latency, and representative trace ids.
   - List deviations and bottlenecks with severity, frequency, impact, and proposed orchestrator change.
   - Separate facts from inferences. Do not claim causality from process-mining correlations without a validation step.

## Failure Modes

- Mining logs without a stable process instance key, causing events from different cases to be mixed.
- Treating raw log messages as activities without normalizing names and lifecycle semantics.
- Optimizing the most visible trace instead of the highest-volume or highest-impact variant.
- Forcing all variants into one ideal flow before understanding why the variants exist.
- Calling every deviation a bug. Some deviations are workarounds that reveal missing model paths.
- Ignoring event quality: missing timestamps, clock skew, duplicate events, retries that look like new cases, or hidden human work.
- Producing a process diagram without actionable changes to templates, checks, monitoring, or recovery behavior.
- Inferring root cause from correlation alone without replay, sampling, controlled rollout, or domain review.

## Boundaries

Process mining is strongest when event logs are rich enough to reconstruct per-case execution. It is weak when the system lacks correlation ids, has sparse logging, or performs important work outside observable systems.

This skill does not replace process design. Use it to learn from actual traces, then pair it with BPM, workflow management, state machines, scheduling, or reliability engineering to implement changes.

Do not use process mining as surveillance theater. For human-in-the-loop orchestrators, minimize unnecessary personal data and focus on workflow evidence, role-level handoffs, and system behavior.

When logs contain regulated, customer-sensitive, or security-sensitive data, sanitize before analysis and keep trace examples minimal.

## Source Closure

This 23-process-mining skill is self-contained for runtime use; its source basis is Process Mining sources and local process-mining entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
