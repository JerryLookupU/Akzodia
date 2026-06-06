---
name: 27-reliable-distributed-systems
description: Use when designing or reviewing an auto-orchestrator that must keep work running across process, node, network, storage, scheduler, or restart failures; especially when choosing replication, membership, recovery, consistency, failover, audit log, or high-availability patterns.
---

# Reliable Distributed Systems

## When To Use

Use this skill when an orchestrator design must continue correctly despite partial failure. Typical triggers include worker loss, controller restart, duplicate delivery, split brain, replay after crash, unreliable health checks, cross-node state replication, rolling upgrades, or "keep the job alive" requirements.

Use it for design reviews before implementing task dispatch, lease ownership, durable queues, replicated control planes, recovery loops, or stateful tool execution. The output should be a concrete reliability design: failure assumptions, preserved invariants, recovery protocol, and verification checks.

## Workflow

1. Define the service contract.
   - Name the user-visible guarantee: at-most-once, at-least-once, effectively-once, ordered execution, bounded recovery time, no lost committed work, or read-your-writes.
   - Separate safety from liveness. Safety is what must never happen; liveness is what must eventually happen when assumptions hold.
   - State the blast radius for each orchestrator role: planner, scheduler, worker, state store, artifact store, message bus, lock service, and observer.

2. Build the failure model.
   - List crash-stop, restart-with-stale-state, omission, duplication, reordering, slow node, network partition, storage write loss, clock skew, and dependency outage.
   - For each failure, decide whether the design masks it, detects it and degrades, or declares it out of scope.
   - Prefer explicit leases, epochs, fencing tokens, monotonic sequence numbers, and durable commit records over implicit "this process is probably alive" assumptions.

3. Choose the coordination core.
   - For single-owner work, use lease plus fencing: every side effect carries the current epoch/token and stale owners are rejected.
   - For replicated state, choose primary-backup, quorum replication, state machine replication, or event-sourced replay based on write rate, consistency needs, and recovery time.
   - For group membership, treat membership change as a state transition with an ordered view, not as informal heartbeats.
   - For high-throughput data movement, colocate computation with data and avoid unnecessary copies before adding more replicas.

4. Design recovery before steady state.
   - Record enough durable intent to resume after any acknowledged step: command accepted, lease acquired, task assigned, side effect started, side effect committed, compensation needed.
   - Make recovery idempotent. A restarted orchestrator should be able to scan durable state, reconstruct ownership, retry incomplete work, and ignore already-committed work.
   - Define orphan handling for workers that continue after the controller restarts: revoke by epoch, fence external writes, and reconcile heartbeats against durable assignment state.

5. Make consistency choices explicit.
   - Identify which state needs strong consistency: task ownership, budget counters, irreversible side effects, checkpoint pointers, user-visible completion.
   - Allow weaker consistency only for cached status, telemetry, speculative scheduling, and non-authoritative progress views.
   - If using eventual consistency, define the convergence rule and the conflict winner before coding.

6. Add observability and tests to prove the contract.
   - Emit structured events for view changes, lease grants, fencing rejects, replay decisions, duplicate command suppression, retry exhaustion, and recovery completion.
   - Test crash points around every durable boundary, including before and after commit acknowledgement.
   - Run partition, duplicate message, slow worker, stale leader, clock skew, and store restart scenarios. Verify both invariant preservation and bounded recovery.

7. Produce a reliability decision record.
   - Include failure model, guarantees, chosen protocol, rejected alternatives, operational knobs, required metrics, and runbook actions.
   - Tie every guarantee to a mechanism and every mechanism to a test.

## Failure Modes

- Treating reliability as retry logic. Retries without durable state, idempotency, and fencing can amplify duplicates or corrupt external systems.
- Confusing health checks with ownership. A green heartbeat does not prove a process still has the right to act.
- Relying on wall-clock time for correctness. Use monotonic versions, leases with conservative expiry, and server-side fencing for safety-critical paths.
- Replicating state without defining order. Multiple copies of unordered updates can produce split brain rather than availability.
- Recovering from memory instead of the log. If a restart cannot reconstruct the world from durable records, acknowledged work can disappear.
- Optimizing throughput before reducing data movement. Birman-style reliable systems work emphasizes that performance and reliability are coupled; unnecessary movement can become the bottleneck and the failure surface.

## Boundaries

Do not use this skill as a complete distributed consensus tutorial or as a replacement for a formal protocol proof. If the system needs Byzantine fault tolerance, cryptographic audit consensus, or cross-organization trust, bring in a BFT/blockchain-specific design.

Do not force strong consistency onto every status surface. For orchestrators, strong consistency is usually required for ownership and irreversible effects, while progress dashboards and telemetry can often be approximate.

Do not claim exactly-once execution unless every external side effect is idempotent, fenced, or transactionally coupled to the orchestrator's durable commit record. In most practical orchestrators, "effectively once under declared assumptions" is the defensible target.
