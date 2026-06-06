# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Assigned Source

The assigned file is an official project/book page snapshot, not a chapter-length theory excerpt. It identifies the book, authors, publisher, official links, and central framing around integrating planning, acting, and learning for autonomous intelligent systems.

## Supplemented Metadata

- Title: *Acting, Planning, and Learning*
- Authors: Malik Ghallab, Dana Nau, Paolo Traverso
- Publisher: Cambridge University Press
- Year: 2025
- Official BibTeX confirms: `@book{ghallab2025acting, title={Acting, Planning, and Learning}, author={Ghallab, Malik and Nau, Dana and Traverso, Paolo}, year={2025}, publisher={Cambridge University Press}}`

## Distilled Operating Ideas

Automated planning becomes useful for an auto-orchestrator when work cannot be represented safely as a static task list. The orchestrator needs a state model, goal conditions, actions with preconditions and effects, observation paths, and a loop that compares expected effects with actual outcomes.

The official source frames the book around combining planning, acting, and learning. For orchestration design, that maps to three runtime duties:

- Planning: choose actions or policies that can reach explicit goal conditions from the current state.
- Acting: execute through guarded actions whose preconditions, effects, and risks are known.
- Learning: update action models, method choices, and cost estimates from execution evidence without violating hard constraints.

The generated skill uses common automated-planning distinctions as execution choices:

- Forward state-space planning for reliable current-state reasoning.
- Backward reasoning for crisp goal-to-action derivation.
- Partial-order planning to preserve independent work and concurrency.
- Hierarchical task network planning for reusable expert procedures.
- Temporal/resource planning when time, capacity, or cost constraints dominate.
- Contingent or policy planning when observations determine the next action branch.

## Auto-Orchestrator Translation

For an AI orchestration system, a planner should not output only a numbered plan. It should output a plan trace:

- current-state assumptions,
- goal conditions,
- action operators,
- causal links from effects to later preconditions,
- threats and resource conflicts,
- sensing steps for unknown facts,
- replanning triggers,
- approval gates for risky actions.

This is the practical difference between task decomposition and automated planning: task decomposition describes work; planning reasons about which action is valid next in a changing state.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Automated Planning sources and local planning-theory entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: State + goal + actions + preconditions + effects + search + execution feedback. Planning is choosing action sequences under observable change.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use automated planning for a static checklist with no state transition, alternative action, or replanning need.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The key distinction is between a plan as a search product and execution as a monitored loop. A plan that cannot sense violations is only a wish.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Define state variables and goal tests, enumerate operators with preconditions/effects, choose decomposition/search style, then specify observation and replanning triggers.
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
