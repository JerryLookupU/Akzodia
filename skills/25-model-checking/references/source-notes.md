# Source Notes

## Manifest Item

- Entry id: 25
- Skill name: `25-model-checking`
- Title: 模型检测 / Model Checking
- Primary source file: `auto_orchestrator_theory_txt_pack_v2/原文目录/04_左脚_跟踪记录回放/25_模型检测__Model_Checking/supplement_model_checking_rwth_intro.txt`

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
