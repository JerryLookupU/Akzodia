# Source Notes: Detection and Estimation Theory

Source file:

- `auto_orchestrator_theory_txt_pack_v2/原文目录/07_感官_观测信息/42_检测与估计理论__Detection_and_Estimation_Theory/supplement_rice_statistical_signal_processing_notes.txt`

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
