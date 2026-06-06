# Source Notes

## Manifest Metadata

- Entry id: 27
- Skill name: `27-reliable-distributed-systems`
- Title: Reliable Distributed Systems
- Source file: `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/27_可靠分布式系统__Reliable_Distributed_Systems/supplement_www_cs_cornell_edu.txt`

## Source Coverage

The provided source is a Cornell Kenneth P. Birman page snapshot. It identifies Birman's textbook, "Guide to Reliable Distributed Systems: Building High-Assurance Applications and Cloud-Hosted Services," and summarizes Cornell work on reliable distributed systems across Isis, Horus, Ensemble, Derecho, Cascade, and mission-critical deployments such as stock exchanges, air traffic control, naval systems, industrial process control, and telephony.

The source is not a full book chapter or course note. It supports the skill's emphasis on high-assurance services, group communication lineage, replication, automatic reconfiguration, consistency, scalability, performance-aware reliability, RDMA/high-speed data movement, edge placement, and durable audit/logging themes. It does not provide complete step-by-step orchestrator design procedures.

## Supplemented Theory

Because the source is incomplete for executable skill construction, the skill supplements stable reliable distributed systems concepts:

- Partial failure must be modeled explicitly: crash, restart, omission, duplication, reordering, slow node, partition, storage loss, clock skew, and dependency outage.
- Safety and liveness should be separated. A reliability design must say what never happens and what eventually happens when assumptions hold.
- Ownership should use leases, epochs, and fencing tokens so stale workers or leaders cannot continue writing after failover.
- Durable logs or commit records are the recovery backbone. Recovery should reconstruct authoritative state from durable records, not process memory.
- Replication requires an ordering or conflict rule. Otherwise redundancy can create split brain.
- Idempotency is required for retries, replay, and crash recovery around side effects.
- Group membership should be treated as ordered view changes for systems that coordinate replicated actors.
- Strong consistency should be reserved for authoritative control-plane state; weak consistency is acceptable for telemetry and derived status.
- Performance and reliability interact: moving computation close to data can reduce both latency and failure surface.

## Distillation For Auto-Orchestrators

The local skill turns the theory into an orchestrator design workflow:

1. Declare guarantees for task ownership, commit, recovery, and user-visible completion.
2. Build a failure matrix for orchestrator roles and dependencies.
3. Select a coordination pattern: leases with fencing, primary-backup, quorum replication, state machine replication, or event-sourced replay.
4. Design crash recovery around durable intent and idempotent replay.
5. Decide which state must be strongly consistent.
6. Verify with crash-point, partition, duplicate, stale owner, and restart tests.

## Audit Note

No local cangjie skill was available in this runtime. The distillation therefore used book2skill and skill-creator-style fallback, with source incompleteness recorded in `audit.json`.
