---
name: 01-general-system-theory
description: Use when designing, auditing, or repairing an auto-orchestrator that must decompose complex work by system boundaries, interacting subsystems, inputs, outputs, feedback loops, environment constraints, and control points instead of by a flat linear checklist.
---

# General System Theory for Auto-Orchestrators

## When To Use

Use this skill when the task needs orchestration design across multiple interacting parts:

- Decomposing a broad goal into agents, stages, tools, queues, budgets, or checkpoints.
- Defining what belongs inside the orchestrator and what remains in the external environment.
- Finding missing feedback loops, handoff contracts, observability points, or escalation paths.
- Auditing plans that look locally correct but may fail because subsystems interfere with each other.
- Turning a user request into a control structure with inputs, outputs, state, feedback, and adaptation.

Do not trigger it for simple one-step tasks, isolated code edits, or ordinary summaries where subsystem interaction is not the main risk.

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

## Failure Modes

- Flat decomposition: breaking work into steps without modeling dependencies, shared state, or feedback.
- Boundary leakage: treating external systems, user choices, or model behavior as if they were under direct control.
- Uncontrolled coupling: two subsystems mutate the same artifact, budget, or decision without arbitration.
- No negative feedback: retries, agent spawning, or search expansion continue after the signal says quality is falling.
- Over-centralization: the orchestrator becomes a bottleneck that must inspect every detail instead of relying on typed contracts and local validators.
- False equilibrium: the system looks stable because errors are suppressed, summarized away, or delayed until the final output.
- Misplaced analogy: forcing biological or engineering system language onto a task that only needs a small deterministic procedure.

## Boundaries

This skill is a design and audit lens, not a substitute for domain-specific architecture, security review, product judgment, or implementation testing.

Use it to structure orchestration decisions before choosing concrete frameworks. Once the system map is clear, hand off to narrower skills for API design, testing, frontend implementation, security, deployment, or runtime-specific agent harness work.

The source entry is incomplete: the assigned supplement file is a 404 page. This skill uses the local metadata for the entry and supplemented public context on Ludwig von Bertalanffy's General System Theory. Treat the resulting workflow as a pragmatic GST-derived orchestration heuristic, not a complete representation of the book.
