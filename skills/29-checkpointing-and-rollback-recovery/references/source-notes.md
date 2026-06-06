# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Item

- id: 29
- title: 检查点与回滚恢复 / Checkpointing and Rollback Recovery
- skillName: 29-checkpointing-and-rollback-recovery
- assigned source files:

## Source Status

The assigned sources are vendor documentation for Apache Flink checkpointing and Confluent Manager for Apache Flink checkpoint configuration. They are complete enough for this local skill because they cover the central runtime concepts needed for auto-orchestrator recovery:

- Checkpoints are fault-tolerant snapshots of state and stream positions.
- Recovery needs durable replayable sources and durable checkpoint storage.
- Checkpointing can provide exactly-once or at-least-once semantics depending on the end-to-end system.
- Production checkpoint storage should be a highly available durable filesystem or object store.
- Important controls include checkpoint interval, timeout, minimum pause, tolerable failures, concurrent checkpoints, externalized checkpoint retention, unaligned checkpoints, and checkpoint behavior after parts of a graph finish.
- Savepoints are distinct from automatic checkpoints: savepoints support planned operations such as upgrades and migrations.

## Distilled Principles

For an auto-orchestrator, checkpointing is not merely "save state sometimes." It is a recovery contract binding together durable state, input replay position, side-effect commit state, and rollback behavior.

The first design move is to define the recoverable unit of work: run, task graph, step, attempt, stream job, SQL statement, or tenant session. Each recoverable unit needs durable identity and a known restore point. A checkpoint must include enough state to resume without trusting worker-local memory.

The second design move is to separate four categories of data:

- Authoritative checkpoint state: state required to continue correctly.
- Replayable input: events, messages, files, or records that can be re-read from a durable position.
- Derived state: caches, views, progress displays, and metrics that can be rebuilt.
- External side effects: actions that may have already escaped the orchestrator.

Exactly-once recovery is only meaningful when these categories are coordinated. A framework may snapshot state exactly once, but the orchestrator still repeats unsafe behavior if remote API calls, emails, tickets, payment events, file writes, or billing updates are not idempotent or commit-protected.

Checkpoint interval expresses a tradeoff. Short intervals reduce reprocessing and can commit outputs sooner, but increase overhead on storage, network, CPU, and coordination. Timeout and minimum-pause settings prevent checkpoint work from consuming the system or silently becoming stale. Concurrency should remain conservative unless overlapping checkpoints have a clear benefit and well-understood restore semantics.

Durable checkpoint storage is a production requirement. A local heap checkpoint may be useful for development, but production recovery needs storage accessible from all recovery participants, with credentials, permissions, isolation, retention, and availability handled explicitly.

Backpressure changes checkpoint mechanics. Unaligned checkpoints can reduce checkpoint duration when barriers are delayed, but they incorporate in-flight buffered data into recovery state. This is useful only when the team accepts the state-size and restore implications.

Partial graph completion matters for orchestrators because some branches may finish while others continue. Finished branches must not drop buffered output, offsets, shared partition state, or transaction pointers before the final durable checkpoint proves that commit state is safe.

Checkpoint retention is a policy decision. Automatic checkpoints support normal fault recovery. Externalized checkpoints and savepoints support cancellation recovery, migration, upgrade, and manual rollback. Retention must also account for privacy, storage cost, tenant isolation, and data lifecycle.

## Auto-Orchestrator Translation

Apply the source material as a design checklist:

1. Define the recoverable unit and the promised recovery semantics.
2. Inventory state, replay sources, derived views, and side effects.
3. Require durable replay sources and durable checkpoint storage before relying on rollback recovery.
4. Choose checkpoint boundaries that include state plus input positions.
5. Tune interval, timeout, minimum pause, and concurrency according to reprocessing cost and overhead.
6. Decide whether backpressure requires unaligned checkpoints or a different throughput design.
7. Persist idempotency keys, transaction pointers, and final-commit evidence for external effects.
8. Specify restore behavior, older-checkpoint fallback, and operator intervention rules.
9. Separate automatic failure-recovery checkpoints from planned-operation savepoints.
10. Test crash, timeout, duplicate delivery, storage slowness, and partial completion cases.

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Metadata Supplement

No external metadata supplementation was required. The manifest provided the target name, skill directory, and source files, and the assigned source files provided enough theory and implementation context to distill an executable auto-orchestrator design skill.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Checkpointing and rollback recovery sources; local recovery entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Consistent global state, checkpoints, message logging, rollback line, domino effect, and recovery protocol.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not roll back irreversible external actions without compensation or human review.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Recovery is about finding a coherent cut in distributed history. A checkpoint that cannot be composed with messages is false safety.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Track local states, in-flight messages, external side effects, checkpoint frequency, rollback dependency, and replay/compensation boundary.
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
