# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Item

- id: 32
- title: Saga / 补偿事务 / Compensating Transaction
- skillName: 32-补偿事务-compensating-transaction
- assigned source files:

## Source Status

The assigned sources are complete enough for this local skill. They include current Microsoft Learn pages for the Saga and Compensating Transaction patterns, a microservices.io Saga pattern page, and local metadata that maps the pattern to auto-orchestrator recovery: long transactions across multiple tools or services should register both forward actions and compensation actions.

No external source supplementation was required. The source set covers:

- Saga as a sequence of local transactions across services.
- Compensating transactions as domain-specific undo or repair actions.
- Choreography and orchestration as coordination styles.
- Compensable, pivot, retryable, and irreversible transaction categories.
- Eventual consistency, lack of distributed ACID isolation, and common saga anomalies.
- The need for idempotent compensation, durable progress records, monitoring, retries, dead-letter/manual recovery, and human review for ambiguous cases.

## Distilled Principles

A saga is not a rollback mechanism in the ACID sense. It is a design contract for a long-running operation that commits local work step by step and still needs to reach a valid final state when later work fails.

The central auto-orchestrator translation is: every meaningful forward action that can escape the process should have a recorded recovery strategy before the orchestrator treats the step as complete. That strategy might be compensation, retry, substitution, manual review, or acceptance that the step is the pivot point.

Compensation is application-specific. It often means "make the business situation valid again," not "restore every record to the exact previous value." This matters when concurrent workflows, customers, providers, or operators have changed the same resource after the original step.

Saga design therefore starts with step classification:

- Compensable steps can be repaired or undone by an explicit command.
- Pivot steps define the point of no return or commitment boundary.
- Retryable steps after the pivot must eventually complete and should be idempotent.
- Irreversible steps need late placement, stronger validation, or human approval.

Retry and alternative forward progress should be considered before compensation. The Microsoft compensating transaction source emphasizes that a single step failure does not always require canceling the whole operation; a substitute path or human decision may be better.

The choice between choreography and orchestration is a control problem. Choreography can keep simple flows decentralized, but complex auto-orchestrator flows usually need explicit state, inspectability, recovery, and operator intervention. That pushes toward orchestration or at least a clearly modeled saga state machine.

Reliable sagas require durable coordination data. The orchestrator should record the forward step, compensation command, idempotency key, correlation id, external transaction id, timeout, result, and retry/dead-letter state. Logs alone are not enough.

Saga isolation is weaker than local ACID isolation. Designers must address dirty reads, lost updates, fuzzy reads, and concurrent saga conflicts using semantic locks, pending states, version checks, rereads, commutative updates, operation logs, or risk-based stronger coordination.

## Auto-Orchestrator Translation

Use the source material as a design checklist:

1. Name the saga boundary and valid terminal states.
2. Decompose the operation into durable local transactions.
3. Attach a recovery strategy to each forward step before implementation.
4. Identify compensable, pivot, retryable, and irreversible steps.
5. Select orchestration or choreography based on complexity, inspectability, and recovery needs.
6. Prefer retry or alternate forward path for transient and substitutable failures.
7. Trigger compensation only when forward progress is invalid, exhausted, canceled, or unsafe.
8. Persist compensation records, idempotency keys, external transaction ids, and audit state.
9. Make both forward and compensation commands duplicate-safe.
10. Test failure after every step, crash during compensation, duplicate messages, and manual review paths.

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Metadata Supplement

No metadata supplementation was required. The manifest provided the target name, skill directory, source files, source type, representatives, and usage note; the assigned source files supplied enough theory and implementation context to distill an executable auto-orchestrator design skill.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Saga and Compensating Transaction pattern sources; local recovery entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Saga boundary, local transactions, compensable/pivot/retryable steps, orchestration/choreography, and semantic undo.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use compensation where stronger validation, reservation, or atomicity is required before an irreversible action.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Compensation is not inverse ACID rollback; it is domain repair that brings the business situation back to an acceptable state.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Classify each step as compensable, pivot, retryable, or irreversible; record forward action, compensation, idempotency key, timeout, and manual review path.
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
