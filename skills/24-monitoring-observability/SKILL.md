---
name: 24-monitoring-observability
description: Use when designing, reviewing, or debugging observability for an auto-orchestrator, including telemetry coverage, metrics/logs/traces, dashboards, alert rules, paging policy, SLO-linked signals, incident triage views, or monitoring maintainability. Trigger for questions about what to measure, when to page a human, how to distinguish symptoms from causes, and how to make orchestrator runs replayable and diagnosable.
---

# Monitoring / Observability for Auto-Orchestrators

## When To Use

Use this skill when the work involves an auto-orchestrator's production visibility:

- Designing telemetry for agent runs, tool calls, routing decisions, retries, queues, budgets, sandbox policy, or external dependencies.
- Deciding which signals should page a human versus appear on dashboards, tickets, reports, or postmortem evidence.
- Reviewing whether metrics, logs, traces, and replay records are sufficient to answer "what broke?" and "why did it break?"
- Simplifying noisy alerting or dashboard sprawl into a smaller, more actionable monitoring model.
- Adding validation for alert rules, metric emission, notification routing, or observability configuration.

## Workflow

1. Start from user impact and SLOs.
   - Name the orchestrator outcomes users depend on: task success, latency to useful result, budget compliance, safety policy enforcement, data isolation, and recovery from failed tools.
   - Define the symptom-level signals first: user-visible failure rate, timeout rate, stale/blocked run rate, wrong-route rate, budget exhaustion rate, and queue delay.
   - Keep paging tied to active or imminent user impact. Non-urgent anomalies belong in dashboards, tickets, or scheduled review.

2. Cover the four golden signals for the orchestrator.
   - Latency: end-to-end run duration, step/tool latency, queue wait, model response latency, replay/recovery latency. Separate successful and failed latency.
   - Traffic: runs started/completed, step counts, tool calls, model calls, dependency calls, concurrent runs, tenant/API-user slices.
   - Errors: failed runs, tool errors, policy denials, invalid outputs, retry exhaustion, schema violations, dependency status classes, and SLO-impacting errors.
   - Saturation: queue depth, worker capacity, token/budget pressure, rate-limit headroom, file/socket/thread/goroutine usage, storage growth, and dependency quotas.

3. Separate symptoms from causes.
   - Page on symptoms: the orchestrator is slow, failing, stuck, unsafe, or unable to complete useful work.
   - Collect cause-oriented data for triage: model/provider versions, prompt/config versions, routing decisions, selected tools, dependency responses, rollout markers, host/resource metrics, and sandbox/policy decisions.
   - Avoid dependency-heavy alert trees unless the dependency relationship is stable and the rule stays easy for every on-call owner to understand.

4. Choose telemetry sources by use case.
   - Metrics for alerting, dashboards, SLO burn, capacity planning, and low-cardinality breakdowns.
   - Structured logs for high-cardinality details, exact failure context, tenant/run/entity identifiers, and root-cause investigation.
   - Traces or replay records for causal chains across model calls, tool calls, retries, and human handoff.
   - Keep high-cardinality fields out of metric labels unless bounded and operationally useful.

5. Design dashboards for action.
   - Put SLI/SLO health and active incidents on the landing view.
   - Add drill-downs for recent intended changes: binary version, prompt version, config version, model/provider version, policy version, and rollout timestamp.
   - Show dependencies with request count, latency, response code/error class, quota/rate-limit headroom, and saturation.
   - Use consistent labels and views across orchestrator components so another team can debug without relearning the dashboard grammar.

6. Gate every page with alert-quality questions.
   - Does this detect an otherwise undetected urgent, actionable, active or imminent user-visible problem?
   - Can the on-call owner take a meaningful action now?
   - Would this ever be safely ignored? If yes, filter or downgrade it.
   - Is another alert already paging someone for the same incident?
   - If the response is rote and scriptable, automate it or convert the page into a lower-severity workflow while the root cause is prioritized.

7. Keep monitoring maintainable.
   - Treat monitoring configuration as code with review, linting, rollback, and ownership.
   - Remove unused metrics, stale dashboards, and alert rules that rarely fire and do not support diagnosis.
   - Prefer simple, robust alert rules over "magic" causal inference.
   - Keep collection, storage, alerting, dashboarding, and analysis loosely coupled behind stable interfaces.

8. Test the observability path.
   - Verify instrumentation changes metric values under known conditions.
   - Test rule evaluation with synthetic time series or a controlled canary service.
   - Test alert routing and labels so notifications reach the right destination with enough context.
   - Include observability gaps in postmortems: ask which metric, log field, trace span, replay record, or dashboard would have shortened diagnosis.

## Failure Modes

- Paging on causes while missing symptoms, producing alerts for weird internal states that users never experience.
- Treating logs as the primary alerting path when a bounded counter metric would be faster and easier to manage.
- Exporting easy metrics without a purpose, then paying for storage and dashboard noise.
- Using averages for latency or resource use while tail latency, queue spikes, or per-worker saturation hides the actual failure.
- Adding unbounded labels such as run IDs, tenant IDs, entity IDs, prompts, or file paths to metrics.
- Building complex dependency suppression rules that nobody can reason about during an incident.
- Letting human responders perform rote remediation instead of automating the loop or prioritizing the underlying fix.

## Boundaries

- This skill designs observability strategy and review criteria; it does not choose a vendor or prescribe a specific stack.
- It emphasizes production reliability for auto-orchestrators, not business analytics, security audit logging, or compliance retention except where they affect reliability diagnosis.
- It does not replace SLO design, incident response, postmortem practice, or distributed tracing implementation details; use those as separate skills when they are the main task.
- Prefer source-specific details in `references/source-notes.md` when you need the distilled rationale behind these rules.
