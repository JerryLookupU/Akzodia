---
name: 42-detection-and-estimation-theory
description: Use when designing an auto-orchestrator that must decide whether evidence supports a route, tool call, escalation, safety gate, retry, or acceptance decision, or estimate a latent confidence, state, parameter, risk, or quality score from noisy observations. Trigger on likelihood ratios, Bayesian or Neyman-Pearson thresholds, ROC/error tradeoffs, sequential tests, detector gates, estimator selection, posterior scoring, Kalman/particle-style state tracking, and uncertainty-aware orchestration.
source_files:
  - references/source-notes.md
---
# 42 Detection and Estimation Theory

## Book-Derived Essence

- Core framework: Hypotheses/state, noisy observations, estimator/detector, threshold, loss, false alarm, miss, and calibration.
- Deep idea: The method makes uncertainty operational: a detector chooses under error tradeoffs, and an estimator reports state with uncertainty.
- Discovery method: Name hypotheses or state variable, observation model, score, threshold, priors/costs, operating curve, validation data, and no-decision branch.
- Boundary: Do not collapse detection into classification labels when false alarms and misses have different consequences.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestrator needs a disciplined bridge from noisy observations to actions:

- A routing, gating, verification, safety, or acceptance decision needs explicit false-alarm, miss, or error-rate control.
- A model, agent, tool, or workflow branch should be selected from multiple plausible hypotheses.
- The system must estimate confidence, task state, user intent, environment state, model quality, tool reliability, or risk from partial evidence.
- The policy currently uses arbitrary thresholds and needs a rationale tied to costs, priors, downstream tolerance, or operating rate.
- The orchestrator receives evidence over time and may stop early, ask for more observations, or defer until likelihood becomes decisive.

## Non-Triggers

- Do not trigger for generic statistical signal-processing history, probability tutorials, or implementation tasks with deterministic inputs.
- Do not trigger for information-flow compression or handoff design unless the main problem is a detector, estimator, threshold, or posterior decision.
- Do not trigger for causal-effect questions, experiment design, or active learning beyond the stop/continue logic of sequential decisions.
- Do not trigger when the user only needs a contractual rule with exact observations and no uncertainty model.

## Standalone Runtime Contract

This SKILL.md contains the full runtime procedure. Do not read external webpages, original books, source reports, external source snapshots, distilled source material, or files outside this skill directory to execute the skill. `references/source-notes.md` is provenance-only: use it only when the user explicitly asks to audit source lineage, not as an execution dependency.

## Activation And Execution Gate

Before applying this skill, state the activation decision in one sentence. Proceed only if all gate conditions are true:

- The task contains noisy, partial, uncertain, or sequential observations.
- The output is a detector decision, route/gate/escalation action, confidence/state estimate, or threshold policy.
- At least one operating requirement can be named: false accept, miss, false alarm, calibration, regret, cost, latency, or decision rate.

If a gate condition is missing, ask up to three targeted questions or recommend a deterministic rule, information-flow design, causal method, or instrumentation-first approach.

## Workflow

1. Classify the problem before designing the mechanism.
   - Use detection when the output is a discrete decision: choose route A/B, accept/reject, safe/unsafe, retry/continue, human/escalate, model/tool selection.
   - Use estimation when the output is a value or latent state: confidence score, risk level, completion quality, task difficulty, user intent probability, tool reliability.
   - Use both when a decision depends on an estimated unknown: estimate missing parameters, then test whether observations fit the action model.

2. Define the observation model.
   - List the observations available to the orchestrator: model logits, verifier results, tool traces, latency, cost, user constraints, retrieval scores, execution errors, historical outcomes.
   - Separate signal from nuisance variables: what carries task-relevant evidence, and what is noise, confounding, drift, or missing data?
   - State the candidate hypotheses or state variables. For detection, define `M0` as the default/null model and `M1...Mk` as alternatives. For estimation, define the parameter or state `theta`.
   - Record what is known: priors, likelihoods, empirical calibration data, assumed distributions, sample size, independence assumptions, and downstream cost tolerance.

3. Choose the criterion before choosing the formula.
   - For detection with known priors and costs, use a Bayes decision rule: choose the model minimizing expected decision cost.
   - For detection with a hard tolerance on false positives or unsafe actions, use a Neyman-Pearson rule: constrain false-alarm probability and maximize detection probability.
   - For multi-route selection, compute comparable model scores such as `log prior + log likelihood` and choose the largest after monotone simplification.
   - For model-consistency checks without a well-defined alternative, use a null-hypothesis region: accept consistency only when observations fall inside the high-probability region under `M0`.
   - For estimation, pick the error criterion explicitly: MMSE for squared-error quality, MAP for most probable state when posterior mean is hard or inappropriate, ML when no trustworthy prior exists, and linear/MMSE filters when state evolves over time.

