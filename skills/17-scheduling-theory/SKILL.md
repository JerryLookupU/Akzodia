---
name: 17-scheduling-theory
description: Use when designing, tuning, or debugging an auto-orchestrator scheduler that assigns tasks, agents, tools, workers, queues, or scarce resources over time under release times, deadlines, precedence constraints, priorities, setup costs, preemption, fairness, throughput, latency, tardiness, or utilization objectives.
source_files:
  - references/source-notes.md
---
# 17 Scheduling Theory

## Book-Derived Essence

- Core framework: Jobs, machines/resources, processing times, release dates, deadlines, precedence, objective, and dispatch policy.
- Deep idea: Scheduling is not just ordering tasks; it is allocating scarce processing capacity under time and precedence constraints.
- Discovery method: Classify resources, job attributes, readiness, precedence, due dates, setup costs, preemption, and objective; then choose dispatch, heuristic, or optimi

zation accordingly.
- Boundary: Do not use scheduling theory for conceptual decomposition before jobs and resources are known.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestration problem is not just "what should happen?" but "which eligible work should run on which constrained resource, in what order, and when should the schedule be revised?"

Strong triggers:
- An orchestrator must assign jobs to agents, tools, queues, workers, GPUs, API quotas, review slots, deploy windows, or other limited resources.
- Work has release times, due dates, deadlines, processing-time estimates, priorities, dependencies, setup costs, batching rules, or cooldowns.
- A scheduler is missing SLAs, starving lower-priority work, overloading one resource, thrashing through retries, or leaving capacity idle while eligible work exists.
- You need a dispatching rule such as shortest processing time, earliest due date, weighted priority, least slack, critical ratio, first-ready, aging, or a hybrid rule.
- You are deciding whether to preempt running work, reserve capacity, batch similar tasks, split work across parallel machines, or replan after failures and arrivals.
- You need to compare "simple queue," "DAG executor," "priority scheduler," "resource allocator," and "calendar planner" designs by their scheduling semantics.

Prefer a workflow-control skill when the main risk is branching, joins, cancellation, or token flow. Prefer a planning skill when the task set itself is still unknown. Use this skill once candidate jobs and resources are visible enough to make allocation decisions.

## Activation And Execution Gate

Activate only when the problem is choosing which eligible jobs run on which constrained resources, in what order, and when to revise that decision. Do not activate for pure task decomposition, pure workflow branching, static dependency drawing, or queue-capacity estimation with no ordering/resource assignment question.

Before execution, identify candidate jobs, constrained resources, hard constraints, at least one objective, and whether arrivals are static/offline or dynamic/online. If jobs or resources are unknown, ask for them or provide a minimal trace table before choosing a dispatching rule. Always filter eligibility before ranking.

Standalone contract: this skill contains the scheduling concepts needed for orchestrator design; `references/source-notes.md` is optional provenance, not required execution context. During normal execution, do not read external files, webpages, original books, source reports, external source folder, distilled source material, or out-of-directory material.

## Workflow

1. Define the scheduling instance.
   - Name each `job`: tool call, agent task, file shard, review, test, deployment, data batch, retry, or human approval.
   - Name each `machine` or constrained resource: worker, model, API quota, database connection, GPU, browser session, reviewer, environment, time window, or lock.
   - Record whether machines are identical, specialized, unrelated, capacity-limited pools, calendars, or mutually exclusive resources.
   - Capture job attributes: release time, processing-time estimate, due date, hard deadline, weight, priority, owner, setup class, retry cost, interruptibility, and required capabilities.
   - Capture precedence constraints separately from resource constraints. A job can be logically ready but still unschedulable because the needed resource is busy.

2. Choose the objective before choosing the algorithm.
   - Use `makespan` when the goal is finishing the whole run as early as possible.
   - Use `flow time` or `response time` when users care about how long each job spends in the system.
   - Use `lateness`, `tardiness`, or SLA miss count when due dates matter.
   - Use weighted completion or weighted tardiness when some jobs are more valuable or costly to delay.
   - Use utilization only as a guardrail. Maximizing busy time can worsen latency, deadlines, and recovery.
   - If objectives conflict, state the priority order: hard constraints first, then SLA risk, then business weight, then throughput, then fairness, unless the product requirement says otherwise.

3. Classify the schedule type.
   - `Static/offline`: all jobs and estimates are known before execution. Use for release plans, migration windows, and fixed batch runs.
   - `Dynamic/online`: jobs arrive while the system runs. Use dispatching rules, aging, admission control, and periodic rescheduling.
   - `Deterministic`: processing times and resource availability are trusted enough for fixed commitments.
   - `Stochastic/uncertain`: estimates are noisy. Keep slack, monitor drift, and revise from actual completions.
   - `Preemptive`: running work may be paused, killed, migrated, or superseded. Define lost work and compensation cost.
   - `Non-preemptive`: once started, work runs to completion unless failure or cancellation intervenes.

4. Build the eligibility filter before ranking jobs.
   - A job is eligible only if dependencies are complete, release time has arrived, required inputs exist, required capability is available, and running it would not violate a hard constraint.
   - Apply safety gates before priority: approval, budget, isolation, quota, lock ownership, deployment freeze, data residency, or exclusive environment access.
   - Split constraints into `hard` constraints that cannot be violated and `soft` constraints that become penalties in the ranking function.
   - Make infeasible jobs explicit with a reason: waiting on dependency, no capable resource, blocked by quota, deadline impossible, or policy denied.

