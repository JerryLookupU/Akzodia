# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Source

- Anand S. Rao and Michael P. Georgeff, "BDI Agents: From Theory to Practice", Proceedings of the First International Conference on Multiagent Systems, AAAI, 1995.

## Distillation

The paper argues that Belief-Desire-Intention agents are useful for complex, dynamic, resource-bounded control domains such as air traffic management, telecommunications, spacecraft, medical services, and business processes. The useful design point is not a generic psychological metaphor. It is a runtime architecture for choosing actions when the environment is nondeterministic, the system has multiple options, objectives can conflict, sensing is partial, and the environment can change while deliberation or execution is underway.

For auto-orchestrator design, the three attitudes map cleanly:

- Beliefs are the mutable information component: current observations, inferred state, tool outputs, constraints, and assumptions.
- Desires are the motivational component: objectives, priorities, payoffs, and requested outcomes, which may conflict.
- Intentions are the deliberative component: the chosen course of action or plan stack retained from the last deliberation cycle.

The important engineering move is the explicit intention state. Recomputing the best action at every step can be too expensive and unstable, while executing a chosen plan to completion can ignore important changes. Intentions let the agent balance reactive behavior and goal-directed persistence.

## Interpreter Pattern

The source gives an abstract BDI interpreter:

1. Initialize state.
2. Generate options from the event queue.
3. Deliberate over options.
4. Update intentions.
5. Execute.
6. Get new external events.
7. Drop successful attitudes.
8. Drop impossible attitudes.
9. Repeat.

The practical version uses dynamic data structures for beliefs, desires, intentions, and an event queue. It recognizes both external and internal events. Plans are selected by invocation conditions and preconditions, then represented as intention stacks that may run, suspend, resume, or terminate.

## Commitment Strategies

The source distinguishes commitment condition from termination condition. It gives three useful behavior families:

- Blindly committed: resist belief or desire changes that conflict with current commitments.
- Single-minded: accept belief changes and drop commitments when they become impossible.
- Open-minded: accept belief and desire changes and drop commitments when the motivating desire no longer applies.

The paper does not prescribe one universal strategy. The strategy must be selected for the application and verified against the required behavior.

## Practical Constraints

The paper explicitly warns that ideal BDI logic is not directly practical as a runtime. Logical closure and theorem-proving procedures can be unbounded and destroy responsiveness. Practical BDI systems constrain representation: current beliefs rather than all temporal belief states, plans rather than arbitrary future-world descriptions, and runtime intention stacks rather than fully enumerated intention-accessible worlds.

For auto-orchestrators, this means BDI should become a fast event-driven execution architecture, not a heavyweight philosophical proof layer.

## Auto-Orchestrator Transfer

Use BDI when an execution center must:

- Track partial and changing runtime observations.
- Maintain several competing objectives.
- Convert events into applicable plan options.
- Commit to selected plan stacks long enough to make progress.
- Reconsider plans at bounded checkpoints when beliefs or desires change.
- Explain to humans why it is continuing, revising, or abandoning a plan.

The paper's OASIS example is especially relevant: the scheduler commits single-mindedly to a landing sequence until aircraft have landed or it no longer believes the next aircraft can meet its assigned time. This is a direct pattern for orchestrators that should not restart a global plan for every small signal but must react when feasibility breaks.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: BDI agent sources and local BDI entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Beliefs describe world state; desires define possible objectives; intentions commit to selected plans under resource limits.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use BDI for simple stateless tool routing or psychological metaphor without executable commitments.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: BDI is useful when action selection must persist despite uncertainty, changing evidence, and competing goals.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: List beliefs, desires, intentions, plan library, commitment strategy, reconsideration triggers, sensing gaps, and conflict handling.
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
