# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Item

- Entry id: 25
- Skill name: `25-model-checking`
- Title: 模型检测 / Model Checking

## Source Basis

The manifest source is an introductory Model Checking lecture by Joost-Pieter Katoen, RWTH Aachen, dated April 3, 2007. It frames model checking as a formal verification technique for checking whether a finite behavioral model satisfies a formal property.

The lecture distinguishes verification from validation: verification checks whether the system is built correctly against qualitative requirements, while validation checks whether the right system is being built. It positions model checking among peer review, testing, simulation, model-based testing, and deductive methods.

Key source points used for this skill:
- Formal methods help integrate verification earlier in design and can offer higher coverage than ordinary testing.
- Model-based verification starts from a model; verification quality depends on model quality.
- Model checking systematically checks a property in all states of a finite behavioral model.
- Typical properties include result correctness, deadlock reachability, bounded deadlock occurrence, and bounded response time.
- Properties must be precise and unambiguous, often stated in temporal logic.
- The process is modeling, running, and analysis: model the system, sanity-check by simulation, formalize the property, run the checker, analyze satisfied or violated properties, inspect counterexamples, refine the model/design/property, and repeat.
- A property violation should produce a counterexample trace that can be simulated and analyzed.
- Model checking is not biased toward the most probable scenarios, unlike ordinary testing and simulation.
- Limitations include state-space explosion, model quality dependency, reduced fit for data-oriented applications, and limited guarantees about generalizations.

## Distilled Operating Model

For auto-orchestrator design, model checking becomes an exhaustive control-flow verification loop:

1. Choose a high-risk orchestrator boundary such as scheduler, workflow state machine, retry policy, handoff, tool transaction, or compensation flow.
2. Build a finite behavioral model with states, transitions, guards, actors, concurrent processes, timers, failures, retries, and external callbacks.
3. Formalize requirements as safety invariants, reachability questions, liveness requirements, fairness assumptions, or bounded response properties.
4. Run a model checker or bounded exhaustive search over all reachable states within the declared abstraction.
5. Treat satisfied properties as scoped evidence, not universal proof of the deployed system.
6. Treat violations as counterexample traces to replay, classify, and convert into design changes.
7. Repeat after refining the model, property, or orchestrator design.

## Key Concepts For The Skill

- Finite-state model: an abstract behavioral model with a bounded state space.
- Formal property: a precise condition to check, often safety, reachability, liveness, fairness, or timing.
- Safety invariant: a property stating that a bad state never occurs.
- Reachability: whether a specific state can occur.
- Liveness: whether a desired event eventually occurs.
- Deadlock: a state where progress halts because no valid transition can continue.
- Counterexample: a concrete trace showing how a property can be violated.
- State-space explosion: the rapid growth of possible states, often requiring abstraction or reduction.
- Model quality: the principle that verification is only as good as the system model.

## Adaptation Notes

The source lecture is general formal-verification material, not auto-orchestrator-specific. This skill narrows the theory to actionable orchestrator design work:

- It emphasizes control-intensive orchestration risks: concurrent agents, queues, tool calls, locks, retries, cancellation, compensation, deadlines, and terminal states.
- It treats counterexamples as design artifacts that feed into guards, atomicity, idempotency, fairness, runtime monitors, and regression tests.
- It keeps testing as a complement because model checking verifies models rather than deployed realizations.
- It avoids generic educational exposition and focuses on when and how an agent should apply model checking during architecture, debugging, and reliability hardening.

## Metadata Supplement

The manifest supplied the skill name, title, directory, and source file. No additional external source was required. The source is a lecture supplement rather than a full book chapter, so the distillation supplements book/theory metadata from the manifest title fields and adapts the lecture content into auto-orchestrator terminology.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Model checking and formal-methods local supplement entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Finite model + temporal property + exhaustive state exploration + counterexample trace.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not overclaim beyond the abstraction; model checking proves properties of the model, not the whole messy system.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Model checking turns “seems safe” into “no reachable bad state under this model,” and its best artifact is often the counterexample.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: State variables, transitions, fairness assumptions, safety/liveness properties, and abstraction boundaries; run the model mentally or formally to seek shortest counterexample.
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
