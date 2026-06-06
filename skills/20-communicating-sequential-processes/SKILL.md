---
name: 20-communicating-sequential-processes
description: Use when designing or repairing an auto-orchestrator with multiple agents, workers, tool runners, services, or resource owners that must coordinate through explicit message passing, rendezvous, backpressure, guarded choices, no shared mutable state, deadlock analysis, termination signals, or channel contracts.
source_files:
  - references/source-notes.md
---
# 20 Communicating Sequential Processes

## Book-Derived Essence

- Core framework: Processes synchroni

ze through events/channels; traces, choices, refusal, and parallel composition define behavior.
- Deep idea: CSP’s essence is protocol discipline: what a process can do, refuse, or synchronize on is the contract.
- Discovery method: List events, channels, ready sets, external/internal choice, synchronization points, termination, timeout, and refusal conditions; then check for deadlock or livelock.
- Boundary: Do not use CSP if communication is informal side effects rather than explicit events or channels.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestration problem is best modeled as isolated sequential processes that coordinate by named communication events rather than by directly sharing mutable state.

Strong triggers:
- Multiple agents, workers, tools, or services must run concurrently while preserving clear ownership of state.
- A workflow needs explicit send/receive contracts: who may talk to whom, with what message shape, and when.
- The design has races caused by shared mutable variables, global queues, ad hoc callbacks, or "any worker can update anything."
- Backpressure, bounded buffering, or synchronous handoff matters more than raw throughput.
- A coordinator must choose among several ready inputs, such as the first available tool result, user reply, cancellation, timeout, or resource grant.
- A failure appears as deadlock, orphaned wait, blocked sender, dropped message, unbounded buffer growth, starvation, or unclear shutdown behavior.

Prefer a transaction-processing skill when the hard part is durable commit and recovery. Prefer a Petri-net/resource skill when the hard part is reachability of tokens or resource counts. Use this skill when the hard part is the communication discipline between concurrent processes.

## Activation Gate

Activate only when the primary problem is communication discipline between concurrent sequential processes: explicit send/receive contracts, rendezvous, buffering, guarded choices, backpressure, deadlock, termination, or no shared mutable state. Do not activate for dashboards, pure database transactions, biography/history summaries, or generic queue usage where protocol correctness is not the design problem.

Before executing, identify the process boundary, at least two communicating processes or one process plus an interrupt/cancellation peer, the channels or shared-state conflict, and the expected artifact. If those facts are unavailable, ask one clarifying question or state a minimal assumed protocol.

## Standalone Contract

This skill must be executable from this `SKILL.md` alone. `references/source-notes.md` is provenance/source trace only; do not load it or any external source file for runtime execution. The result should define enough process, channel, and guard information that another agent can test the protocol independently.

## Output Format

Return a compact CSP-style contract with:
- Activation decision: why CSP is active and which nearby skills were ruled out.
- Process table: process id, local state owner, accepted messages, emitted messages, guards, lifecycle, and termination rule.
- Channel map: `source -> destination`, message variants, buffering/rendezvous mode, capacity, ordering, timeout, cancellation, and overflow behavior.
- Synchronization review: matched send/receive checks, guarded-choice policy, fairness rule, and traced deadlock/starvation cycle analysis.
- Verification plan: protocol tests for malformed messages, blocked peers, shutdown, timeout, cancellation, and competing ready inputs.

## Failure, Recovery, and Idempotency

If a protocol step cannot be matched to a sender, receiver, or buffer, mark the contract incomplete and do not pretend it is safe. On re-run, preserve process and channel names where possible, update only the changed protocol edges, and call out new or removed messages. If a repair introduces buffering, record how it affects backpressure and replay of in-flight work.

## Hard Rules

- Do not treat a queue as a rendezvous unless sender/receiver synchronization is explicitly preserved.
- Do not allow shared mutable coordination as an unstated side channel.
- Do not rely on implementation fairness for correctness; encode priority, aging, quota, or round-robin when starvation matters.
- Do not omit termination behavior for blocked senders, blocked receivers, closed inputs, cancellation, and failed peers.

## Workflow

1. Identify the sequential processes.
   - Name each active entity as a process: user session, planner, worker, tool adapter, queue consumer, resource manager, reviewer, scheduler, or external service facade.
   - Give each process one owner for its local state. Other processes may observe or change that state only by sending messages to that owner.
   - Mark each process as finite, long-running, restartable, singleton, replicated, or an indexed array of equivalent workers.
   - Avoid hidden shared variables. If a value is read or mutated by more than one process, either assign one owner process or convert the interaction into explicit messages.

