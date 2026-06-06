---
name: 02-artificial-systems-design-theory
description: Use when designing, diagnosing, or evaluating an auto-orchestrator as a goal-directed artificial system: map preferred outcomes, outer environment constraints, inner mechanisms, interfaces, task decomposition, adaptation loops, and bounded-rationality tradeoffs.
source_files:
  - references/source-notes.md
---
# 02 Artificial Systems / Design Theory

## Book-Derived Essence

- Core framework: Inner environment / outer environment / interface / purpose. Design is search through possible artifacts under bounded rationality.
- Deep idea: An artificial system is judged by fit: does its internal structure mediate between purpose and environment? The skill should discover the interface where a better artifact can change the situation.
- Discovery method: Name the desired state, the current environment, and the artifact interface. Then ask what constraints are real, what are design choices, and what satisficing threshold is enough to move forward.
- Boundary: Do not turn it into generic brainstorming; use it when the artifact, environment, and fitness criterion can be named.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the work is not just explaining an existing system, but designing an artifact that should change an existing situation into a preferred one. It is especially useful for auto-orchestrators, agent runtimes, workflow engines, task routers, planner/executor systems, tool policies, and evaluation loops.

Trigger on requests such as:

- Design or refactor an orchestrator, planner, routing layer, task decomposition policy, or agent control loop.
- Diagnose why a system behaves poorly in a specific environment despite plausible internal logic.
- Turn broad goals into a bounded architecture, feedback loop, and verification plan.
- Decide whether to adapt the inner mechanism, the outer environment, or the interface between them.

For provenance, use `audit.json`; normal execution must not require reading the original source files.

## Standalone Contract

This skill is self-contained. It applies Herbert Simon-style artificial-systems design ideas to orchestration work without requiring the user or agent to read source material.

The skill should transform a purposeful artifact problem into a design frame: preferred situation, outer environment, inner mechanism, interface, means-ends decomposition, bounded-rationality tradeoffs, near-decomposable modules, adaptation loop, and perturbation checks.

## Activation and Execution Gate

Activate only when the request is about designing, diagnosing, or evaluating a purposeful artifact whose behavior depends on fit between goals, environment, mechanism, and interface. Do not activate for a generic design opinion, literature summary, natural-science explanation, or isolated implementation task.

Before running the workflow, identify the artifact and the preferred situation it is meant to create. If the preferred situation, environment, or evaluation threshold is missing, ask one focused clarification or mark the design as provisional with explicit assumptions.

## Workflow

1. **State the preferred situation.** Write the existing situation, preferred situation, stakeholders, success criteria, hard constraints, and non-goals. Treat vague preferences as design debt until they are made testable.

2. **Draw the artificial-system boundary.** Separate:
   - Outer environment: users, tasks, tools, APIs, files, latency, budgets, approvals, safety rules, failure costs, and deployment context.
   - Inner environment: prompts, planners, memory, state machines, models, policies, code modules, schedulers, and evaluators.
   - Interface: inputs, outputs, state handoffs, tool contracts, telemetry, escalation paths, and feedback signals.

3. **Check fit before optimizing.** Ask whether the inner mechanism is adapted to the real outer environment. If behavior fails, identify whether the mismatch is in the goal definition, interface contract, mechanism, missing feedback, or environmental assumption.

4. **Use means-ends decomposition.** Convert the preferred situation into subgoals, operators, preconditions, resources, stop conditions, and verification points. For each subgoal, specify what the orchestrator observes, decides, does, and learns.

5. **Satisfice under bounded rationality.** Choose the first architecture that meets explicit thresholds for correctness, cost, latency, recoverability, and operator control. Avoid pretending the orchestrator can globally optimize across unknown preferences and changing environments.

6. **Design for near-decomposability.** Split the orchestrator into modules that can fail, evolve, and be tested independently: intake, classification, planning, execution, memory, tool mediation, evaluation, recovery, and reporting. Keep interfaces stable and narrow.

7. **Close the adaptation loop.** Add instrumentation and review points that show whether the artifact is achieving its intended purpose in context. Decide what changes when evidence arrives: prompts, policies, tools, task boundaries, evaluations, or user-facing contracts.

8. **Validate with perturbations.** Test normal cases, edge cases, missing information, tool failure, budget limits, adversarial instructions, stale state, and conflicting goals. A design is not mature until its failure behavior is specified.

## Output Format

Return a compact design diagnosis or design proposal with:

- `Preferred situation`: current state, desired state, stakeholders, success thresholds, non-goals.
- `Boundary`: outer environment, inner mechanism, and interfaces.
- `Fit diagnosis`: goal, environment, mechanism, interface, feedback, and assumption mismatches.
- `Means-ends decomposition`: subgoals, operators, preconditions, resources, stop conditions, verification points.
- `Tradeoffs`: satisficing thresholds and rejected options.
- `Architecture`: near-decomposable modules and stable interface contracts.
- `Adaptation loop`: telemetry, review cadence, revision triggers, and perturbation results.

## Failure Modes

- **Mechanism-first design:** starting with agents, models, or frameworks before defining the preferred situation and outer environment.
- **Naturalizing the artifact:** treating orchestrator behavior as something to observe passively rather than something designed around goals and constraints.
- **Undefined preference:** optimizing for throughput, autonomy, or elegance when the actual desired outcome is reliability, auditability, safety, or user control.
- **Interface blindness:** ignoring handoff formats, tool contracts, state boundaries, and feedback channels.
- **Perfect-rationality fantasy:** assuming exhaustive search, complete knowledge, stable goals, or unlimited context.
- **Overcoupled hierarchy:** making every part depend on every other part, so local changes create global regressions.
- **No adaptation evidence:** shipping a control loop without telemetry, evaluation, or explicit revision triggers.
- **Local optimum lock-in:** accepting a working decomposition that blocks better alternatives or hides systemic failure costs.

## Failure, Recovery, and Idempotency

If goals or preferences conflict, separate stakeholder validation criteria from internal mechanism choices before proposing architecture. If evidence is insufficient, produce a provisional design with the smallest useful set of assumptions and name the tests that would confirm or reject them.

On re-run, preserve the same artifact boundary and preferred-situation statement unless new evidence changes them. Report changed thresholds, assumptions, interfaces, and adaptation triggers so the design can evolve without losing traceability.

## Hard Rules

- Do not start with agents, tools, frameworks, or modules before stating the preferred situation and outer environment.
- Do not present global optimization as achievable when preferences, context, or information are incomplete.
- Do not treat missing feedback, telemetry, or perturbation behavior as optional for an adaptive orchestrator.
- Do not replace domain-specific safety, security, or compliance review when the artifact can cause high-stakes harm.

## Boundaries

This skill does not replace domain-specific safety, security, legal, medical, or financial review. Use those skills when the orchestrator can cause high-stakes harm.

Do not use this skill for a pure literature summary, natural-science explanation, or generic design critique unless the task involves designing or evaluating a purposeful artifact.

This skill gives a design frame, not a complete implementation pattern. Pair it with architecture, testing, security, or product skills when the output must become production code or policy.

## Source Closure

This 02-artificial-systems-design-theory skill is self-contained for runtime use; its source basis is Herbert Simon, The Sciences of the Artificial; local artificial-systems design entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
