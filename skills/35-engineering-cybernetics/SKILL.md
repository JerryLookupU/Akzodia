---
name: 35-engineering-cybernetics
description: Use when designing an auto-orchestrator as a controlled feedback system: execution loops, planner-worker feedback, stability criteria, transfer of signals through tool chains, time lag, sampling, noise filtering, adaptive optimizing control, ultrastability, or redundancy/error control. Trigger when a task asks how an orchestrator should monitor, correct, stabilize, decouple, optimize, or recover during execution; do not trigger for generic cybernetics history or ordinary task planning without feedback/control behavior.
source_files:
  - references/source-notes.md
---
# 35 Engineering Cybernetics

## Book-Derived Essence

- Core framework: Model class -> transfer path -> feedback criterion -> stability/lag/noise/noninteraction -> optimizing or redundancy design; categorical wiring keeps module interfaces typed.
- Deep idea: Tsien’s deepest contribution is engineering classification: the right question changes with system class. Spivak adds that composed modules must preserve typed structure, not just be connected by names.
- Discovery method: Identify plant/controller/sensors/actuators, classify dynamics as linear, sampled, delayed, nonlinear, random, multivariable, or error-prone; then check typed wiring, stability margins, hunting, and redundancy independence.
- Boundary: Do not apply categorical language to simple control tuning unless interface preservation or compositional schema translation is genuinely at stake.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an auto-orchestrator must behave like a controlled system rather than a static planner. Typical signals include:

- The orchestrator receives runtime observations and must adjust agent/tool behavior.
- A workflow is unstable, oscillates, over-corrects, stalls, repeats work, or reacts too slowly.
- Multiple agents, tools, or queues interact and changes in one channel disturb another.
- The design must trade off response speed, accuracy, stability margin, noise tolerance, delay, or failure probability.
- The system must search for a good operating point when the plant, user workload, model quality, or tool latency is not known in advance.
- Reliability depends on redundant checks, voting, retries, checkpoints, or restoring components.

## Do Not Trigger

- Do not use this skill for generic cybernetics history or ordinary project planning.
- Do not use it for a workflow that has no measured feedback, actuator, delay, stability, noise, or reliability question.
- Do not use it when a lightweight feedback contract is enough and no stability, lag, coupling, optimization, or error-control analysis is needed.
- Do not use it to make formal control claims when signals and assumptions are not available.

## Standalone Contract

This skill is self-contained. Do not browse, open, or depend on external source files, source reports, original books, websites, or cross-skill distilled text during normal execution. `references/source-notes.md` is optional provenance only, not required runtime knowledge. A compliant answer must define the plant, controller, sensors, actuators, inputs, outputs, disturbances, feedback path, control criteria, dynamics class, loop model, design move, and validation checks.

## Activation and Execution Gate

Proceed only if all of these are true:

1. The request is about runtime control behavior, not merely task decomposition or implementation.
2. There is a stability, delay, sampling, noise, coupling, optimization, redundancy, or error-control concern.
3. The answer can name at least one measurable output and one actuator that can influence it.

If any condition is false, state the mismatch and route to cybernetics, requisite variety, observability, or ordinary engineering guidance.

## Workflow

1. Define the control boundary.
   - Name the plant: the workflow, tool chain, agent pool, queue, memory system, or deployment process being controlled.
   - Name inputs, outputs, disturbances, feedback signals, actuators, sensors, and the controller.
   - Separate command signals from measured outputs. In an orchestrator, "plan says done" and "verified done" are different signals.

2. Convert goals into control criteria.
   - Stability: no runaway loops, no unbounded queue growth, no repeated escalation.
   - Accuracy: output tracks the user's requested state with bounded correction error.
   - Rapidity: correction happens before the workflow becomes stale or costly.
   - Noise filtering: spurious logs, flaky tests, transient tool failures, and partial observations do not dominate control.
   - Optimization: the system finds better cost/latency/quality settings while keeping hunting loss acceptable.
   - Error control: component mistakes do not propagate into final irreversible actions.

3. Classify the orchestrator dynamics.
   - Linear constant-coefficient approximation: stable repeated loop with predictable latency and fixed policy gains.
   - Variable-coefficient system: behavior changes by task phase, model, context length, user priority, or resource pressure.
   - Time-lag system: observations arrive late, tool calls are slow, or corrective actions affect future state after delay.
   - Sampled system: the controller only observes at checkpoints, polling intervals, eval batches, or review gates.
   - Random-input/noisy system: failure reports, model judgments, or external data are uncertain.
   - Nonlinear/relay system: thresholds, hard gates, escalation switches, budget cutoffs, or retry limits dominate behavior.
   - Optimizing/adaptive system: the controller probes settings during operation because prior plant knowledge is incomplete.
   - Error-control system: reliability comes from duplication, multiplexing, consensus, restoration, or rollback.

