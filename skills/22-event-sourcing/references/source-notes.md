# Source Notes

## Assigned Sources

- `auto_orchestrator_theory_txt_pack_v2/原文目录/04_左脚_跟踪记录回放/22_事件溯源__Event_Sourcing/01_martinfowler_com.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/04_左脚_跟踪记录回放/22_事件溯源__Event_Sourcing/02_learn_microsoft_com.txt`

## Metadata

- Source 1: "Event Sourcing," Martin Fowler, 12 December 2005, draft material from *Further Enterprise Application Architecture*.
- Source 2: "Event Sourcing Pattern - Azure Architecture Center," Microsoft Learn, updated 2026-04-20 in the provided metadata, with article date 2026-03-27.

The Fowler source defines Event Sourcing as capturing all application state changes as a sequence of events. It supplies the core capabilities used in this skill: complete rebuild, temporal query, replay, event reversal, snapshots/current-state caches, event log versus application state as record, event handler placement, external gateway suppression during replay, external query logging for deterministic rebuild, code-change implications, and accounting-style audit use cases.

The Microsoft Learn source frames event sourcing as an append-only store for the full series of domain actions. It contributes implementation guidance: per-entity event streams, command handlers, CQRS/materialized views, optimistic concurrency, append-only immutability, compensating events, event versioning, tolerant deserialization, upcasting, snapshotting, idempotent handlers, event ordering, event store versus broker distinction, personal-data compliance, and when the pattern is or is not suitable.

## Distillation For Auto-Orchestrators

For auto-orchestrators, Event Sourcing becomes a design pattern for durable execution memory:

- A stream represents a run, task, agent session, resource ledger, approval case, or domain aggregate.
- Events are authoritative orchestration facts, not just logs: accepted commands, decisions, tool lifecycle changes, budget reservations, approvals, cancellations, and compensations.
- Current state, queues, dashboards, search views, and agent-readable context are projections that can be rebuilt.
- Rehydration lets a command handler reconstruct the current state before accepting the next orchestration command.
- Expected stream versions detect concurrent workers racing to update the same run or task.
- Snapshots bound replay cost without replacing the event stream.
- Replays support incident reconstruction, deterministic debugging, parallel testing of new code, projection migration, and retroactive correction.
- External tool calls, notifications, payments, and tickets must be isolated behind gateways so replay does not repeat side effects.
- External query answers that influence orchestration decisions should be persisted or converted into events so future replay sees the original answer.
- Schema evolution must be designed before adoption because immutable event histories constrain later changes.

## Source Constraints And Interpretation

The sources are sufficient for the entry. No external supplement was needed. The Fowler article is explicitly draft material from 2005, so the skill uses it for enduring conceptual mechanics and combines it with the newer Microsoft architecture guidance for current implementation concerns.

The skill intentionally converts enterprise application examples into auto-orchestrator artifacts: stream definitions, command handlers, projections, replay modes, side-effect gateways, idempotency rules, and schema evolution policies.
