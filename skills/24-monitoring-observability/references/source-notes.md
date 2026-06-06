# Source Notes

## Manifest Item

- id: 24
- title: 可观测性 / Monitoring / Observability
- skillName: 24-monitoring-observability
- source set: Google SRE monitoring material from the SRE book and SRE workbook.

## Distilled Principles

The source material frames monitoring as collecting, processing, aggregating, and displaying real-time quantitative data about a system. It distinguishes white-box monitoring from black-box monitoring, and stresses that an effective monitoring system answers two questions: what is broken, and why it is broken.

For auto-orchestrator design, "what is broken" should map to user-visible run outcomes: failed tasks, slow completion, blocked queues, bad routing, unsafe or policy-denied execution, exhausted budget, or inability to recover. "Why" should map to cause-oriented evidence: tool failures, provider changes, prompt/config versions, dependency responses, resource saturation, rollout events, and decision traces.

The four golden signals are the core coverage model:

- Latency: successful and failed request latency must be separated. For orchestrators, track end-to-end run duration and per-step/tool/model latency, with tail percentiles.
- Traffic: demand should be measured in domain terms. For orchestrators, track runs, steps, model calls, tool calls, dependency calls, queue load, and concurrency.
- Errors: failures may be explicit, implicit, or policy-defined. For orchestrators, include failed runs, invalid outputs, tool errors, retry exhaustion, policy denials, and SLO-impacting partial failures.
- Saturation: measure the constrained resource and impending exhaustion. For orchestrators, include queue depth, worker capacity, rate limits, token/budget pressure, storage growth, and dependency quota headroom.

The source warns against paging humans because something is merely unusual. Paging is expensive and creates fatigue. A page should represent an urgent, actionable, active or imminent user-visible problem. Alerts that can be ignored, alerts with rote responses, and duplicate alerts should be filtered, downgraded, automated, or removed.

The source favors simple and comprehensible critical-path monitoring. Complex dependency hierarchies and magical causal inference tend to become fragile, especially in systems that are continuously refactored. Cause-oriented data remains valuable, but mainly as triage and debugging support after symptom-level alerting fires.

Metrics and logs serve different purposes. Metrics are near-real-time and fit dashboards, alerting, SLO burn, and bounded breakdowns. Structured logs are more granular and better for exact root-cause investigation, high-cardinality identifiers, and detailed reports. A useful pattern is to export a bounded metric for alerting while keeping exact context in logs or traces.

Dashboards should be designed around their audience and should expose SLI/SLO status prominently. For incident diagnosis, dashboards should surface recent intended changes: binary versions, command-line flags, dynamic configuration, prompt/model/provider versions, policy versions, and rollout timestamps. Dependency dashboards should show request and response size, latency, response code/error class, peer/method labels, and saturation.

Monitoring configuration should be treated as code. Review, rollback, linting, and consistent frameworks reduce operational confusion. The monitoring system should be loosely coupled: separate collection, storage, alerting, and visualization behind stable interfaces where possible.

Alerting logic should be tested. The source recommends testing metric emission, rule evaluation, and alert routing. For orchestrators, this implies synthetic runs that exercise success, failure, timeout, policy denial, dependency degradation, and saturation cases.

## Auto-Orchestrator Translation

Apply the source material by designing an observability path for each orchestrator lifecycle stage:

1. Intake: request accepted, tenant/API-user context, budget, policy envelope, and initial queue state.
2. Planning/routing: selected model, prompt version, planner route, tool policy, and expected constraints.
3. Execution: step latency, tool calls, retries, dependency responses, sandbox/file effects, and resource use.
4. Recovery: retry reasons, fallback path, human handoff, replay availability, and final status.
5. Review: SLO impact, incident correlation, postmortem gaps, and long-term trend signals.

Do not require every detail to become a metric. Use metrics for bounded operational questions and logs/traces/replay records for high-cardinality or causal details.

## Source Files

- `auto_orchestrator_theory_txt_pack_v2/原文目录/04_左脚_跟踪记录回放/24_可观测性__Monitoring_Observability/01_sre_google.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/04_左脚_跟踪记录回放/24_可观测性__Monitoring_Observability/02_sre_google.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/04_左脚_跟踪记录回放/24_可观测性__Monitoring_Observability/03_sre_google.txt`

## Metadata Supplement

The manifest provided enough metadata to build the skill. Source identity was supplemented from the source file headers:

- Google SRE book, Chapter 6, "Monitoring Distributed Systems", written by Rob Ewaschuk and edited by Betsy Beyer.
- Google SRE workbook, Chapter 4, "Monitoring", by Jess Frame, Anthony Lenton, Steven Thurgood, Anton Tolchanov, Nejc Trdin, with Carmela Quinito.
- Table of contents source confirms chapter placement and publication/license context.
