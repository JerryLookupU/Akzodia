# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
: Detection and Estimation Theory

Source file:

Identified source:

- Don H. Johnson, *Statistical Signal Processing*, Rice University, 2013.
- Relevant chapters: Chapter 4, "Estimation Theory"; Chapter 5, "Detection Theory"; introduction framing.

## Distilled Thesis

Statistical signal processing separates two tasks that auto-orchestrators often blur:

- Detection: decide which model, route, action, or gate is most consistent with observations.
- Estimation: infer a parameter, latent state, waveform, or score from noisy observations.

Detection is driven by decision criteria and error tradeoffs. Estimation is driven by the chosen loss function and assumptions about priors, likelihoods, and state dynamics. Effective orchestrator design should first classify which task it faces, then bind the mechanism to explicit costs, error constraints, and validation metrics.

## Operational Concepts

### Detection

- The central detector is the likelihood-ratio or equivalent likelihood-ordering test.
- If priors and costs are known, use a Bayes decision rule that minimizes expected cost.
- If one error type must be controlled, use a Neyman-Pearson criterion: constrain false-alarm probability and maximize detection probability.
- For more than two models, choose the largest comparable model statistic, typically `prior * likelihood` or `log prior + log likelihood`.
- A sufficient statistic is any reduced evidence score that preserves the ordering needed for the decision.
- ROC curves express the tradeoff between false alarms and detections; problem difficulty is driven by overlap between conditional evidence distributions.
- Model-consistency testing is appropriate when the null model is defined but alternatives are not.
- Sequential likelihood testing supports stop/continue decisions when evidence arrives over time.

### Estimation

- Estimation quality depends on the criterion: MMSE, MAP, ML, linear MMSE, or another explicit loss.
- MMSE estimates the posterior mean and is appropriate for squared-error objectives.
- MAP chooses the posterior mode and is useful when posterior means are hard to compute or not the desired summary.
- ML is useful when no prior is available or when parameters are treated as non-random.
- Bias, consistency, variance, and efficiency are separate estimator properties; unbiasedness alone does not guarantee low error.
- Wiener and Kalman filters express linear minimum-mean-squared waveform or state estimation. Kalman filtering generalizes steady-state filtering to recursive state updates.
- Particle filtering approximates recursive Bayesian state estimation when dynamics or observations are nonlinear or non-Gaussian.

## Orchestrator Translation

Use detection theory for:

- model/router selection;
- answer accept/reject gates;
- safety and policy triggers;
- tool-call authorization;
- escalation or retry decisions;
- consistency checks for retrieved evidence, tool outputs, or execution traces.

Use estimation theory for:

- confidence calibration;
- task difficulty estimation;
- user intent or latent requirement inference;
- tool reliability scoring;
- evolving plan-state tracking;
- risk, cost, quality, or completion estimates.

Hybrid pattern:

1. Estimate unknown nuisance values such as task difficulty, tool reliability, user intent, or environment state.
2. Insert those estimates into a detector.
3. Make the final route/gate decision against an explicit threshold.
4. Validate realized false-alarm, miss, and calibration behavior.

## Design Checklist

- Define `M0` as the safe/null/default model before alternatives.
- State each observation and which hypothesis or state it informs.
- Choose the objective before tuning thresholds.
- Convert operational tolerance into statistical errors: false alarm, miss, incorrect route, bad acceptance, wasted escalation.
- Account for decision rate and downstream impact.
- Use monotone transformations only when simplifying scores.
- Include a no-decision or gather-more-evidence branch for sequential settings.
- Validate with held-out traces, simulation, and distribution-shift checks.

## Caveats

- Priors must be measured or justified; arbitrary priors can dominate the posterior.
- Thresholds tuned on a single environment can fail under drift.
- Gaussian and independence assumptions are convenient but often false for orchestrator traces.
- When distributions are only partially known, robust or non-parametric tests are safer than overconfident parametric detectors.
- A detector can be optimal under its stated criterion and still unsuitable if the criterion is wrong.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Detection and estimation theory sources; local detection entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Hypotheses/state, noisy observations, estimator/detector, threshold, loss, false alarm, miss, and calibration.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not collapse detection into classification labels when false alarms and misses have different consequences.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The method makes uncertainty operational: a detector chooses under error tradeoffs, and an estimator reports state with uncertainty.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Name hypotheses or state variable, observation model, score, threshold, priors/costs, operating curve, validation data, and no-decision branch.
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
