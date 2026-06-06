---
name: 01-general-system-theory
description: Use when designing, auditing, or repairing an auto-orchestrator that must decompose complex work by system boundaries, interacting subsystems, inputs, outputs, feedback loops, environment constraints, and control points instead of by a flat linear checklist.
source_files:
  - references/source-notes.md
---
# 01 General System Theory

## Book-Derived Essence

- Core framework: Boundary -> elements -> relations -> flows -> feedback -> environment. Treat the task as an open system before decomposing it into actions.
- Deep idea: The most important move is not “break it down”; it is to decide what counts as the system and what belongs to the environment. Bad orchestration often comes from optimizing a part while hiding the coupling that controls the whole.
- Discovery method: Draw the system boundary, then trace every input, output, state store, feedback signal, and environmental constraint. Any output without feedback, subsystem without interface, or constraint outside the boundary is a likely failure point.
- Boundary: Do not use systems language for a small deterministic task with no meaningful coupling, environment, or feedback.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the task needs orchestration design across multiple interacting parts:

- Decomposing a broad goal into agents, stages, tools, queues, budgets, or checkpoints.
- Defining what belongs inside the orchestrator and what remains in the external environment.
- Finding missing feedback loops, handoff contracts, observability points, or escalation paths.
- Auditing plans that look locally correct but may fail because subsystems interfere with each other.
- Turning a user request into a control structure with inputs, outputs, state, feedback, and adaptation.

Do not trigger it for simple one-step tasks, isolated code edits, or ordinary summaries where subsystem interaction is not the main risk.

## Standalone Contract

This skill is self-contained. Use the concepts and workflow below without reading the original source files. `audit.json` is provenance only, and source snapshots are not required for normal execution.

The skill should produce a practical systems map for an orchestration problem: purpose, boundary, subsystems, relationships, flows, feedback loops, controls, failure behavior, and handoff contracts.

## Activation and Execution Gate

Activate only when the request involves at least two interacting subsystems, shared state, feedback, environmental constraints, or control decisions. If the task is a flat checklist, a single code edit, or a historical/literature question, do not use this skill.

Before running the workflow, state the target system and why system-boundary analysis is needed. If the boundary, success signal, or controlled actors are unknown, ask one focused clarification or proceed with a clearly marked provisional boundary.

## Workflow

1. State the system purpose in one sentence.
   - Name the outcome the orchestrator must maintain, not just the tasks it must perform.
   - Identify the beneficiary, success signal, and unacceptable failure state.

2. Draw the boundary.
   - Inside: agents, tools, memory, queues, prompts, policies, budgets, and validators the orchestrator directly controls.
   - Outside: users, external APIs, file systems, model providers, legal or business constraints, and unknown runtime events.
   - Mark any boundary-crossing item as an interface with an owner, input shape, output shape, and failure behavior.

3. List subsystems and relationships.
   - For each subsystem, record role, inputs, outputs, state, dependencies, and authority.
   - Prefer relationship mapping over task listing: dependency, feedback, inhibition, escalation, delegation, transformation, or resource sharing.
   - Flag any subsystem that consumes or changes shared state without an explicit contract.

4. Trace flows.
   - Input flow: what enters, from where, in what format, with what trust level.
   - Work flow: how tasks move between subsystems and how partial results are recombined.
   - Information flow: what each subsystem knows, withholds, summarizes, or persists.
   - Output flow: what is returned, committed, logged, or escalated.

5. Add feedback and control.
   - Define at least one fast feedback loop for local correction and one slower loop for strategic replanning.
   - Attach each loop to a measurable signal, threshold, action, and owner.
   - Include negative feedback for stabilization: stop, retry, narrow scope, ask user, rollback, or route to review.
   - Include positive feedback only when growth is intended and bounded, such as expanding search after evidence quality improves.

6. Check viability under stress.
   - Perturb the system with stale inputs, missing tools, conflicting goals, budget pressure, noisy evidence, and partial failure.
   - Ask whether the orchestrator degrades gracefully, oscillates, deadlocks, duplicates work, or hides uncertainty.
   - Convert each likely failure into a boundary rule, feedback signal, or subsystem contract.

7. Emit an orchestration blueprint.
   - Purpose and boundary.
   - Subsystems with responsibilities and authority.
   - Interface contracts.
   - Feedback loops and stop conditions.
   - Observability points.
   - Known limits and assumptions.

## Output Format

Return a concise orchestration blueprint with these sections:

- `Purpose`: maintained outcome, beneficiary, success signal, and unacceptable failure.
- `Boundary`: inside, outside, interfaces, and ownership.
- `Subsystems`: role, inputs, outputs, state, dependencies, and authority.
- `Flows`: input, work, information, output, and persistence/escalation paths.
- `Feedback and control`: signals, thresholds, actions, owners, and stop conditions.
- `Stress checks`: perturbations tested and design changes made.
- `Limits`: assumptions, unresolved risks, and handoff recommendations.

## Failure Modes

- Flat decomposition: breaking work into steps without modeling dependencies, shared state, or feedback.
- Boundary leakage: treating external systems, user choices, or model behavior as if they were under direct control.
- Uncontrolled coupling: two subsystems mutate the same artifact, budget, or decision without arbitration.
- No negative feedback: retries, agent spawning, or search expansion continue after the signal says quality is falling.
- Over-centralization: the orchestrator becomes a bottleneck that must inspect every detail instead of relying on typed contracts and local validators.
- False equilibrium: the system looks stable because errors are suppressed, summarized away, or delayed until the final output.
- Misplaced analogy: forcing biological or engineering system language onto a task that only needs a small deterministic procedure.

## Failure, Recovery, and Idempotency

If required information is missing, keep the analysis useful by labeling unknowns and producing a provisional system map rather than inventing hidden contracts. If subsystems conflict over state, authority, or feedback ownership, stop optimizing and first define an arbitration or escalation rule.

On re-run, preserve stable subsystem and interface names when possible, update changed assumptions explicitly, and report what changed since the prior blueprint. Repeated execution should refine the same system map, not create unrelated decompositions.

## Hard Rules

- Do not model environment actors, user choices, external APIs, or model behavior as directly controlled by the orchestrator.
- Do not emit a task list without boundary, subsystem, flow, and feedback analysis.
- Do not recommend unlimited retries, unbounded agent spawning, or positive feedback without a stop condition.
- Do not hide uncertainty; mark provisional assumptions and the signal that would retire them.

## Boundaries

This skill is a design and audit lens, not a substitute for domain-specific architecture, security review, product judgment, or implementation testing.

Use it to structure orchestration decisions before choosing concrete frameworks. Once the system map is clear, hand off to narrower skills for API design, testing, frontend implementation, security, deployment, or runtime-specific agent harness work.

Distillation note: the source entry was incomplete because the assigned supplement file was a 404 page. The runtime guidance above is self-contained and should be treated as a pragmatic GST-derived orchestration heuristic, not a complete representation of the book.

## Source Closure

This 01-general-system-theory skill is self-contained for runtime use; its source basis is Ludwig von Bertalanffy, General System Theory; local theory-pack system entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
