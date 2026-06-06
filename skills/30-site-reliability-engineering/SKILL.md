---
name: 30-site-reliability-engineering
description: Use when designing or reviewing production reliability for an auto-orchestrator, agent platform, workflow engine, tool gateway, or long-running run service. Trigger for SLOs, SLIs, error budgets, toil reduction, monitoring signals, alert quality, incident response, postmortems, launch readiness, overload handling, operational ownership, and reliability tradeoffs between velocity and user-visible availability.
source_files:
  - references/source-notes.md
---
# 30 Site Reliability Engineering

## Book-Derived Essence

- Core framework: SLI, SLO, error budget, toil reduction, incident response, overload handling, and launch readiness.
- Deep idea: SRE’s sharpest idea is the error budget: reliability becomes an explicit product tradeoff, not an infinite aspiration.
- Discovery method: Define user-visible SLIs, set SLOs, compute budget burn, identify toil, rehearse incidents, and gate launches against reliability evidence.
- Boundary: Do not turn SRE into generic ops hygiene; the method needs user-facing reliability measures and budget decisions.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when reliability must become an explicit operating contract, not an afterthought:

- A planner, scheduler, worker pool, tool gateway, memory store, queue, or artifact service is becoming production-critical.
- Users, tenants, or downstream systems need a clear expectation for run availability, correctness, freshness, latency, or completion.
- The team is debating whether to ship faster, pause launches, shed load, add redundancy, or pay down reliability risk.
- Alerts are noisy, missing user-impacting failures, or tied to machine symptoms without service-level meaning.
- Operators spend recurring effort on manual retries, stuck-run cleanup, paging triage, capacity babysitting, or release babysitting.
- Incidents recur because postmortems do not turn into system, process, test, or ownership changes.
- A launch, migration, model/tool rollout, or orchestration feature needs production readiness gates.

Do not trigger for low-level protocol design, checkpoint storage formats, raw exporter implementation, generic incident communications, or prototypes with no user-visible reliability obligation.

## Standalone Contract

This skill must provide production reliability guidance without requiring source files. Do not load or depend on external files, webpages, original books, source reports, external source folders, or source-pack material at runtime. `references/source-notes.md` is optional local provenance only and is not required for execution.

The expected result is an SRE operating decision: reliability surface, user promise, SLIs, SLOs, error budget policy, toil plan, monitoring/page rules, degradation behavior, incident process, postmortem actions, launch gates, and review cadence.

## Activation And Execution Gate

Activate only when all of these are true:
- The service has production, customer, tenant, or downstream reliability obligations.
- The task concerns SLOs, SLIs, error budgets, alert quality, toil, incidents, launch readiness, overload, ownership, or reliability tradeoffs.
- The deliverable can tie metrics and operations to user-visible impact.

Before proposing SLOs or alerts, identify:
- The service boundary and user-visible promise.
- Eligible traffic, measurement window, exclusions, and owner for budget decisions.
- Which symptoms require immediate human action and which belong in tickets, dashboards, or automation.

If these are unknown, define assumptions and ask for the missing operating contract before setting targets.

## Workflow

1. Name the service and the user promise.
   - Define the reliability surface: orchestration API, run admission, plan generation, task scheduling, tool execution, memory persistence, artifact delivery, callback delivery, or end-to-end run completion.
   - State the user-visible promise in plain language before choosing metrics.
   - Separate availability, latency, freshness, durability, correctness, and safety; do not compress them into one vague "uptime" target.

2. Choose SLIs that track user experience.
   - Prefer request success rate, run completion rate, time-to-first-useful-output, time-to-terminal-state, queue age, stuck-run rate, duplicate side-effect rate, data-loss rate, and tenant-isolation violation count.
   - Measure at meaningful boundaries: client request, accepted run, scheduled step, tool call, checkpoint write, final commit, callback, and artifact read.
   - Exclude synthetic health checks from the primary SLI unless they are proven to predict user-visible failure.

3. Set SLOs and an error budget.
   - Pick targets that are good enough for the product contract and economically defensible, not simply the highest number that sounds responsible.
   - Define the measurement window, eligible traffic, exclusions, burn calculation, and owner who can spend or defend the budget.
   - Convert budget burn into decisions: normal release pace, feature freeze, reliability sprint, rollback, capacity action, or degraded-mode activation.

4. Identify and cap toil.
   - List recurring manual operational tasks: replaying runs, clearing leases, reconciling tool calls, updating run state, paging humans for known issues, hand-building reports, and shepherding deploys.
   - Classify each task as necessary operations, automatable toil, or product/support work.
   - Set a reduction plan for high-frequency or high-pain toil: remove the cause, automate the action, make it self-service, or change the service contract.

5. Design monitoring from symptoms to causes.
   - Start with user-impacting symptoms: failed admissions, slow runs, stuck queues, missed callbacks, repeated unsafe retries, artifact unavailability, and budget exhaustion.
   - Add cause-oriented signals for triage: dependency saturation, queue backlog, lease churn, checkpoint failures, tool timeout rates, worker restarts, storage latency, and deploy version skew.
   - Ensure every page has an owner, a suspected user impact, a runbook entry, and a threshold that justifies waking someone.

