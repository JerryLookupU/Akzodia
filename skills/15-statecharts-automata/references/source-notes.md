# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Bibliographic Grounding

- Entry: `15 状态机 / Statecharts / Automata`.
- Main representative source: David Harel, "Statecharts: a visual formalism for complex systems", *Science of Computer Programming*, 8(3), 231-274, June 1987. DOI: `10.1016/0167-6423(87)90035-9`.
- The entry metadata also names Michael Sipser, *Introduction to the Theory of Computation*, as representative automata background, but the assigned local source files only provide Harel statecharts material and publication metadata.

## Extracted Ideas For Auto-Orchestrator Design

Harel frames reactive systems as event-driven systems whose behavior is best understood as allowed sequences of events, conditions, actions, and timing constraints. Auto-orchestrators fit this class: they react to tool results, user approval, budget changes, dependencies becoming ready, retries, and cancellation.

Conventional flat state diagrams are useful but break down for complex systems because they become large, repetitive, and hard to review. Statecharts add three practical mechanisms:

- Hierarchy: cluster substates into superstates and attach shared transitions to the superstate.
- Orthogonality/concurrency: split a state into parallel regions so independent dimensions do not create a Cartesian explosion of flat states.
- Communication: transitions can emit actions/events that trigger behavior elsewhere, including across concurrent regions.

Important statechart concepts mapped to orchestration:

- State transition: "when event occurs in state, if guard holds, perform action and enter target state."
- Superstate: a lifecycle group such as `active` containing `ready`, `running`, `blocked`, and `retrying`.
- Default entry: the substate chosen when entering a compound state without a more specific target.
- History entry: re-enter the last active substate when restoration is intentional.
- Orthogonal product: simultaneous state across regions, such as execution state plus budget state plus approval state.
- Action: instantaneous effect such as persisting a transition, emitting an event, or enqueueing work.
- Activity: durable work such as a tool call, timer, or worker process; it needs explicit start and stop.
- Formal next-step semantics: from a current configuration plus current events and conditions, compute the next valid configuration, including internally generated events, until stable.

## Design Implications

Use statecharts to keep orchestration behavior inspectable:

- Put global events like cancellation, budget exhaustion, or fatal error at the highest superstate where they apply.
- Use guards for policy checks rather than duplicating policy states.
- Use parallel regions for independent dimensions and explicit events for synchronization.
- Treat nondeterminism as a bug unless the runtime explicitly resolves it.
- Review the statechart as an executable contract: states, events, guards, actions, activities, invariants, and transition tests.

## Source Completeness Notes

The assigned text file `01_www_weizmann_ac_il.txt` contains only page markers and no extracted article body. The local PDF at the same source path was image-only for embedded text extraction, so selected pages were OCRed locally with Tesseract to recover the paper's core concepts. The second assigned source file provides complete publication metadata and abstract text.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Statecharts and automata sources; local state-machine entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: States + events + guards + actions + hierarchy + orthogonal regions + history. Behavior is legal transition structure.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not build a state machine when behavior is purely data transformation with no persistent mode.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Statecharts compress complex reactive behavior by separating mode, event, guard, and action, while hierarchy prevents state explosion.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Name stable modes, events that can arrive, guards that make them valid, side effects of transitions, parallel regions, terminal states, and illegal-event handling.
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
