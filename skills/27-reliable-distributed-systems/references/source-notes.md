# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Metadata

- Entry id: 27
- Skill name: `27-reliable-distributed-systems`
- Title: Reliable Distributed Systems

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

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Reliable distributed systems sources and local reliability entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Fault model + replication + quorum/consensus + failure detection + recovery protocol.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use consensus language unless the safety and liveness assumptions are explicit.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Reliability is a protocol property under a fault model, not a promise made by adding replicas.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Name crash/Byzantine/omission assumptions, quorum intersection, leader behavior, timeout meaning, reconfiguration, and recovery evidence.
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