6. Build graceful degradation and overload behavior.
   - Define admission control, tenant quotas, priority classes, queue limits, retry budgets, deadline propagation, and cancellation paths.
   - Decide what the system may drop, defer, approximate, or serve stale under load.
   - Preserve control-plane safety under data-plane overload; operators must still be able to pause, drain, inspect, and recover runs.

7. Make incident response executable.
   - Predefine severity levels, incident commander role, communications channel, status cadence, escalation path, rollback authority, and customer-facing update rules.
   - During an incident, optimize for reducing user impact first, then root cause.
   - Capture a timeline with decisions, signals, mitigations, failed hypotheses, and externally visible effects.

8. Run blameless postmortems that change the system.
   - Write postmortems for meaningful user impact, repeated near misses, unsafe manual intervention, or violated SLOs.
   - Focus on contributing conditions: missing automation, unclear ownership, weak tests, bad defaults, dependency assumptions, release process gaps, and observability blind spots.
   - Convert lessons into tracked actions with owners, due dates, and verification criteria; reject action lists that only say "be more careful."

9. Gate launches and changes by reliability risk.
   - Require prelaunch checks for SLO impact, monitoring, rollback, capacity, dependency limits, data migration, abuse cases, runbook coverage, and on-call readiness.
   - For risky orchestrator changes, use canaries, shadow runs, feature flags, tenant allowlists, progressive rollout, and rapid rollback.
   - Do not launch a feature whose failure mode cannot be detected, limited, or reversed within the promised reliability envelope.

10. Rebalance engineering work with reliability evidence.
   - Review SLO performance, budget burn, top toil sources, incident themes, alert quality, and launch outcomes on a fixed cadence.
   - Spend engineering time where it reduces repeated operational load or user-visible risk.
   - Retire obsolete alerts, runbooks, dashboards, and manual processes when the system changes.

## Output Format

Return:
- `service_promise`: reliability surface, users/tenants, availability/latency/freshness/durability/correctness/safety promises.
- `sli_slo_budget`: SLIs, SLO targets, windows, eligible events, exclusions, burn policy, and budget owner.
- `toil`: recurring tasks, classification, reduction plan, and automation/root-cause strategy.
- `monitoring_alerts`: symptom signals, cause signals, paging thresholds, owner, runbook, and non-page routing.
- `degradation_overload`: admission control, quotas, priority, queue limits, retries, deadlines, stale/drop/defer choices, and operator controls.
- `incident_postmortem`: severity, roles, communication cadence, escalation, rollback authority, timeline, and action verification.
- `launch_review`: readiness gates, canary/flag/allowlist plan, rollback, capacity, dependency limits, runbooks, and on-call handoff.
- `review_cadence`: SLO review, error-budget decisions, alert cleanup, toil trends, and remaining risks.

## Failure, Recovery, And Idempotency

If user impact cannot be measured, start with instrumentation and symptom definitions before setting SLOs. If an alert has no owner, runbook, or immediate action, demote it from paging until the response path is defined.

Repeated reviews should be idempotent: keep stable SLI names, SLO windows, budget formulas, incident IDs, toil categories, and launch-gate IDs so trend comparisons remain valid.

## Failure Modes

- Treating SRE as an on-call staffing model instead of a discipline for measurable reliability, engineering ownership, and controlled risk.
- Defining SLOs around host health, process uptime, or internal queues while users experience failed or stuck orchestrator runs.
- Setting targets so strict that no feature work can ship, or so loose that users lose trust before the budget is exhausted.
- Letting product teams spend error budget without an agreed policy for freezes, rollbacks, or reliability work.
- Paging on every anomaly instead of symptoms that require immediate human action.
- Automating toil without removing its root cause, creating a faster way to perform a bad operation.
- Running postmortems that blame individuals, omit user impact, or produce unowned process reminders.
- Designing overload behavior only after the first capacity incident.
- Launching orchestration capabilities without rollback, tenant scoping, monitoring, runbooks, and on-call handoff.
- Using aggregate reliability numbers that hide one tenant, region, tool provider, model, or workflow class failing badly.

## Boundaries

- This skill designs the SRE operating model for auto-orchestrators; it is not a replacement for low-level distributed systems, checkpointing, transaction, or idempotency design.
- Use observability-specific guidance when the main task is dashboard layout, telemetry schema, tracing instrumentation, or alert implementation detail.
- Use incident-management guidance when the process and communications mechanics are the primary deliverable.
- Use capacity planning or queueing theory when the question is mathematical sizing rather than reliability policy.
- Do not apply heavyweight SRE process to prototypes, internal throwaway tools, or single-user experiments unless they already have user-visible reliability obligations.
- Optional provenance and source trace live in `references/source-notes.md`; do not load it for routine execution.

## Hard Rules

- Do not define primary SLOs around host/process health when users experience run-level failures.
- Do not page on signals without user impact, owner, runbook, and immediate operator action.
- Do not launch reliability-risky changes without detection, blast-radius limits, rollback, and ownership.
- Do not accept postmortem actions that lack owner, due date, and verification criteria.

## Source Closure

This 30-site-reliability-engineering skill is self-contained for runtime use; its source basis is Site Reliability Engineering source notes and local SRE entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
