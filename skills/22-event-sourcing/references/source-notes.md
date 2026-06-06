# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
Runtime note: this file is provenance/source trace only. The executable skill contract and required operating knowledge are contained in `../SKILL.md`; do not require external source files, webpages, source reports, or original texts at runtime.

## Assigned Sources

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

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Event Sourcing sources and local event-sourcing entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Persist facts as append-only events; rebuild state through projections; commands decide, events record.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not event-source data whose history has no audit, rebuild, temporal, or integration value.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Event sourcing’s power is historical reconstruction: state is not merely stored, it is explainable and replayable.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Separate command intent from event fact, define aggregate boundary, event schema, projection rebuild, idempotency key, snapshot point, and replay risk.
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
