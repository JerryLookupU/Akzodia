# Source Notes

## Manifest Item

- id: 28
- title: 数据密集型系统 / Data-Intensive Applications
- skillName: 28-data-intensive-applications
- assigned source file: `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/28_数据密集型系统__Data_Intensive_Applications/supplement_martin_kleppmann_com.txt`

## Source Status

The assigned source file is incomplete for distillation. It contains only a failed fetch from Martin Kleppmann's site:

- original URL in file: `https://martin.kleppmann.com/2017/03/27/data-intensive-applications.html`
- local content: `404 Not Found` / `NoSuchKey`

Metadata was therefore supplemented before distillation. The corrected public source identity is Martin Kleppmann's official page for *Designing Data-Intensive Applications*:

- corrected source page: `https://martin.kleppmann.com/2017/03/27/designing-data-intensive-applications.html`
- book site: `https://dataintensive.net/`
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

## Source Files

- `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/28_数据密集型系统__Data_Intensive_Applications/supplement_martin_kleppmann_com.txt`

## Metadata Supplement

The manifest provided the target name, skill directory, and assigned source file, but the source content was only a 404 response. Metadata and theory coverage were supplemented from the corrected official Martin Kleppmann page, the public book site, and O'Reilly's public catalog/table-of-contents metadata for the same book.