4. Model the loop before changing it.
   - Draw a block diagram in text: `input -> controller -> actuator/tool/agent -> output -> sensor/verifier -> feedback`.
   - For each block, record gain-like behavior: how strongly it changes output per unit input.
   - Record delay, sampling interval, noise source, saturation, threshold, retry cap, and irreversible action boundary.
   - For multi-agent systems, create a matrix of channels: which setting or controller action affects which output. Identify unwanted off-diagonal coupling.

5. Choose the design move that matches the failure.
   - Poor tracking: increase useful feedback gain, add verifier feedback, or reduce open-loop assumptions.
   - Oscillation or thrashing: reduce gain, add damping, widen hysteresis, slow sampling, or increase phase margin by reducing delay.
   - Slow response: shorten sensing latency, make corrective actions more direct, or add local controllers for fast loops.
   - Cross-agent interference: decouple channels, isolate queues, split objectives, or add noninteraction constraints.
   - Time lag: avoid aggressive correction based on stale observations; add prediction, cooldowns, or lag-aware stability checks.
   - Noise: filter observations, require repeated evidence, use mean-square/error budgets, or separate signal bands from interference.
   - Unknown optimum: add low-amplitude probes, peak-holding, or band-limited exploration; bound hunting loss and recovery time.
   - Unreliable components: use duplication only when independent failures are plausible; add restoration/voting and calculate the reliability cost.

6. Validate with control-specific checks.
   - Test free response: what happens after an initial disturbance with no new user input?
   - Test forced response: can the orchestrator track a deliberate user change?
   - Test disturbance response: inject flaky tools, delayed signals, noisy evaluations, and partial failures.
   - Test saturation: budgets, rate limits, queue capacity, context length, and retry limits.
   - Test rollback/error containment before relying on adaptation or high feedback gain.

## Output Format / Deliverables

Return an engineering-control design note with:

- `control_boundary`: plant, controller, inputs, outputs, disturbances, sensors, actuators, and feedback path.
- `criteria`: stability, accuracy, rapidity, noise filtering, optimization, and error-control assumptions.
- `dynamics_class`: linear approximation, variable coefficient, time lag, sampled, noisy, nonlinear/relay, adaptive, or error-control.
- `loop_model`: text block diagram, gain-like effects, delays, sampling interval, thresholds, saturation, and irreversible boundaries.
- `design_moves`: damping, gain change, filter, cooldown, decoupling, local controller, bounded probing, redundancy, or restoration.
- `validation`: free response, forced response, disturbance, saturation, rollback/error-containment, and residual risk checks.

## Failure, Recovery, and Idempotency

- Re-running this skill should preserve the same control-boundary labels and update assumptions, evidence, or validation results.
- If observed behavior is not instrumented, first specify measurements and avoid guessing controller dynamics.
- If a design move causes instability, roll back to the prior policy, reduce gain or action frequency, and add a verification checkpoint before retrying.
- Any corrective action that writes externally must rely on idempotency, compensation, or human approval before high-gain automation.

## Failure Modes

- Treating a delayed observation as current state and over-correcting.
- Increasing feedback gain to improve accuracy while destroying stability.
- Ignoring off-diagonal coupling between agents, causing one controller to disturb another objective.
- Filtering away rare but safety-critical errors as "noise."
- Using adaptive optimizing control without bounding exploration loss, budget use, or irreversible side effects.
- Assuming redundancy improves reliability when components share the same prompt, data, model failure, or tool dependency.
- Applying linear transfer-function intuition after thresholds, saturation, or retry caps have become the dominant behavior.

## Boundaries

- This skill designs orchestrator control behavior; it is not a generic project-management planner.
- Do not claim stability, optimality, or reliability without explicit criteria and assumptions.
- Do not use high-gain automation for actions that cannot be rolled back unless a human or stronger verifier gate is present.
- Do not model social, legal, medical, or financial decisions as purely technical control loops; use domain review and applicable policy.
- Keep the mathematics lightweight unless the user asks for formal analysis or the implementation already exposes measurable signals.
- If the source of observed behavior is unknown, first instrument the loop instead of guessing the controller.

Optional provenance trace is recorded in `references/source-notes.md`; do not load it during normal runtime execution.

## Hard Rules

- Do not claim stability, optimality, or reliability without explicit assumptions and validation checks.
- Do not increase feedback gain for accuracy without checking delay, noise, saturation, and rollback risk.
- Do not treat delayed observations as current state.
- Do not use redundancy unless failure modes are plausibly independent or restoration/voting is defined.
- Keep irreversible or high-impact actions behind stronger verification or human review.

## Source Closure

This 35-engineering-cybernetics skill is self-contained for runtime use; its source basis is Hsue-Shen Tsien, Engineering Cybernetics; Spivak category-theory fusion notes. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
