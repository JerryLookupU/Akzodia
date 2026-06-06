# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Item

- id: 26
- title: 分布式系统 / Distributed Systems
- skillName: 26-distributed-systems

## Source Status

The assigned source file is the official page for the 4th edition of *Distributed Systems* by Maarten van Steen and Andrew S. Tanenbaum. It is not a full book extraction. The page states that version 4.03 was released in January 2025 with small corrections, identifies the citation as:

`M. van Steen and A.S. Tanenbaum, Distributed Systems, 4th ed., distributed-systems.net, 2023.`

The same page says the edition keeps the setup of the third edition, discusses general principles close to examples from existing distributed systems, includes blockchain material, updates Python examples to Python 3, and provides downloadable slides plus code/figures.

Local metadata supplements the source identity:

- Representative resource: Maarten van Steen & Andrew S. Tanenbaum, *Distributed Systems*, 4th edition.
- Why included in the theory pack: when an orchestrator has multiple workers, tools, and services, it is naturally a distributed system.
- Intended use: handle replication, consistency, clocks, failures, coordination, and message passing.

## Distilled Principles

For auto-orchestrator design, distributed-systems theory becomes operational when the orchestrator cannot rely on one address space, one clock, one failure domain, or one linear order of events.

The central design move is to identify the unit of work and the authority for state. Each run, step, tool call, artifact, side effect, and tenant context needs a durable identity. Every mutable record needs either a single writer or an explicit conflict-resolution rule. Without this, retries and concurrent workers will create duplicate effects, contradictory statuses, and unreplayable histories.

A distributed orchestrator should separate authoritative state from derived state. Event logs, run records, ownership claims, budget consumption, safety decisions, and final statuses are authoritative. Dashboards, progress views, caches, worker-local memory, and search indexes are derived. Derived state may lag, be rebuilt, or be discarded.

Communication semantics must be declared, not assumed. Queues and RPCs rarely deliver the exact semantics a product wants by default. At-least-once delivery requires idempotency and deduplication. At-most-once delivery may lose work. Ordering usually holds only within a narrow key, if at all. "Exactly once" should be treated as a property of the whole workflow, not a label on one transport component.

Coordination is expensive and should be attached to correctness-critical decisions: claiming work, committing final state, spending scarce budget, choosing the sole executor for a non-repeatable side effect, or changing membership. Less critical views can be eventually consistent. This split prevents global coordination from becoming the bottleneck while keeping high-risk invariants protected.

Partial failure is normal. A worker can die while a tool call continues. A timeout can fire while the remote side later commits. A queue can redeliver an already-completed message. A database can fail over while a lease owner still believes it is active. A model provider can be degraded for one route but not another. The design should assign retry, compensation, fallback, human handoff, or fail-fast behavior by boundary.

Time needs special care. Wall clocks are useful for display and coarse deadlines, but not for proving causal order. For orchestrators, persist causal links: run id, step id, attempt id, message id, predecessor ids, idempotency key, and emitted event id. Use monotonic durations for timeouts and treat timeout as suspicion, not proof that work stopped.

Scaling is a topology decision. Partitioning by tenant, run id, workflow type, tool class, region, or priority changes fairness and failure blast radius. A slow tool or noisy tenant should not block unrelated work. The control plane should remain available enough to pause, route, shed load, or recover even when execution workers saturate.

## Auto-Orchestrator Translation

Apply the source material as a design checklist:

1. Inventory participants and boundaries: API, planner, scheduler, workers, queues, stores, model providers, tool gateways, sandboxes, notifiers, and human handoff.
2. Define authoritative state and single-writer or conflict-resolution policy for each mutable entity.
3. Choose communication semantics per channel and add idempotency for every retried or externally visible action.
4. Coordinate only the decisions that protect correctness or scarce resources.
5. Decide which reads may be stale and which must be strongly consistent.
6. Model partial failures at every boundary and bind each to retry, fallback, compensation, pause, or fail-fast behavior.
7. Verify with drills that duplicate messages, worker death, stale leases, database failover, and remote timeouts preserve key invariants.

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Metadata Supplement

The manifest provided the target name, skill directory, and assigned source file. The source file was incomplete for full theory extraction because it is a short official book page rather than the book text. Metadata was supplemented from the adjacent local `metadata.json` and source-pack index notes, not from unrelated files outside the theory pack.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Distributed systems sources and local distributed-systems entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Nodes, messages, clocks, replication, partitioning, consistency, coordination, and partial failure.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not treat distributed work as a bigger single process; locality and partial failure change the problem.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The central lesson is that failure is normal and knowledge is local. Design must specify what each node can know and do when communication is delayed or broken.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Map state ownership, message paths, clock assumptions, consistency needs, partition behavior, retry semantics, and recovery ownership.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
