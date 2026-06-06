# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Item

- id: 28
- title: 数据密集型系统 / Data-Intensive Applications
- skillName: 28-data-intensive-applications

## Source Status

The assigned source file is incomplete for distillation. It contains only a failed fetch from Martin Kleppmann's site:

- local content: `404 Not Found` / `NoSuchKey`

Metadata was therefore supplemented before distillation. The corrected public source identity is Martin Kleppmann's official page for *Designing Data-Intensive Applications*:

- public catalog/source metadata: O'Reilly page for *Designing Data-Intensive Applications*, first edition, published 2017

The public source material identifies the book's focus as the principles and tradeoffs behind reliable, scalable, and maintainable data systems. Public chapter listings cover foundations of data systems, data models and query languages, storage and retrieval, encoding and evolution, replication, partitioning, transactions, distributed-system trouble, consistency/consensus, batch processing, stream processing, and the future of data systems.

## Distilled Principles

For auto-orchestrator design, data-intensive application theory becomes useful when the orchestrator's behavior must survive scale, failure, replay, and evolution.

The core distinction is between authoritative data and derived data. Orchestrator run history, step claims, budget decisions, tenant/API-user context, external side-effect records, and final statuses need durable authority. Dashboards, search indexes, analytics, progress summaries, and caches are derived views that may lag, be rebuilt, or be discarded. Many reliability bugs come from treating a derived view as if it were authoritative.

Reliable orchestration depends on explicit reconstruction. A data design should be able to answer "what happened?", "what is true now?", and "how can we rebuild this view?" Append-only event histories are useful for audit, replay, recovery, process mining, and backfills, while current-state records are useful for fast status checks and operator workflows. The design should specify how these relate.

Consistency is not a single global choice. Stronger coordination is justified for invariants that users, billing, safety, authorization, and external systems rely on. Eventual consistency is acceptable for many views and analytics if the staleness is visible and no downstream component treats it as authoritative.

Idempotency and atomic commit boundaries are mandatory for retried agents and tool calls. Auto-orchestrators naturally retry after timeouts, worker crashes, queue redelivery, model/provider failures, and deploys. Each retried command needs a stable key, and dual writes need a transaction, outbox, append log, reconciliation path, or compensation policy.

Storage technologies should follow access patterns and invariants. Transactional stores fit constrained mutable state. Event logs fit ordered history, fan-out, and rebuildable projections. Search stores fit flexible retrieval. Object stores fit artifacts. Streams fit near-real-time reactions. Batch jobs fit verification, repair, recomputation, and migration.

Partitioning and replication are design choices with product consequences. Partition keys affect fairness, locality, tenant isolation, hot spots, and recovery blast radius. Replicas improve read scale and availability but can expose stale reads unless the design marks which reads need leader/quorum freshness.

Schema evolution is part of runtime design, not a maintenance footnote. Long-running workflows and replayable histories mean new code must often read old records and old events. Versioned schemas, tolerant readers, additive migrations, and controlled backfills reduce deploy risk.

## Auto-Orchestrator Translation

Apply the source material as a design checklist:

1. Classify every data item as authoritative, event history, derived view, cache, blob, telemetry, or disposable worker state.
2. Pick the source of truth for run history, current status, step ownership, budgets, tenant isolation, and external side effects.
3. Use invariant-specific consistency: coordinate correctness-critical decisions and expose staleness for derived views.
4. Attach idempotency keys and atomic write/message boundaries to all retried work.
5. Choose storage models based on access patterns, not technology preference.
6. Define partitioning, replication, and stale-read rules before scaling workers.
7. Design schema evolution, backfill, replay, and projection rebuilds as first-class workflows.
8. Verify data integrity with duplicate, replay, migration, failover, and rebuild drills.

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Metadata Supplement

The manifest provided the target name, skill directory, and assigned source file, but the source content was only a 404 response. Metadata and theory coverage were supplemented from the corrected official Martin Kleppmann page, the public book site, and O'Reilly's public catalog/table-of-contents metadata for the same book.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Designing Data-Intensive Applications source notes and local data-systems entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Data model, storage, encoding, replication, partitioning, consistency, transactions, streams, and derived views.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not choose databases by preference before access patterns, invariants, and evolution paths are known.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The most useful frame is “source of truth versus derived view.” Data architecture fails when rebuildable projections are treated as authority.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Classify records as authoritative, event history, derived view, cache, blob, telemetry, or worker state; then trace invariants, replay, migration, and stale-read tolerance.
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
