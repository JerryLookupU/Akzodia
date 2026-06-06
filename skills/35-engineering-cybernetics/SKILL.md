---
name: 35-engineering-cybernetics
description: Use when designing an auto-orchestrator as a controlled feedback system: execution loops, planner-worker feedback, stability criteria, transfer of signals through tool chains, time lag, sampling, noise filtering, adaptive optimizing control, ultrastability, or redundancy/error control. Trigger when a task asks how an orchestrator should monitor, correct, stabilize, decouple, optimize, or recover during execution; do not trigger for generic cybernetics history or ordinary task planning without feedback/control behavior.
---

# Engineering Cybernetics For Auto-Orchestrators

## When To Use

Use this skill when an auto-orchestrator must behave like a controlled system rather than a static planner. Typical signals include:

- The orchestrator receives runtime observations and must adjust agent/tool behavior.
- A workflow is unstable, oscillates, over-corrects, stalls, repeats work, or reacts too slowly.
- Multiple agents, tools, or queues interact and changes in one channel disturb another.
- The design must trade off response speed, accuracy, stability margin, noise tolerance, delay, or failure probability.
- The system must search for a good operating point when the plant, user workload, model quality, or tool latency is not known in advance.
- Reliability depends on redundant checks, voting, retries, checkpoints, or restoring components.

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