2. Define channel and message contracts.
   - For every interaction, write `source -> destination: message` with payload schema, correlation id, expected reply, timeout, and cancellation behavior.
   - Decide whether the interaction is rendezvous-style, buffered, broadcast, or request/reply. Use rendezvous when backpressure and synchronization are part of correctness.
   - Treat automatic buffering as a design decision, not a default. If buffering is needed, model the buffer as its own process with capacity, ordering, overflow, and shutdown rules.
   - Use typed message variants for commands, queries, results, errors, and end signals. Reject unknown or mismatched messages instead of letting them block invisibly.

3. Replace shared-state coordination with protocol steps.
   - Convert direct reads into queries sent to the owning process.
   - Convert direct writes into commands accepted only when the owner's guard condition is true.
   - For resources such as tools, model endpoints, credentials, budgets, rate limits, and locks as manager processes that grant or deny requests.
   - When multiple clients call one manager, include the caller identity in each message so replies and fairness checks are explicit.

4. Design guarded choices.
   - For each process state, list the input messages it is prepared to accept and the Boolean guards that must hold.
   - When several inputs are ready, specify the selection rule: arbitrary, priority order, oldest-ready, cost-ranked, risk-ranked, or externally scheduled.
   - Never rely on implementation fairness for correctness. If starvation would break the workflow, add quotas, aging, round-robin, or explicit priority rules.
   - Make disabled actions visible: record why a message waits, such as empty buffer, full buffer, missing approval, exhausted budget, or resource unavailable.

5. Check synchronization and deadlock.
   - For every send, identify the matching receive or buffer process. For every receive, identify the possible senders.
   - Trace wait cycles: A waits for B, B waits for C, C waits for A. Break cycles with ordering, a mediator process, a buffer, timeout, cancellation, or protocol redesign.
   - Check common CSP deadlocks: both sides send first, both sides receive first, a process terminates while another still expects it, or a message shape no longer matches the receiver.
   - Add bounded wait behavior for external services and humans: timeout, retry, cancellation, escalation, or explicit "still waiting" state.

6. Specify termination and failure propagation.
   - Define how each process knows its upstreams are finished: explicit `end`, `closed`, `cancel`, `failed`, or `no-more-work` messages.
   - For loops that wait on input from several sources, state whether they terminate when one source closes, all sources close, or a controlling process cancels them.
   - Decide what happens to blocked senders and receivers when a peer terminates.
   - Make shutdown an ordinary protocol path, not an implicit side effect of process death.

7. Produce the orchestration artifact.
   - Output a process table with local state ownership, accepted messages, emitted messages, guards, and termination rules.
   - Output a channel map showing source, destination, buffering, capacity, ordering, and message variants.
   - Include a deadlock/starvation checklist with at least one traced wait-cycle analysis.
   - Include tests or simulations for matched send/receive, backpressure, malformed messages, peer termination, cancellation, timeout, and competing ready inputs.

## Failure Modes

- Sharing mutable state between agents and then adding messages only for notification. CSP-style design requires communication to be the coordination mechanism.
- Treating a queue as equivalent to a rendezvous. Queues decouple sender and receiver; that can hide overload, stale work, and lost backpressure.
- Leaving channel endpoints implicit. If a process can receive from "anyone," replies, authorization, and fairness become ambiguous.
- Ignoring message shape matching. A sender can appear healthy while the receiver waits forever for a different command variant.
- Designing a coordinator that waits on one source while another source must be serviced first to unblock the system.
- Assuming fair scheduling. If one ready input must eventually be selected, encode that rule in the orchestrator.
- Forgetting termination protocol. Closed sources, canceled jobs, failed peers, and drained buffers need explicit messages or state transitions.
- Adding unbounded buffers to avoid blocking. This often converts a synchronization bug into memory growth, stale work, or delayed failure.
- Modeling external services as reliable CSP peers. They need timeouts, retries, idempotency, and fallback states.
- Using synchronous handoff for long-running or human work without a lease, callback, or timeout path.

## Boundaries

CSP is a communication and concurrency discipline. It does not by itself provide durable transactions, crash recovery, schema migration, probabilistic planning, UI design, or business prioritization.

Use synchronous rendezvous only when the handoff itself is part of correctness. For high-latency tools, humans, or remote services, prefer an explicit request/accepted/callback protocol with durable correlation ids.

CSP can describe monitors, buffers, semaphores, and schedulers as processes, but this does not mean every implementation should hand-code them from primitives. Use proven queues, actors, workflow engines, locks, or databases when they provide the needed contract; keep the CSP model as the design and verification frame.

The original CSP paper intentionally used a static process model and noted proof and implementation limitations. In modern auto-orchestrators, dynamic agent creation is acceptable, but each created process still needs a name, owner, channel contract, lifecycle rule, and bounded failure behavior.

## Source Closure

This 20-communicating-sequential-processes skill is self-contained for runtime use; its source basis is CSP sources and local communicating-processes entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
