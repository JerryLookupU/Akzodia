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

- Book title: *Communicating Sequential Processes*
- Author: C. A. R. Hoare
- Publisher: Prentice Hall International
- Publication year: 1985
- Related paper: "Communicating Sequential Processes," C. A. R. Hoare, *Communications of the ACM*, Volume 21, Number 8, August 1978.

The Oxford source supplies the book metadata and describes CSP as a language for patterns of interaction supported by mathematical theory, proof tools, and literature. It frames the book as an introduction to both the language and the theory for specification, design, and implementation of continuously interacting computer systems.

The CMU source is the 1978 CACM paper text. It gives the operational basis used for this skill: input and output as programming primitives, parallel composition of sequential processes, explicit source/destination naming, no communication through global-variable updates, synchronous communication without automatic buffering, input guards, arbitrary selection among ready guarded alternatives, termination behavior for repetitive commands, and deadlock risk when corresponding input/output commands cannot meet.

## Distillation For Auto-Orchestrators

CSP maps well onto auto-orchestrator design when agents and tools should be treated as independent state owners connected by explicit protocol events:

- A process becomes an agent, worker, service facade, resource manager, scheduler, or tool adapter.
- Local process state becomes owned state that other participants must access by message.
- CSP input/output commands become channel contracts: sender, receiver, payload type, reply, timeout, and termination behavior.
- Synchronous communication becomes rendezvous, backpressure, or request/accepted handoff.
- Input guards become accept conditions for commands, such as resource availability, buffer capacity, budget, approval, or valid state.
- Alternative guarded commands become orchestrator choice among ready events.
- Deadlock analysis becomes wait-cycle analysis across agents, tools, queues, buffers, and resource managers.
- CSP's caution about fairness becomes an explicit scheduling requirement: correctness must not depend on a runtime "probably" choosing a ready input eventually.

## Source Constraints And Interpretation

The skill paraphrases the sources rather than summarizing the full language. The 1978 paper states that the proposed notation is partial and omits proof method and efficient implementation. For auto-orchestrators, this means CSP should be used as a design and verification lens for communication contracts, not as a demand to implement every queue, lock, monitor, or scheduler from primitive synchronous sends.

No external supplement was needed. The assigned sources contained enough metadata and source content for the entry.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: CSP sources and local communicating-processes entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Processes synchronize through events/channels; traces, choices, refusal, and parallel composition define behavior.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use CSP if communication is informal side effects rather than explicit events or channels.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: CSP’s essence is protocol discipline: what a process can do, refuse, or synchronize on is the contract.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: List events, channels, ready sets, external/internal choice, synchronization points, termination, timeout, and refusal conditions; then check for deadlock or livelock.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

zvous, backpressure, guarded choices, no shared mutable state, deadlock analysis, termination signals, or channel contracts.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
