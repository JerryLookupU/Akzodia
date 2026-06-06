---
name: 25-model-checking
description: Use when designing, reviewing, or hardening an auto-orchestrator by formally checking whether all reachable workflow states satisfy precise properties such as no deadlock, bounded response time, invariant preservation, safe retries, valid compensation, liveness, fairness, and absence of unsafe concurrent interleavings.
source_files:
  - references/source-notes.md
---
# 25 Model Checking

## Book-Derived Essence

- Core framework: Finite model + temporal property + exhaustive state exploration + counterexample trace.
- Deep idea: Model checking turns “seems safe” into “no reachable bad state under this model,” and its best artifact is often the counterexample.
- Discovery method: State variables, transitions, fairness assumptions, safety/liveness properties, and abstraction boundaries; run the model mentally or formally to seek shortest counterexample.
- Boundary: Do not overclaim beyond the abstraction; model checking proves properties of the model, not the whole messy system.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestrator design has finite or abstractable states and the question is: "Can this bad state happen, or does this required property hold across all reachable executions?"

Strong triggers:
- You need to verify workflow control logic, state machines, agent handoffs, retry loops, compensation paths, locks, queues, or concurrent tool calls.
- You need confidence beyond simulation, sampling, unit tests, or likely happy paths.
- You suspect a race condition, deadlock, livelock, starvation, missed response, unsafe rollback, duplicate side effect, or impossible terminal state.
- You can express the system as a finite behavioral model, transition system, Promela/TLA+/NuSMV/UPPAAL-style model, bounded state graph, or executable abstract model.
- You need a counterexample trace that shows exactly how a violation can occur.
- You are deciding what invariants and temporal properties the orchestrator must enforce at runtime.

Prefer ordinary testing when the behavior is data-heavy, continuous, poorly abstracted, or the user only needs examples of failures. Prefer theorem proving when the system is better represented as mathematical theory than finite behavior. Pair with testing because model checking verifies the model, not the deployed realization.

Do not trigger for generic testing, log analytics, product requirements, implementation debugging without a finite state abstraction, or textbook summaries that do not require a checkable model.

## Standalone Contract

This skill must provide model-checking guidance without requiring the original source material. Do not load or depend on external files, webpages, original books, source reports, external source folders, or source-pack material at runtime. Use `references/source-notes.md` only as optional local provenance, not as an execution dependency.

The expected result is a verification package: target boundary, finite abstraction, explicit assumptions, properties, model/checker choice, run limits, result summary, counterexample traces when present, design changes, and complementary implementation tests.

## Activation And Execution Gate

Activate only when all of these are true:
- The user asks to verify reachable behavior, invariants, temporal properties, deadlock/liveness, or counterexample traces.
- The system can be represented as finite states or a deliberately bounded abstraction.
- The work concerns orchestrator control behavior, protocols, retries, recovery, scheduling, or concurrent interleavings.

Before running or proposing a check, confirm:
- The target boundary and state variables are named.
- At least one safety, reachability, liveness, fairness, or bounded-time property is precise enough to check.
- The abstraction limits, bounds, and excluded behaviors are explicit.

If any gate item is missing, ask for the missing item or produce a bounded modeling plan instead of claiming verification.

## Workflow

1. Define the verification target.
   - Name the orchestrator boundary: workflow template, task planner, scheduler, queue worker, agent handoff, tool transaction, state reducer, retry policy, or recovery subsystem.
   - Identify why exhaustive checking matters: safety-critical side effects, expensive failures, concurrency, unbounded retries, hard deadlines, or subtle state transitions.
   - Separate verification from validation: model checking asks whether the design satisfies stated properties, not whether the product goals are the right goals.

2. Build a finite behavioral model.
   - Represent states, variables, actors, messages, locks, timers, queues, retries, terminal outcomes, and external callbacks at the smallest useful abstraction.
   - Keep control behavior explicit: enabled actions, guards, state updates, nondeterministic choices, parallel processes, timeouts, and failure events.
   - Abstract data values into finite categories such as `empty/non_empty`, `valid/invalid`, `fresh/stale`, `authorized/unauthorized`, or bounded counters.
   - Preserve behavior that can affect the property. Do not abstract away ordering, atomicity, retry counts, cancellation, or compensation when those are relevant.
   - Run a few simulations or trace walks first as a sanity check before trusting the model checker.

3. Formalize properties before running checks.
   - Write safety invariants: "nothing bad ever happens", such as no negative inventory, no duplicate irreversible tool call, no two owners for one exclusive task, or no success without validation.
   - Write reachability checks: "can this state be reached", such as deadlock, cancelled-and-charged, completed-without-artifact, or human-approval-skipped.
   - Write liveness and response properties: "something good eventually happens", such as every accepted task eventually completes, escalates, or times out.
   - Write bounded-time properties when deadlines matter: response within N minutes, retry budget exhausted within N attempts, or cancellation observed before next side effect.
   - Make every property precise enough to be checked. Ambiguous requirements must be rewritten before verification.