5. Select a dispatching rule that matches the objective.
   - For low mean latency on one interchangeable pool, consider shortest estimated processing time, with aging to prevent starvation.
   - For deadlines, consider earliest due date, least slack, or critical ratio. Add weight when some misses cost more than others.
   - For high-value work, use weighted shortest processing time or a score such as `business_weight / estimated_duration`, bounded by fairness rules.
   - For setup-heavy resources, group compatible jobs when batching reduces setup cost without causing unacceptable tardiness.
   - For scarce specialized resources, reserve capacity for jobs that only that resource can run; avoid filling it with work that a generic resource could handle.
   - For heterogeneous resources, rank feasible `(job, resource)` pairs, not just jobs. Include speed, cost, capability, warm state, and setup transition.

6. Add fairness, starvation, and overload controls.
   - Add aging so waiting jobs gain priority over time.
   - Enforce per-tenant, per-owner, or per-class concurrency limits when one source can flood the scheduler.
   - Keep a small slack buffer for urgent arrivals if the domain has frequent emergency jobs.
   - Use admission control when accepting more work would make already-accepted deadlines impossible.
   - Track queue age distribution, not just average queue length. A good average can hide abandoned tail work.

7. Decide rescheduling and preemption rules.
   - Reschedule on meaningful events: job arrival, job completion, failure, deadline change, resource loss, quota refill, manual override, or estimate drift.
   - Avoid global replanning on every small event if the cost causes instability. Use a planning cadence or threshold.
   - Preempt only when the gain exceeds the interruption cost: saved deadline miss, released scarce resource, avoided cascade failure, or canceled obsolete work.
   - Define what happens to partial work: checkpoint, discard, resume, compensate, or mark as late result ignored.
   - Preserve auditability by recording why the scheduler changed order, not only the final order.

8. Verify the scheduler with trace cases.
   - Construct small tables of jobs, resources, release times, processing times, due dates, weights, and dependencies.
   - Simulate at least three cases: normal load, overload near due dates, and a late urgent arrival.
   - Check invariants: no job starts before release/dependencies, no resource exceeds capacity, hard deadlines/policies are respected, and every waiting job has a visible reason.
   - Check objective behavior: shorter jobs improve latency, urgent jobs reduce tardiness, aging eventually moves old work, and specialized resources are not wasted on generic jobs.
   - Add production metrics for queue age, SLA risk, resource utilization, preemptions, retries, starvation, and schedule churn.

## Output Format / Deliverables

Return a scheduler contract:
- Instance table: jobs, resources, release times, processing estimates, due dates/deadlines, weights, priorities, setup classes, capabilities, dependencies, and interruptibility.
- Objective order: hard constraints, SLA/deadline risk, weight/value, throughput, fairness, and utilization guardrails.
- Eligibility filter: dependency, release-time, capability, policy, budget, quota, lock, and calendar checks with infeasible reasons.
- Dispatching policy: ranking function for jobs or `(job, resource)` pairs, tie-breakers, aging, reservations, batching, overload control, and preemption/rescheduling triggers.
- Verification: trace simulations, invariants, expected objective behavior, metrics, and audit fields explaining schedule changes.

## Failure / Recovery / Idempotency

If estimates are weak, use ranges and trace simulations rather than a false precise schedule. If no feasible job exists, return visible blocked reasons instead of silently idling capacity.

For repeated runs, preserve stable job/resource ids and policy names. Rescheduling should explain deltas from the prior order and avoid churn unless a trigger or threshold fires.

When scheduling decisions fail, recover by replaying the trace, checking eligibility reasons, restoring preempted work from checkpoints or compensation rules, and revising the ranking function or hard-constraint model before adding capacity.

## Hard Rules

- Do not rank jobs before applying eligibility and safety gates.
- Do not make utilization the primary objective when latency, deadlines, or fairness matter.
- Do not let high-priority streams starve old or long-running work without an explicit fairness exception.
- Do not preempt without naming interruption cost, partial-work handling, and audit evidence.
- Do not hide scheduling policy inside worker code without observable metrics and trace tests.

## Failure Modes

- Ranking jobs before filtering eligibility. This can select impossible work and hide the true bottleneck.
- Treating every task as equal FIFO work when deadlines, weights, or scarce resources differ.
- Optimizing utilization as the primary goal. Fully busy resources can increase lateness and make urgent work impossible to absorb.
- Ignoring setup and warm-state costs. Constantly switching tools, models, environments, or reviewers can dominate processing time.
- Letting high-priority streams starve everything else. Add aging, quotas, or minimum service guarantees.
- Using shortest-job rules without guarding large jobs. Long tasks can wait forever under steady arrivals of small tasks.
- Assuming estimated duration is truth. Noisy estimates need slack, confidence bands, and correction from observed runtime.
- Preempting too aggressively. Schedule churn can waste partial work and make audit trails unreadable.
- Scheduling specialized resources with generic FIFO queues. Work that only one resource can run should not be blocked by work that many resources can run.
- Hiding scheduling policy inside ad hoc worker code. The orchestrator then cannot explain, test, or revise allocation decisions.

## Boundaries

This skill covers resource allocation and timing policy for known or discoverable work. It does not by itself decompose goals into tasks, prove workflow branching semantics, design compensation logic, or choose business priorities.

Do not use this skill to produce a full mathematical optimization model unless the user asks for one and the data supports it. For most auto-orchestrators, a transparent dispatching rule plus targeted simulation is more useful than an opaque optimal solver.

Hard real-time and safety-critical scheduling require domain-specific verification beyond this skill. Treat missed deadlines, preemption safety, and admission control as engineering contracts, not preferences.

When the target runtime only exposes a simple queue, do not pretend advanced scheduling is unavailable. But make the missing semantics explicit: eligibility filter, ranking function, resource reservation, aging, preemption, telemetry, and trace tests must live somewhere observable.

## Source Closure

This 17-scheduling-theory skill is self-contained for runtime use; its source basis is Scheduling theory sources and local scheduling entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
