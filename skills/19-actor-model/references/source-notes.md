# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
Runtime note: this file is provenance/source trace only. The executable skill contract and required operating knowledge are contained in `../SKILL.md`; do not require external source files, webpages, source reports, or original texts at runtime.

## Assigned Source

The assigned file is an MIT DSpace publication record and abstract for Gul Agha's *ACTORS: A Model of Concurrent Computation in Distributed Systems*. It is not a full thesis text extraction.

## Supplemental Local Context

Additional local files used to fill missing metadata and orchestration mapping:

Relevant metadata:

- Title: *ACTORS: A Model of Concurrent Computation in Distributed Systems*
- Author: Gul Abdulnabi Agha
- Date issued: June 1, 1985
- Series/report number: AITR-844

## Distilled Concepts

The source abstract frames Actor Model as a concurrency model for distributed systems. The extracted operating ideas for auto-orchestrator design are:

- Concurrency is limited by hardware resources and logical dependencies rather than by a single global control flow.
- Actors communicate through asynchronous message passing.
- Actors can encapsulate changing local state.
- Actors can create other actors dynamically.
- Pipelining and message passing can expose large-scale parallelism.
- Deadlock and divergence are first-class distributed-computing risks.

The local theory pack maps these ideas to orchestrator roles:

- `SchedulerActor`: decides what work is ready and where it should go.
- `WorkerActor`: executes a unit of work or wraps a tool.
- `MonitorActor`: observes health, queue depth, progress, and timing.
- `RecoveryActor`: retries, restarts, compensates, or escalates failed work.
- `MemoryActor`: serializes writes to shared memory or experience stores.

## Auto-Orchestrator Interpretation

For agent orchestration, Actor Model is most useful as a state-ownership and communication discipline:

- Put mutable state behind one actor or one transactional boundary.
- Use explicit message schemas instead of hidden shared variables.
- Make mailboxes observable and bounded.
- Treat supervision as part of the design, not an implementation afterthought.
- Record delivery assumptions and idempotency rules anywhere messages cross process, queue, or storage boundaries.

The resulting skill therefore turns Actor Model into a design checklist for actor boundaries, mailbox contracts, local state ownership, supervision trees, backpressure, dynamic actor creation, and message-failure testing.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Agha Actor Model sources and local actor entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Actors own state, receive messages, send messages, create actors, and change behavior for the next message.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use actors as mere threads; if state is shared freely, the model’s protection has been lost.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The Actor model makes isolation and asynchronous causality the primary design units. Shared-state coordination becomes message protocol design.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Find state ownership, mailbox boundaries, message types, creation paths, supervision, ordering assumptions, backpressure, and what happens when a message is late or duplicated.
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
