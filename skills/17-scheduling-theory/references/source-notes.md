# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Local Source

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

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Scheduling theory sources and local scheduling entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Jobs, machines/resources, processing times, release dates, deadlines, precedence, objective, and dispatch policy.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use scheduling theory for conceptual decomposition before jobs and resources are known.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Scheduling is not just ordering tasks; it is allocating scarce processing capacity under time and precedence constraints.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Classify resources, job attributes, readiness, precedence, due dates, setup costs, preemption, and objective; then choose dispatch, heuristic, or optimization accordingly.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

zation objectives.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