4. Build the sufficient statistic or estimator.
   - Reduce evidence to the smallest statistic that preserves ordering for the decision: likelihood ratio, log-likelihood difference, calibrated score, verifier margin, consistency statistic, or posterior odds.
   - Preserve monotone transformations only; do not change decision ordering when simplifying.
   - For dynamic state, use recursive updates: prior state prediction, observation update, uncertainty update, and stop/continue decision. Kalman-style updates fit linear Gaussian assumptions; particle-style updates fit nonlinear or non-Gaussian states.
   - For unknown nuisance parameters, either integrate over a prior, estimate then plug into the detector, or choose a robust/non-parametric test when distributional assumptions are weak.

5. Set thresholds from operating requirements.
   - Translate downstream tolerance into error rates: false tool invocation, missed hazard, unnecessary escalation, rejected good answer, accepted bad answer.
   - Account for decision rate. A threshold acceptable for one decision per day can be unacceptable for thousands of routing decisions per minute.
   - Use ROC or equivalent tradeoff curves when possible. Report both controllable thresholds and non-controllable problem difficulty, such as overlap between score distributions.
   - For sequential orchestration, use three outcomes at each step: accept `M1`, accept `M0`, or collect more evidence. Stop only when accumulated likelihood crosses a boundary.

6. Validate and instrument.
   - Estimate false-alarm, miss, detection, calibration, and regret metrics on held-out traces or simulation.
   - Compare estimator behavior for bias, consistency, and variance; biased estimates can be useful, but their role must be explicit.
   - Stress threshold sensitivity under distribution shift, adversarial inputs, sparse observations, and correlated evidence.
   - Log the observation vector, statistic, threshold, selected action, and realized outcome so the orchestrator can recalibrate.

## Failure Modes

- Treating an estimation score as a detector without specifying the decision threshold and error costs.
- Optimizing for average accuracy when the real constraint is a low false-alarm or low miss rate.
- Using a prior that encodes a guess rather than measured or defensible domain knowledge, causing the posterior to mirror assumptions.
- Ignoring decision rate; small per-decision error probabilities can become frequent incidents at high throughput.
- Collapsing all uncertainty into one confidence number when separate false-positive, false-negative, calibration, and drift risks matter.
- Assuming Gaussian, independent, or stationary observations because the math is convenient; validate these assumptions or choose robust tests.
- Tuning thresholds on the same traces used to report performance.
- Letting sequential tests keep sampling without a budget, latency cap, or explicit no-decision branch.

## Output Format And Deliverables

Return the design or review in this order unless the user requests another format:

1. Activation decision and problem class: detection, estimation, or both.
2. Observation model with hypotheses or state variable, assumptions, priors/likelihoods/data availability, and nuisance variables.
3. Decision or estimation criterion with threshold or scoring rule.
4. Operating metrics: false alarm, miss, calibration, regret, cost, latency, and decision-rate implications.
5. Validation and instrumentation plan, provisional assumptions, and remaining risks.

## Failure, Recovery, And Idempotency

- Treat thresholds and estimators as design recommendations until the user explicitly asks for implementation.
- Re-running the skill should preserve hypothesis names, statistic definitions, thresholds, and calibration datasets unless a change is justified.
- If likelihoods, priors, or labeled outcomes are unavailable, produce a conservative provisional detector plus instrumentation rather than claiming validation.
- On partial failure or distribution shift, log the observation vector, statistic, threshold, action, outcome, and recalibration decision.
- Sequential tests must include accept, reject, collect-more-evidence, and no-decision/escalation branches with budget and latency limits.

## Boundaries

This skill designs orchestration decisions and estimators; it does not prove statistical optimality for an unspecified data-generating process. Do not use it as a substitute for domain safety policy, legal compliance, security review, or human approval rules.

Use simpler deterministic rules when observations are exact and the action boundary is contractual. Use causal inference methods when the main question is intervention effect rather than state inference. Use experiment design or active learning methods when the core task is deciding which new observations to collect, beyond the sequential stop/continue logic here.

When likelihoods, priors, or labeled outcomes are unavailable, produce an explicit provisional detector with conservative thresholds, instrumentation, and a plan to collect calibration data instead of presenting the design as statistically validated.

## Hard Rules

- Do not recommend a detector without naming hypotheses, statistic or score, threshold logic, and error tradeoff.
- Do not recommend an estimator without naming the estimated state or parameter, loss/error criterion, assumptions, and validation metric.
- Do not tune and report on the same traces as if the result were held-out performance.
- Do not let sequential evidence collection run without stop boundaries, budget, latency cap, and escalation/no-decision behavior.
- Provenance files are not runtime inputs. `references/source-notes.md` may only be cited as source trace when provenance is requested.

## Source Closure

This 42-detection-and-estimation-theory skill is self-contained for runtime use; its source basis is Detection and estimation theory sources; local detection entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
