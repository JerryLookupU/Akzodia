---
name: 19-actor-model
description: Use when designing or repairing an auto-orchestrator whose agents, tools, workers, schedulers, monitors, or recovery loops should be isolated as actors that communicate through mailboxes, asynchronous messages, event protocols, supervision trees, backpressure, dynamic worker creation, or single-writer local state instead of shared mutable state.
---

# Actor Model

## When To Use

Use this skill when the orchestration problem is mainly about concurrent execution units that need isolated state, message-driven coordination, failure containment, and scalable dispatch.

Strong triggers:
- Multiple agents, workers, tools, or services need to run concurrently without corrupting shared state.
- The design mentions actors, mailboxes, message queues, async dispatch, event protocols, worker pools, supervision, or dynamic worker creation.
- A scheduler, monitor, memory writer, recovery loop, or tool adapter has state that should have one owner and receive commands through a queue.
- Failures should be isolated so one bad worker, stuck tool call, or poisoned task does not collapse the whole orchestrator.
- The system needs backpressure, mailbox limits, priority messages, deadlines, retries, or dead-letter handling.
- A bug appears as message storms, lost replies, duplicate work, unbounded queues, stuck actors, hidden shared state, or workers waiting on each other.

Prefer transaction-processing skills when the hard part is durable commit boundaries or idempotent side effects. Prefer Petri nets when the hard part is formal reachability or resource-token deadlock. Use this skill when the first design move is to split the runtime into state-owning concurrent actors with explicit message contracts.

## Workflow

1. Identify actor boundaries.
   - List every active role in the orchestrator: scheduler, worker, tool adapter, monitor, recovery actor, memory actor, budget actor, approval actor, or user-session actor.
   - Give each actor one owned responsibility and one local state boundary. State that can be changed by many parties should either move behind one actor or become an explicit transactional resource.
   - Avoid "manager" actors that own everything. Split by independent concurrency and failure domains.
   - Mark which actors may be created dynamically per job, per tenant, per tool, per resource shard, or per long-running conversation.

2. Define mailboxes and message contracts.
   - For each actor, specify accepted message types, required fields, correlation ids, causation ids, sender identity, priority, deadline, idempotency key, and expected reply or event.
   - Classify messages as command, event, query, reply, cancellation, timeout, heartbeat, supervision signal, or poison/dead-letter notice.
   - Make message handling atomic at actor level: receive one message, inspect local state, update local state, emit zero or more messages, then finish.
   - Treat message order as local to a mailbox unless the runtime gives stronger guarantees. Do not rely on global ordering across actors.

3. Route state through single writers.
   - Assign every mutable orchestration fact a writer: job status, lease ownership, budget consumption, resource capacity, tool health, memory index, or retry schedule.
   - Other actors request changes by message; they do not mutate the state directly.
   - Use stable ids and version numbers for messages that can be replayed or arrive late.
   - If two actors must coordinate a shared invariant, either introduce a state-owning coordinator actor or use a real transaction boundary.

4. Design concurrency, backpressure, and fairness.
   - Define mailbox capacity, queue selection policy, priority rules, starvation guard, and deadline handling for each hot actor.
   - Add admission control before creating actors or enqueueing work: max active jobs, max per-tool concurrency, tenant quotas, budget ceilings, and circuit breakers.
   - Use pull or credit-based dispatch when workers are heterogeneous or tools have volatile capacity.
   - Detect message storms by limiting fan-out, recursion depth, retry rate, and actor spawning rate.

5. Add supervision and recovery.
   - Define parent/supervisor relationships: who starts an actor, watches it, restarts it, drains its mailbox, escalates failure, or marks work failed.
   - Choose a recovery policy per actor: resume, restart with state reload, stop, replace, quarantine mailbox, or escalate to human review.
   - Persist the minimal state needed for actors whose work must survive process crashes.
   - Send cancellations and timeouts as first-class messages; do not assume a blocked actor will notice shared flags.

6. Specify observability and tests.
   - Expose actor id, mailbox depth, message type, correlation id, handler latency, queue age, retry count, dead-letter count, supervisor action, and downstream messages in traces.
   - Test delayed, duplicated, reordered, expired, and poison messages.
   - Test actor crash before state update, after state update before send, after send before ack, and while holding a resource.
   - Return an executable design contract: actor catalog, mailbox schemas, message protocol, state ownership table, supervision tree, backpressure policy, and failure tests.

## Failure Modes

- Smuggling shared mutable state behind actor APIs. If two actors can mutate the same object, the actor boundary is mostly cosmetic.
- Building one central actor that serializes the whole orchestrator and becomes the bottleneck.
- Treating message send as durable commit. A message in memory, a queue ack, and a business-state transition are different facts.
- Ignoring mailbox growth. Unbounded queues turn overload into latency spikes, memory pressure, and delayed cancellations.
- Relying on synchronous request/reply chains between actors. This recreates distributed call-stack deadlocks and makes failures contagious.
- Assuming messages arrive once, in order, and on time unless the transport explicitly guarantees it.
- Creating actors dynamically without lifecycle limits, ownership, naming, cleanup, or quota controls.
- Restarting actors without idempotency, state reload rules, or fencing against stale completions.
- Letting supervision hide repeated failures. Restart loops need counters, backoff, quarantine, and escalation.
- Using actors for pure data transformations where a simple function, batch job, or workflow step would be clearer.

## Boundaries

Actor modeling is a runtime decomposition discipline for concurrent state-owning components. It does not by itself provide durable transactions, exactly-once side effects, optimal scheduling, security policy, or business prioritization.

The useful invariant is local: an actor owns its state and reacts to messages. Anything crossing actors needs an explicit protocol, delivery assumption, retry rule, and observability trail.

Actors are strongest when work can proceed asynchronously and independently. They are weaker for tightly coupled invariants, global optimization, or workflows whose correctness depends on simultaneous updates across many resources.

This skill complements scheduling, queueing, CSP, Petri-net, and transaction-processing skills. Use Actor Model to decide who owns state and how concurrent components talk; use the other skills to prove resource reachability, tune throughput, or make durable side effects recoverable.
