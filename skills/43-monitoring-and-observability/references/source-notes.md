# Source Notes

## Manifest Metadata

- Entry id: `43`
- Skill name: `43-monitoring-and-observability`
- Title: `监控与可观测性 / Monitoring and Observability`
- Source files:
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/07_感官_观测信息/43_监控与可观测性__Monitoring_and_Observability/01_sre_google.txt`
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/07_感官_观测信息/43_监控与可观测性__Monitoring_and_Observability/02_sre_google.txt`

## Source Coverage

`01_sre_google.txt` is Google SRE Book Chapter 6, "Monitoring Distributed Systems." It supplies the core alerting philosophy: monitoring definitions, why to monitor, symptoms versus causes, black-box versus white-box monitoring, the four golden signals, tail latency, measurement resolution, simplicity, page-quality questions, and long-term alert health.

`02_sre_google.txt` is Google SRE Workbook Chapter 4, "Monitoring." It supplies implementation guidance: metrics/logs/traces as monitoring sources, speed and calculation requirements, dashboard/interface design, alert severity and suppression, monitoring configuration as code, loose coupling, purposeful metrics, intended-change and dependency telemetry, saturation metrics, and three-tier alert testing.

The two source files are enough to construct a local auto-orchestrator skill. No supplemental external source was required.

## Distilled Principles For Auto-Orchestrators

1. Monitoring is the orchestrator's sensing layer.
   - It must detect whether the orchestrator is keeping its promise: completing useful work, within acceptable latency, without unsafe tool use, runaway spend, stuck queues, or silent wrong results.

2. Page on symptoms or imminent user-visible failure.
   - For an orchestrator, symptoms include failed black-box canary tasks, breached task-completion SLOs, elevated user-impacting error rates, severe latency/queue delay, and near exhaustion of hard resources.
   - Causes include provider errors, tool failures, malformed plans, bad deploys, policy denials, context overflows, retry loops, and dependency incidents. These usually belong in triage dashboards unless they imply imminent failure.

3. Use both black-box and white-box checks.
   - Black-box checks prove the orchestrator can complete representative workflows as a user would experience them.
   - White-box telemetry explains internal behavior: state transitions, planning failures, retries, worker health, dependency latency, tool call classes, budgets, and event stream lag.

4. Apply the four golden signals in orchestrator terms.
   - Latency: end-to-end task time, queue wait, planner/executor/tool/model latency, checkpoint recovery time.
   - Traffic: tasks, steps, model calls, tool calls, event volume, requests per tenant/workflow.
   - Errors: failed tasks, invalid plans, tool errors, policy denials, wrong output, timeout, retry exhaustion.
   - Saturation: workers, queues, concurrency, rate limits, tokens, budget, memory, storage, dependency quota, and predicted exhaustion.

5. Metrics and logs have different jobs.
   - Metrics are for near-real-time alerting, dashboards, SLO burn, trend views, and bounded-cardinality breakdowns.
   - Structured logs and traces are for high-cardinality investigation, request/entity details, prompt/tool summaries, and root-cause reconstruction.
   - Promote data from logs to metrics only when it is bounded and operationally useful.

6. Monitoring itself is production software.
   - Keep monitoring configuration in version control.
   - Test instrumentation, rule evaluation, and alert routing.
   - Keep collection, storage, alerting, and dashboards loosely coupled so components can evolve.

7. Simplicity protects incident response.
   - Alert rules should be understandable during a page.
   - Remove metrics and alerts that are unused, rarely exercised, or not connected to an operational decision.
   - Avoid complex dependency hierarchies except for stable and clearly understood conditions such as drained traffic or maintenance windows.

8. Dashboards should answer questions, not create surveillance work.
   - Landing dashboards answer whether the orchestrator is healthy now.
   - Triage dashboards explain where failures cluster.
   - Trend dashboards support capacity planning and long-term reliability work.

9. Rote pages are design bugs.
   - If the human response is predictable and scriptable, automate it or demote the page while preserving a long-term fix path.
   - Track alert load as a reliability signal for the team and the orchestrator.

## Practical Design Checklist

- What user-visible promise should monitoring protect?
- What are the orchestrator's SLIs and SLOs?
- Which golden signals are collected, at what labels and resolution?
- Which signals are black-box symptoms and which are white-box causes?
- Which events need metrics, logs, traces, or all three?
- Which deploy/config/model/tool versions appear on dashboards?
- Which dependency signals are collected uniformly through shared libraries or wrappers?
- Which alerts are page-worthy, ticket-worthy, or dashboard-only?
- How are duplicate, dependency-caused, drained-traffic, and test-traffic alerts suppressed?
- How is suppression cleared?
- How are instrumentation, rule evaluation, and alert routing tested?
- Which metrics or alerts are candidates for deletion because nobody uses them?

## Anti-Patterns To Catch During Review

- Alerting because "something seems weird."
- Alerting on every node, worker, or task when a global symptom would identify the incident once.
- Relying on mean latency for user experience.
- Labeling metrics with tenant IDs, run IDs, prompt IDs, or entity IDs without a cardinality plan.
- Requiring operators to inspect CI/CD logs to correlate outages with deploys.
- Keeping alerts that fire quarterly or less without any synthetic test.
- Suppressing dependency or maintenance alerts without an explicit recovery condition.
- Using email alerts as a dumping ground for unactionable information.
