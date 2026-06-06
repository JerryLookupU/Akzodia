# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
Runtime note: this file is provenance/source trace only. The executable skill contract and required operating knowledge are contained in `../SKILL.md`; do not require external source files, webpages, source reports, or original texts at runtime.

Primary assigned sources:

Local metadata consulted:

## Source-Derived Points

- The representative resource is Stephen Boyd and Lieven Vandenberghe, *Convex Optimization*, published by Cambridge University Press in 2004.
- The Stanford page records that Cambridge University Press allowed the book to remain available on the web and links the open PDF, lecture slides, exercises, and code resources.
- The Cambridge page describes the book as a comprehensive introduction that teaches recognition of convex optimization problems, numerical solution methods, duality, approximation, statistical estimation, and applications.
- The book defines an optimization problem around variables, an objective function, constraint functions, and bounds. A solution is the feasible point with the smallest objective value.
- Convex optimization generalizes least squares and linear programming. The standard convex form minimizes a convex objective subject to convex inequality constraints and affine equality constraints.
- The source emphasizes that recognizing or reformulating a practical problem as convex is the central skill; after that, solving is comparatively reliable and efficient.
- Interior-point and special-purpose methods can solve many convex problems reliably, especially when problem structure such as sparsity is exploited.
- General nonlinear optimization lacks comparable guarantees; local methods may depend heavily on initial guesses and can return only local optima.
- Lagrangian duality augments the objective with weighted constraints. Dual functions give lower bounds, dual problems are convex, and dual variables can support interpretation of constraints.
- For convex problems satisfying suitable conditions, KKT conditions provide necessary and sufficient optimality conditions.
- Multi-objective problems can be scalarized with nonnegative weights, and varying weights can explore an optimal tradeoff curve or surface.

## Auto-Orchestrator Distillation

For auto-orchestrator design, convex optimization becomes a formulation discipline:

- Decision variables represent controllable orchestration choices: allocation shares, quotas, permits, retry budgets, model mix, batching levels, admission rates, or policy weights.
- Objectives represent measurable cost or utility: latency penalty, dollar cost, quota use, risk, fairness deviation, quality loss, or deadline miss penalty.
- Constraints represent hard runtime contracts: SLA ceilings, token budgets, API quotas, worker capacity, queue fairness, memory, deadline feasibility, and conservation of allocation.
- Convexity checks protect the design from pretending a heuristic or nonconvex assignment is solver-ready.
- Dual variables and active constraints can be interpreted as resource pressure signals when the formulation and solver conditions support that.
- Relaxations are useful when exact scheduling or assignment is discrete: solve the convex version for bounds, weights, resource prices, or a continuous policy, then round and validate.

## Metadata Completeness

Metadata and source coverage are complete enough for this skill: the manifest supplies the skill name, target directory, and source files; the local metadata identifies the representative book, authors, status, links, and auto-orchestrator usage; and the full open PDF text is available locally.

No long source quotations were copied into the skill.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Convex optimization sources and local convex-optimization entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Convex objective + convex feasible set + duality + KKT/sensitivity. Convexity makes local evidence globally meaningful.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not label a problem convex until variables, constraints, and objective preserve convexity.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The distinctive insight is certificates: a convex problem can often prove not just a good answer, but why no better feasible answer exists under the model.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Define variables, objective, constraints, convexity assumptions, feasible region, dual variables, and sensitivity to weights or bounds.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

zation is the right skill for a request.
- Key fragment: Use when designing or auditing an auto-orchestrator that must choose resource allocations, worker/tool assignments, rate limits, SLA tradeoffs, budgets, retry quotas, batching levels, or scheduling policy weights under constraints that may be formulated as a convex optimization problem or convex relaxation.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
