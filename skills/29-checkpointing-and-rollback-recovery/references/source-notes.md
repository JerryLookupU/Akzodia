# Source Notes

## Manifest Item

- id: 29
- title: 检查点与回滚恢复 / Checkpointing and Rollback Recovery
- skillName: 29-checkpointing-and-rollback-recovery
- assigned source files:
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/29_检查点与回滚恢复__Checkpointing_and_Rollback_Recovery/01_nightlies_apache_org.txt`
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/29_检查点与回滚恢复__Checkpointing_and_Rollback_Recovery/02_docs_confluent_io.txt`

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

## Source Files

- `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/29_检查点与回滚恢复__Checkpointing_and_Rollback_Recovery/01_nightlies_apache_org.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/29_检查点与回滚恢复__Checkpointing_and_Rollback_Recovery/02_docs_confluent_io.txt`

## Metadata Supplement

No external metadata supplementation was required. The manifest provided the target name, skill directory, and source files, and the assigned source files provided enough theory and implementation context to distill an executable auto-orchestrator design skill.
