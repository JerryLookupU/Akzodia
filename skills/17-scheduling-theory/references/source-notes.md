# Source Notes

## Local Source

- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/17_调度理论__Scheduling_Theory/supplement_wp_nyu_edu.txt`

## Metadata

The local source is a short NYU faculty page excerpt for Michael Pinedo's books. It identifies the relevant book as:

- Michael L. Pinedo.
- `Scheduling: Theory, Algorithms, and Systems`.
- Editions listed by the local source: 1994, 2001, 2008, 2012, 2016, 2022.
- Domain grouping on the page: Planning, Scheduling & Queueing.

Supplemented metadata/context gathered during distillation:

- The NYU book page for `Scheduling: Theory, Algorithms, and Systems` links to the sixth edition, table of contents, preface, introduction, slides, downloadable material, reviews, and Python algorithms.
- Springer metadata for DOI `10.1007/978-3-031-05921-6` describes the sixth edition as a graduate textbook covering scheduling theory and practice, with additional focus on applications.
- The available NYU table of contents shows core themes: role of scheduling, deterministic model preliminaries, framework and notation, classes of schedules, complexity hierarchy, single-machine models, weighted completion time, maximum lateness, number of tardy jobs, total tardiness, earliness/tardiness, bicriteria problems, parametric analysis, and trade-off curves.

## Distilled Claims

- Scheduling is the problem of assigning work to constrained resources over time.
- A useful scheduling model separates jobs, machines/resources, release times, processing times, due dates, weights, precedence constraints, setup costs, and objective functions.
- Scheduling objectives differ: minimizing makespan, completion time, flow time, lateness, tardiness, weighted cost, SLA misses, or resource idle time can lead to different schedules.
- Deterministic scheduling assumes known jobs and processing times; online or stochastic settings require dispatching rules, slack, monitoring, and rescheduling.
- Single-machine and parallel-machine models provide useful mental templates for orchestrators even when the "machines" are agents, tools, quotas, environments, reviewers, or model endpoints.
- Precedence constraints and resource constraints are different. A job may be logically ready but still unable to run because its required resource, lock, quota, or calendar window is unavailable.
- Dispatching rules are policy decisions, not implementation details. A FIFO queue, shortest-processing-time rule, earliest-due-date rule, weighted priority score, batching policy, or least-slack rule encodes different tradeoffs.
- Preemption and rescheduling must account for interruption cost, partial work, stale results, and auditability.

## Auto-Orchestrator Translation

- Job: one schedulable unit, such as a tool call, agent task, review, test, shard, deployment, retry, or human approval.
- Machine/resource: a constrained executor or capacity pool, such as an agent worker, model endpoint, browser session, API quota, GPU, reviewer, lock, database connection, environment, or time window.
- Release time: earliest time a job can start because inputs, dependencies, policy, or calendar availability are not ready before then.
- Due date/deadline: target or hard latest completion time.
- Processing time: expected duration, preferably with observed historical correction.
- Weight: business value or penalty multiplier for delay.
- Setup cost: cost of switching resource context, such as model warm-up, environment reset, reviewer context loading, API batch setup, or deployment preparation.
- Eligibility filter: hard gate that decides which jobs can legally run now.
- Dispatching rule: ranking function for eligible jobs or job-resource pairs.
- Rescheduling trigger: event that justifies revising assignments.

## Distillation Choices

- The provided local source was too sparse for a self-contained operational skill, so metadata and context were supplemented from the linked NYU book page and Springer book metadata.
- The skill does not attempt to summarize the full textbook. It distills scheduling theory into a compact design procedure for modern auto-orchestrators.
- Historical edition details and mathematical proof details were omitted.
- The result emphasizes executable scheduler design: define the instance, choose the objective, filter eligibility, select dispatching rules, handle fairness/preemption, and verify with trace cases.
- Long source quotations were avoided; source content is paraphrased.
