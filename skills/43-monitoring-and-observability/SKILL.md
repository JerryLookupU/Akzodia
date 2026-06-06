---
name: 43-monitoring-and-observability
description: Use when designing, reviewing, or repairing auto-orchestrator monitoring: telemetry contracts, dashboards, alert rules, SLO/SLI signals, black-box and white-box probes, log-vs-metric choices, alert suppression, and tests that prove the orchestrator can detect user-impacting failures without noisy pages.
---

# Monitoring and Observability

## When To Use

Use this skill when an auto-orchestrator needs a sensing layer: deciding what to measure, how to expose run health, what should page a human, what should be routed to tickets or dashboards, and how to validate that alerting still works.

Use it for agent runtimes, workflow engines, planner-executor systems, tool-calling services, evaluation harnesses, and distributed automation where failures may appear as bad outputs, stuck runs, retry storms, budget exhaustion, queue buildup, stale state, dependency failures, or silent degradation.

Read `references/source-notes.md` when you need the source rationale, source-file mapping, or a reminder of the SRE monitoring principles behind this workflow.

## Workflow

1. Define the monitored surface from the user's point of view.
   - Name the orchestration product promise: successful task completion, bounded latency, correct tool execution, safe budget use, or reliable handoff.
   - Separate symptoms from causes. Page on symptoms or imminent real failures; use cause-oriented telemetry for triage.
   - Identify the primary consumers: on-call engineer, orchestrator operator, product owner, evaluator, or end user.

2. Establish the four golden signals for the orchestrator.
   - Latency: queue wait, plan time, tool-call time, end-to-end run time, checkpoint restore time, and separate latency for failed runs.
   - Traffic: runs started, steps executed, tool calls, model calls, event volume, per-tenant/request-class demand.
   - Errors: failed runs, invalid plans, tool errors, policy denials, malformed outputs, retry exhaustion, SLO-impacting wrong-result reports.
   - Saturation: worker capacity, queue depth, concurrency slots, rate limits, budget remaining, memory, disk, token limits, context size, dependency quota, and predicted exhaustion.

3. Choose black-box and white-box checks.
   - Black-box: synthetic tasks, public API health, canary workflows, externally visible completion and correctness probes. Prefer these for paging because they represent real symptoms.
   - White-box: internal state transitions, planner confidence, retry counters, event stream lag, tool-specific errors, dependency status, cache hit rates, and model/provider responses. Use these to diagnose and to detect imminent failures.
   - For multilayer systems, state whether a signal is a symptom for this layer or a cause for a downstream layer.

4. Design metrics and logs with purpose.
   - Use metrics for real-time alerts, dashboards, SLO burn, trend detection, and bounded-cardinality breakdowns.
   - Use structured logs or traces for high-cardinality investigation, entity IDs, prompts, tool payload summaries, run timelines, and root-cause drill-down.
   - Promote a log field to a metric label only when the cardinality is bounded and the label will change an alert, dashboard, or diagnosis path.
   - Treat monitoring configuration as code. Keep collection, storage, alerting, and dashboarding loosely coupled behind stable interfaces.

5. Build dashboards that answer operational questions.
   - Landing dashboard: SLO/SLI status, current incidents, golden signals, recent deploy/config/model versions, dependency health, and saturation forecasts.
   - Triage dashboard: run breakdowns by tenant, workflow type, model, tool, response code, error class, retry reason, and deploy/config version.
   - Trend dashboard: growth, cost, token/budget use, queue load, capacity, and recurring failure classes.
   - Avoid dashboards that require someone to stare at a screen; dashboards support investigation and subcritical review.

6. Write alert rules with a page-quality gate.
   - An alert is page-worthy only if it detects an otherwise undetected condition that is urgent, actionable, actively or imminently user-visible, and not already paging another owner.
   - Prefer alerts tied to SLO burn, failed black-box canaries, severe golden-signal changes, and hard-resource exhaustion.
   - Route non-urgent or non-actionable findings to tickets, dashboards, postmortem follow-ups, or automation backlogs.
   - Suppress duplicate alerts for shared causes, drained/test traffic, known maintenance windows, and dependency incidents, but define how suppression clears.

7. Tune resolution, aggregation, and tail visibility.
   - Match measurement frequency to the decision it supports. Incident response needs fresh data; planning can tolerate slower data.
   - Track distributions or histograms for latency and queue wait; do not rely on averages where tail behavior matters.
   - Measure saturation with thresholds below 100% when systems degrade before full utilization.
   - Keep rarely used or orphaned signals eligible for removal.

8. Test the monitoring path.
   - Binary reporting: prove instrumentation changes under expected orchestrator events.
   - Monitoring rules: feed synthetic time series or a controlled test service and assert derived series and alert states.
   - Alert routing: verify severity, labels, deduplication, suppression, destination, and runbook links.
   - Include tests for stale telemetry, missing labels, dependency failure, canary failure, high-cardinality rejection, and alert recovery.

9. Close the learning loop.
   - After each incident, ask which metric, log field, trace, dashboard, or alert would have reduced diagnosis time.
   - If a page has a rote response, automate the response or demote the page while scheduling the real fix.
   - Review alert volume and incident load periodically; excessive paging is itself an orchestrator reliability problem.

## Failure Modes

- Paging on causes instead of symptoms, producing noise when users are not affected.
- Exporting metrics because they are easy, without a clear alert, dashboard, planning, or debugging purpose.
- Depending on averages while tail latency, queue wait, or retry storms hurt users.
- Using high-cardinality identifiers as metric labels, making the monitoring system expensive or unusable.
- Hiding incidents through stale suppression rules, drained-traffic filters, or untested alert routing.
- Creating a monitoring stack so complex that operators cannot reason about pages during incidents.
- Treating logs as the only alert source when a bounded metric counter would make alerts consistent and manageable.
- Letting rote human responses persist as pages instead of automation candidates.

## Boundaries

This skill designs the sensing and alerting layer for auto-orchestrators. It does not replace SLO engineering, incident response, postmortem practice, security audit logging, tracing implementation details, or vendor-specific observability setup.

Do not use it for generic product analytics, business intelligence, or one-off debugging unless the task changes the orchestrator's durable monitoring design.

Do not require perfect root-cause detection before paging. A good page identifies real or imminent user impact and gives enough context for fast triage; root-cause telemetry can live in dashboards, logs, traces, and runbooks.
