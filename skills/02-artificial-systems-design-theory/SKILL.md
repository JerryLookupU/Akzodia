---
name: 02-artificial-systems-design-theory
description: Use when designing, diagnosing, or evaluating an auto-orchestrator as a goal-directed artificial system: map preferred outcomes, outer environment constraints, inner mechanisms, interfaces, task decomposition, adaptation loops, and bounded-rationality tradeoffs.
---

# Artificial Systems / Design Theory

## When To Use

Use this skill when the work is not just explaining an existing system, but designing an artifact that should change an existing situation into a preferred one. It is especially useful for auto-orchestrators, agent runtimes, workflow engines, task routers, planner/executor systems, tool policies, and evaluation loops.

Trigger on requests such as:

- Design or refactor an orchestrator, planner, routing layer, task decomposition policy, or agent control loop.
- Diagnose why a system behaves poorly in a specific environment despite plausible internal logic.
- Turn broad goals into a bounded architecture, feedback loop, and verification plan.
- Decide whether to adapt the inner mechanism, the outer environment, or the interface between them.

Read `references/source-notes.md` only when you need provenance, book metadata, or the underlying theory notes.

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

## Failure Modes

- **Mechanism-first design:** starting with agents, models, or frameworks before defining the preferred situation and outer environment.
- **Naturalizing the artifact:** treating orchestrator behavior as something to observe passively rather than something designed around goals and constraints.
- **Undefined preference:** optimizing for throughput, autonomy, or elegance when the actual desired outcome is reliability, auditability, safety, or user control.
- **Interface blindness:** ignoring handoff formats, tool contracts, state boundaries, and feedback channels.
- **Perfect-rationality fantasy:** assuming exhaustive search, complete knowledge, stable goals, or unlimited context.
- **Overcoupled hierarchy:** making every part depend on every other part, so local changes create global regressions.
- **No adaptation evidence:** shipping a control loop without telemetry, evaluation, or explicit revision triggers.
- **Local optimum lock-in:** accepting a working decomposition that blocks better alternatives or hides systemic failure costs.

## Boundaries

This skill does not replace domain-specific safety, security, legal, medical, or financial review. Use those skills when the orchestrator can cause high-stakes harm.

Do not use this skill for a pure literature summary, natural-science explanation, or generic design critique unless the task involves designing or evaluating a purposeful artifact.

This skill gives a design frame, not a complete implementation pattern. Pair it with architecture, testing, security, or product skills when the output must become production code or policy.
