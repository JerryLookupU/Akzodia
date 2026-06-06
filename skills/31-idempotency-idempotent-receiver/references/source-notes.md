# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Metadata

- Entry id: 31
- Title: 幂等理论 / Idempotency / Idempotent Receiver
- Skill name: `31-idempotency-idempotent-receiver`

## Source Basis

The provided source is the Enterprise Integration Patterns page for **Idempotent Receiver**, whose core problem is that a receiver may observe the same message more than once even when the sender intended to send it once.

Core claims distilled:

- A receiver should be designed so receiving the same message multiple times is safe.
- In messaging, idempotency means the message has the same effect whether processed once or many times.
- The source identifies two primary approaches:
  - explicit de-duplication by removing duplicate messages;
  - message semantics that are naturally idempotent.
- Related pattern context includes Command Message, Guaranteed Delivery, Messaging, and Resequencer.

## Supplemented Theory Metadata

The source file contains enough pattern text to identify the theory and executable design implications, but it is a short web excerpt rather than the full book chapter. Supplemented metadata used for distillation:

- Primary domain: enterprise integration, message endpoints, distributed workflow recovery.
- Auto-orchestrator mapping: queue redelivery, retry loops, webhooks, tool timeouts, checkpoint restore, external side effects, and finalization.
- Key design translation: duplicate safety must live at the receiver/effect boundary, not only in the sender or broker.

## Distillation Notes

For auto-orchestrators, the practical unit is not only a message endpoint. The receiver can be a worker step, tool adapter, webhook handler, sink writer, run finalizer, or recovery worker. The skill therefore turns the EIP pattern into a concrete design workflow:

1. identify the duplicate boundary and business identity;
2. classify operations as naturally idempotent or unsafe;
3. persist a stable idempotency key and result state;
4. define behavior for completed, pending, retryable, terminal, and mismatched states;
5. test crash, redelivery, timeout, and concurrent duplicate cases.

## Auto-Orchestrator Heuristic

If a step can be retried automatically and has any external side effect, require one of:

- semantic idempotency through a stable target state;
- durable deduplication with a stable idempotency key;
- downstream idempotency support using the same key;
- a transaction, outbox, reconciliation, or compensation design.

Without one of these, retries and recovery must be gated by human review or an explicit risk acceptance.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Idempotent Receiver pattern sources and local idempotency entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Stable operation identity + duplicate detection + state-specific response + side-effect reconciliation.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not claim idempotency when side effects happen before the duplicate record is durable.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Idempotency is not “do it twice safely” in the abstract; it is a contract for what repeated messages mean at each state boundary.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Find retry boundaries, idempotency keys, durable duplicate store, external side effects, retention windows, and response behavior for completed/failed/in-flight states.
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
