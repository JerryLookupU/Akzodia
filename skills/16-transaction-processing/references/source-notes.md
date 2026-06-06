# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Assigned Source

The assigned file is a Microsoft Learn page snapshot for an Azure Architecture Center transactional outbox URL, but the captured content is a `404 - Page not found` page rather than the pattern article. It contains no usable transaction-processing theory beyond the intended source URL.

## Supplemented Metadata And Context

Because the assigned source content is incomplete, the distillation supplements operational transaction-processing knowledge needed for auto-orchestrator design:

- Transaction processing theory as used in database and distributed-system design: atomicity, consistency, isolation, durability, concurrency control, recovery, logging, commit boundaries, and failure handling.
- Transactional outbox pattern: commit business state and an outbox record in one local transaction, then publish asynchronously with idempotent publication and consumer deduplication.
- Saga pattern: coordinate long-running, cross-resource workflows through durable forward steps and compensating actions rather than assuming global rollback.
- Idempotent consumer/inbox pattern: store processed message identifiers so at-least-once delivery can be retried without repeating business effects.
- Lease/fencing and optimistic concurrency: prevent stale workers and duplicate agents from finalizing the same case after retries or ownership changes.

Relevant canonical book metadata for the broader theory entry:

- Title: *Transaction Processing: Concepts and Techniques*
- Authors: Jim Gray and Andreas Reuter
- Publisher: Morgan Kaufmann
- Year: 1992

## Distillation For Auto-Orchestrators

For agent orchestration, transaction processing is less about textbook database internals and more about deciding where durable truth lives:

- Every orchestrated case needs explicit state transitions with stable ids, versions, and evidence.
- Every non-rollbackable side effect needs idempotency, compensation, or reconciliation.
- Every state-update-plus-message pattern needs an atomic strategy, usually a transactional outbox when a single database is the local source of truth.
- Every retry path must be designed before the retry occurs; otherwise retries amplify duplicate side effects.
- Every concurrent actor needs a claim, lease, version, or single-writer rule before it can mutate shared state.

The resulting skill therefore turns transaction-processing theory into an executable design checklist for commit boundaries, outbox/inbox, idempotency, sagas, crash recovery, and concurrency control.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Transaction processing sources and local TP entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Atomicity, consistency, isolation, durability, schedules, logs, recovery, and concurrency control.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not demand ACID semantics for every workflow; use weaker guarantees when invariants and users tolerate them.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The heart of transaction processing is protecting invariants while operations interleave and failures occur.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Identify invariants, read/write sets, isolation anomalies, commit boundary, log record, recovery point, and compensation or rollback path.
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