4. Run the model check.
   - Choose a checker or bounded exhaustive search that fits the model style. Use SPIN/Promela, TLA+, NuSMV, UPPAAL, Alloy, custom state exploration, or a repo-local verification harness when available.
   - Explore all reachable states within the declared abstraction and bounds.
   - Record the state count, depth, bounds, fairness assumptions, excluded behaviors, and any reductions used to fit memory.
   - If the checker exhausts memory or time, reduce the model deliberately: smaller domains, symmetry, partial-order reduction, tighter bounds, compositional checks, or property-specific abstraction.

5. Analyze results as design evidence.
   - If a property is satisfied, state the model and bounds under which it was satisfied, then check the next high-value property.
   - If a property is violated, replay the counterexample as an execution trace with actors, state changes, tool calls, messages, and decision points.
   - Classify the source: model bug, bad property, missing assumption, real design flaw, unsafe interleaving, insufficient atomicity, missing guard, or incomplete recovery path.
   - Do not patch the property to make the violation disappear unless the requirement was actually wrong.

6. Feed findings back into orchestrator design.
   - Convert violations into concrete changes: atomic sections, guards, idempotency keys, lock ordering, compensation rules, timeout transitions, retry caps, state-machine constraints, or scheduler fairness.
   - Convert checked properties into runtime assertions, conformance checks, CI verification cases, monitors, or release gates.
   - Keep counterexample traces as regression scenarios for simulation, integration tests, and process mining.
   - Repeat the model, property, check, analysis loop until high-risk properties are covered or the remaining risk is explicit.

7. Report with verification limits.
   - Include the target model, property list, satisfied/violated results, counterexamples, state-space size, bounds, assumptions, reductions, and unresolved risks.
   - Distinguish facts proven about the model from inferences about the deployed orchestrator.
   - Recommend complementary tests for model-to-implementation drift.

## Output Format

Return:
- `target`: orchestrator boundary and why exhaustive checking is justified.
- `model`: state variables, actors, transitions, nondeterminism, bounds, and abstractions.
- `properties`: safety/reachability/liveness/timing properties in checkable form.
- `checks`: checker or search method, state count/depth if known, reductions, and assumptions.
- `results`: satisfied properties, violations, counterexample trace, and classification of each issue.
- `design_feedback`: required guards, atomicity, idempotency, compensation, fairness, runtime assertions, and regression tests.
- `limits`: what the model does not prove about the deployed system.

## Failure, Recovery, And Idempotency

If the state space explodes, reduce only with a stated rationale and re-check that the reduced behavior still preserves the property under review. If the model or property is ambiguous, pause verification and refine it rather than treating an ambiguous pass as evidence.

Repeated runs should be idempotent: preserve property IDs, model version, bounds, assumptions, and counterexample IDs so results can be compared across iterations. When a violation is fixed, keep the original trace as a regression scenario.

## Failure Modes

- Treating model checking as testing and only exploring likely or manually chosen scenarios.
- Modeling the happy path while omitting failures, retries, cancellation, races, external callbacks, or nondeterministic scheduling.
- Stating properties in vague business language instead of precise invariants, reachability, liveness, or timing constraints.
- Trusting a satisfied property without documenting bounds, abstractions, assumptions, and reductions.
- Ignoring counterexamples because they look unlikely. Model checking is valuable precisely because it is not biased toward probable scenarios.
- Overfitting the model to avoid state explosion and accidentally removing the dangerous behavior.
- Forgetting that a verified model is only as good as the model-to-implementation correspondence.
- Using model checking for data-centric correctness that would be better handled with tests, type systems, contracts, or theorem proving.

## Boundaries

Model checking is strongest for finite, control-intensive behavior: workflows, protocols, concurrent processes, state machines, schedulers, retries, and temporal requirements.

It is weaker for unbounded data transformations, fuzzy policy decisions, statistical model quality, open-ended natural language reasoning, or behavior that cannot be abstracted without losing the property under review.

The result does not validate product intent. It verifies whether the modeled system satisfies the formalized properties.

Model checking should complement implementation testing, simulation, runtime monitoring, and process mining. Use tests to ensure the deployed system matches the model, and use logs to discover behaviors the model omitted.

## Hard Rules

- Do not claim a property is proven without naming the model, bounds, fairness assumptions, and exclusions.
- Do not remove failures, retries, ordering, cancellation, or side effects from the model when they affect the property.
- Do not convert a real counterexample into an assumption unless the requirement or scope is explicitly changed.
- Do not present model-checking results as validation of product intent or deployed implementation correctness.

## Source Closure

This 25-model-checking skill is self-contained for runtime use; its source basis is Model checking and formal-methods local supplement entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
