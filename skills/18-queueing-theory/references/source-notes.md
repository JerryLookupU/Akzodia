# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
Primary assigned source:

Local metadata consulted:

## Source-Derived Points

- Queueing analysis starts by choosing or building a mathematical model for a real service system.
- The modeling step necessarily simplifies, approximates, and often relies on assumptions about behavior that may not be directly evidenced.
- Queueing results should usually be treated as approximate indicators for real systems, useful for finding operating weaknesses, improvement directions, and rough values of controllable variables.
- Many exact queueing results assume equilibrium or steady-state behavior; transient and nonstationary behavior is harder.
- There is a tradeoff between realistic models that may be analytically intractable and simplified models whose validity may be limited.
- Queueing theory is strong at estimating expected waiting time, number of users/jobs in the system, server busy/idle fraction, and busy-period duration.
- It is less generally strong at producing full probability distributions, except in special cases or with transform and numerical methods.
- The source highlights Poisson arrivals and exponential interarrival/service assumptions as common foundations for many exact results.

## Auto-Orchestrator Distillation

For orchestrator design, the theory becomes a capacity-control workflow:

- Model tasks, tool calls, review requests, test runs, or subagent jobs as arrivals.
- Model workers, API permits, browser sessions, review lanes, test environments, and database connections as servers.
- Use `lambda`, `mu`, `c`, and `rho = lambda / (c * mu)` as first-pass congestion variables.
- Treat high utilization as a warning sign because wait time can rise sharply near full capacity.
- Separate queues by task class or urgency when mixed work would cause priority inversion or long-job blocking.
- Add backpressure and retry budgets so incidents do not multiply arrival load.
- Use measurement and simulation when steady-state or exponential assumptions are too weak.

## Supplemented Context

The representative book named in local metadata is Leonard Kleinrock, *Queueing Systems, Volume I: Theory*, but the available assigned source is a MIT web supplement rather than the book text. To make the skill executable for auto-orchestrator design, the skill supplements the source with standard queueing concepts also reflected in the local pack notes:

- Little's Law as a steady-flow sanity check.
- Utilization `rho`, arrival rate `lambda`, service rate `mu`, and worker count `c`.
- Queue discipline choices such as FIFO, priority queues, aging, bounded queues, admission control, and backpressure.
- Engineering observability metrics: arrival rate, service time, queue length, wait time, sojourn time, utilization, idle time, retries, timeouts, and abandonment.

No long source quotations were copied into the skill.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Queueing theory sources and local queueing entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Arrival process, service process, servers, utilization, waiting time, queue length, Little’s Law, and capacity tradeoffs.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not apply steady-state formulas blindly to adversarial, nonstationary, or strongly coupled workloads.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Queues diagnose delay as a structural consequence of variability and utilization, not merely worker slowness.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Measure arrivals, service times, concurrency, utilization, blocking, priority, retries, and abandonment; look for high utilization, burstiness, and feedback retries.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

zation targets, or capacity-sizing decisions based on arrival rates, service rates, and queue behavior.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
