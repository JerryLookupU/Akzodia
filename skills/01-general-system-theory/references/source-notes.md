# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Entry

- Entry id: 01
- Chinese title: 系统论
- English title: General System Theory
- Representative work: Ludwig von Bertalanffy, *General System Theory: Foundations, Development, Applications*
- Local metadata note: use the theory to view tasks as wholes composed of elements, relationships, boundaries, inputs, outputs, and feedback; avoid only linear task decomposition.

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Supplemented Context

- Publisher metadata listed the representative book as *General System Theory: Foundations, Development, Applications* by Ludwig von Bertalanffy.
- Public ISSS/system-science context supports treating systems as organized wholes whose parts are understood through relationships, boundaries, environments, and feedback rather than isolated components.
- The local metadata's intended use was prioritized over broad historical summary: this skill is for auto-orchestrator decomposition, subsystem contracts, and feedback-control design.

## Distilled Concepts For Orchestrator Work

- System: a purposeful whole made of interacting elements.
- Boundary: the distinction between controlled internals and external environment.
- Subsystem: a component with role, state, inputs, outputs, and authority.
- Interface: a boundary crossing with a contract and failure behavior.
- Feedback: information from results or state changes used to correct or adapt future action.
- Negative feedback: stabilizing control that narrows, stops, retries, or escalates.
- Positive feedback: amplifying control that expands effort only when bounded and intended.
- Viability: the orchestrator keeps useful behavior under perturbation rather than succeeding only in the nominal path.

## Distillation Notes

The skill avoids treating GST as a generic philosophy summary. It turns the entry into a repeatable design workflow:

1. Define purpose.
2. Draw boundaries.
3. Map subsystems and relationships.
4. Trace flows.
5. Install feedback and control loops.
6. Stress the system.
7. Emit an orchestration blueprint.

No long source quotations were used because the provided source content was unavailable and the user requested concise paraphrase.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Ludwig von Bertalanffy, General System Theory; local theory-pack system entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Boundary -> elements -> relations -> flows -> feedback -> environment. Treat the task as an open system before decomposing it into actions.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use systems language for a small deterministic task with no meaningful coupling, environment, or feedback.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The most important move is not “break it down”; it is to decide what counts as the system and what belongs to the environment. Bad orchestration often comes from optimizing a part while hiding the coupling that controls the whole.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Draw the system boundary, then trace every input, output, state store, feedback signal, and environmental constraint. Any output without feedback, subsystem without interface, or constraint outside the boundary is a likely failure point.
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
