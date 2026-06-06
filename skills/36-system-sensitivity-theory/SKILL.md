---
name: 36-system-sensitivity-theory
description: Use when designing, auditing, or tuning an auto-orchestrator by testing how changes in inputs, assumptions, thresholds, budgets, tool reliability, model choices, routing policies, or feedback signals affect output quality, cost, latency, safety, completion rate, or robustness. Trigger when the work needs sensitivity ranking, uncertainty-aware parameter hardening, or robustness checks instead of a single nominal workflow.
---

# System Sensitivity Theory for Auto-Orchestrators

## When To Use

Use this skill when orchestration design depends on knowing which inputs or assumptions most influence outcomes:

- You need to tune thresholds, retry limits, budgets, routing policies, evaluator cutoffs, confidence gates, or escalation rules.
- The orchestrator behaves acceptably in one scenario but fails when task difficulty, tool reliability, context quality, latency, or user ambiguity changes.
- You need to identify which uncertain inputs deserve measurement, tighter contracts, redundancy, or conservative defaults.
- A proposed design has many parameters and you need to simplify it without removing important control variables.
- Stakeholders are making claims such as "this will be robust" or "the threshold does not matter" and those claims need stress testing.
- You need to separate local one-at-a-time tuning from global interaction testing across multiple uncertain factors.

## Workflow

1. Frame the orchestrator as an input-output model.
   - Define the model boundary: planner, router, workers, tools, memory, evaluator, budget policy, retry policy, human review, and external dependencies.
   - Name the outputs that matter: task success, user intent match, evidence quality, cost, latency, safety violations, rework, queue backlog, or escalation rate.
   - Treat every tunable or uncertain element as an input: prompts, model selection, context size, retrieval depth, confidence threshold, timeout, retry count, tool accuracy, evaluator noise, budget ceiling, and user clarification policy.

2. State the uncertainty ranges.
   - For each input, record a credible range or distribution rather than a single preferred value.
   - Separate epistemic uncertainty, which can shrink with measurement or better evidence, from aleatory variability, which must be tolerated at runtime.
   - Mark correlated inputs. For example, task complexity may raise latency, cost, tool failures, and evaluator uncertainty together.
   - Reject unrealistic ranges that make the analysis look stable only because the perturbations are too narrow.

3. Choose the sensitivity question before choosing a method.
   - Use one-at-a-time perturbation for quick local debugging around a known operating point.
   - Use screening methods when there are many parameters and the goal is to discard low-impact inputs.
   - Use global sampling when nonlinear effects, correlated uncertainty, or policy interactions are plausible.
   - Use scenario or adversarial sensitivity auditing when the concern is hidden framing assumptions, not just numeric parameters.

4. Design the experiment.
   - Create a small matrix of orchestrator runs, simulations, log replays, or dry-run evaluations that varies inputs deliberately.
   - Hold immutable requirements fixed, but vary assumptions that the runtime will actually face.
   - Include interaction cases: high ambiguity plus low retrieval quality, flaky tools plus aggressive retry, low budget plus strict evaluator, delayed feedback plus irreversible actions.
   - Capture enough run metadata to attribute outcome changes to input changes.

5. Measure output effects.
   - For each output, record the delta from baseline and the direction of effect.
   - Normalize effects when inputs have different units so rankings are comparable.
   - Distinguish first-order effects from interaction effects. If an input is harmless alone but dangerous in combination, do not simplify it away.
   - Track distributional changes, not only averages, when tail risk matters.

6. Rank and interpret sensitivities.
   - Classify inputs as dominant, interaction-sensitive, low-impact, unknown, or policy-fragile.
   - Check whether the ranking is stable across task classes, model versions, tools, and load levels.
   - Treat surprising relationships as model or instrumentation bugs until inspected.
   - Document which conclusion is robust, which depends on assumptions, and which cannot be trusted with available evidence.

7. Convert findings into orchestration design changes.
   - Harden dominant inputs with tighter measurement, explicit defaults, validation, redundancy, or human review.
   - Reduce low-impact knobs by fixing defaults or removing unused configuration.
   - Add guardrails where interaction effects create unsafe or costly regions.
   - Move fragile thresholds into adaptive policies only when the feedback signal is reliable enough.
   - Update dashboards and run records so future regressions expose the same sensitive factors.

8. Re-test after changing the design.
   - Repeat the sensitivity check on the revised orchestrator, not just the original model.
   - Verify that the design is less fragile under credible perturbations.
   - Keep a sensitivity register: input, range, output affected, rank, mitigation, residual risk, and owner.

## Failure Modes

- Tuning a single happy-path run and calling the design robust.
- Using one-at-a-time tests when inputs interact nonlinearly or are correlated.
- Varying parameters across unrealistic ranges, then trusting the resulting ranking.
- Measuring only average success while ignoring tail latency, rare unsafe actions, or high-cost outliers.
- Treating evaluator scores, confidence estimates, or benchmark labels as ground truth without checking their own sensitivity.
- Removing a low first-order factor that has a large interaction effect with another policy.
- Suppressing uncertainty because it makes the orchestration decision harder to justify.
- Running sensitivity analysis without a decision to make, producing rankings that do not change the design.
- Forgetting that a sensitivity result is local to the selected task class, runtime, tools, and measurement setup.

## Boundaries

- This skill designs sensitivity-aware auto-orchestrators; it is not a general statistics tutorial or a request to compute formal Sobol indices by hand.
- Use cybernetics when the primary task is designing closed-loop feedback control rather than ranking uncertain inputs.
- Use monitoring and observability when the problem is telemetry coverage, alerting, or incident diagnosis.
- Use model checking when the question is whether all reachable states satisfy a formal safety property.
- Use queueing or scheduling theory when the dominant concern is capacity, waiting time, or resource allocation under load.
- Use optimization when the objective and constraints are already stable and the task is to find the best assignment.
- Do not run elaborate global sensitivity analysis when a cheap local perturbation or log replay can answer the design decision.
- For source provenance and distilled rationale, read `references/source-notes.md`.
