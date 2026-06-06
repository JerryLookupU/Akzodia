---
name: 33-cybernetics
description: Use when designing or reviewing auto-orchestrators as feedback-controlled systems: monitoring signals, state estimates, comparators, control policies, corrective actions, noise filters, homeostasis targets, and communication loops between planner, executor, evaluator, tools, and humans. Trigger when a system must adapt during execution instead of following a static plan.
source_files:
  - references/source-notes.md
---
# 33 Cybernetics

## Book-Derived Essence

- Core framework: Sensor -> comparator -> controller -> actuator -> controlled process -> feedback under disturbance and noise.
- Deep idea: Cybernetics abstracts control across machines, organisms, and organi

zations: behavior is regulated by information loops, not by isolated commands.
- Discovery method: Name the target band, sensed variable, comparator, control action, loop delay, noise, disturbance, and how the system learns from error.
- Boundary: Do not call any iterative workflow cybernetic unless feedback changes future action.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when orchestration quality depends on closed-loop control rather than one-shot planning:

- An agent, workflow, or runtime must monitor execution and adjust actions from feedback.
- You need to define what signals the orchestrator observes, what target state it maintains, and how deviations trigger intervention.
- Runs degrade because telemetry is noisy, delayed, missing, ambiguous, or interpreted by the wrong component.
- A planner keeps issuing tasks without checking whether previous actions changed the environment as expected.
- You are designing recovery loops, budget controls, human escalation, evaluator feedback, tool retry policy, or adaptive routing.
- You need a control contract between subsystems: who senses, who compares, who decides, who acts, and who learns.

## Do Not Trigger

- Do not use this skill for historical or biographical cybernetics summaries.
- Do not use it for static plans, checklists, or one-shot workflows with no feedback-dependent action.
- Do not use it when the only task is adding dashboards or logs and no control policy will consume the signals.
- Do not use it for duplicate side-effect safety unless the main question is the broader feedback loop around that safety mechanism.

## Standalone Contract

This skill is self-contained. Do not browse, open, or depend on external source files, source reports, original books, websites, or cross-skill distilled text during normal execution. `references/source-notes.md` is optional provenance only, not required runtime knowledge. A compliant answer must name the controlled system, target bounds, sensor/state-estimate path, comparator, control policy, actuators, noise controls, loop timing, and disturbance tests.

## Activation and Execution Gate

Proceed only if all of these are true:

1. Runtime feedback can change execution, routing, retrying, stopping, escalation, or learning behavior.
2. There is a target variable or acceptable bound the orchestrator is trying to maintain.
3. The answer can identify at least one sensor, comparator, policy decision, and actuator.

If any condition is false, explain whether the request is observability, planning, idempotency, requisite-variety, or another skill instead.

## Workflow

1. Name the controlled system and its equilibrium target.
   - State what the orchestrator is trying to keep within bounds: task progress, quality, cost, latency, safety risk, user intent match, tool reliability, queue depth, or human-review load.
   - Define acceptable ranges instead of vague success: maximum retries, minimum confidence, budget ceiling, freshness window, error budget, or completion criteria.
   - Separate the object being controlled from the controller. For example, a worker pool, retrieval pipeline, plan executor, or tool gateway may be controlled by a separate monitor and policy layer.

2. Map the communication loop.
   - Identify the message path from environment to sensor, sensor to state estimate, estimate to comparator, comparator to control policy, policy to actuator, and actuator back to environment.
   - For each message, specify payload, cadence, owner, retention, and trust level.
   - Include human messages when approval, clarification, review, or escalation is part of the loop.
   - Make the loop observable as a first-class runtime artifact, not hidden inside ad hoc logs.

3. Define sensors and state estimates.
   - Choose signals that reveal the controlled variable: tool result status, diff quality, test output, evaluator score, token spend, elapsed time, queue lag, exception class, user correction, or artifact integrity.
   - Convert raw signals into state estimates the controller can use: healthy, uncertain, diverging, blocked, over-budget, unsafe, stale, or complete.
   - Record confidence and evidence with each estimate so the controller can distinguish knowledge from guesswork.
   - Add sampling, aggregation, or smoothing when raw telemetry is too sparse or too noisy.

4. Build the comparator.
   - Compare estimated state against the equilibrium target and explicit constraints.
   - Classify deviation severity: no action, observe, adjust, retry, replan, throttle, compensate, escalate, or stop.
   - Use hysteresis or cooldowns for flapping signals so minor oscillations do not trigger repeated corrective action.
   - Require stronger evidence before high-impact actions such as deletion, external writes, budget expansion, or user-facing finalization.

5. Design corrective actions as actuators.
   - List the allowed interventions: change plan, retry with same idempotency key, switch model/tool, request user input, pause queue, roll back checkpoint, add tests, reduce scope, or trigger human review.
   - Tie each actuator to preconditions, expected effect, timeout, and failure response.
   - Prefer bounded actions with measurable outcomes over open-ended "try harder" loops.
   - Ensure actuators cannot fight each other; if two policies can act on the same variable, define arbitration.

6. Control noise and corrupted information.
   - Identify likely noise sources: flaky tests, partial tool output, stale cached context, hallucinated state, delayed callbacks, inconsistent user instructions, or low-quality evaluator feedback.
   - Add redundancy for high-risk signals: independent checks, source attribution, replay, checksums, structured schemas, or direct inspection.
   - Treat missing or contradictory feedback as a state requiring policy, not as success.
   - Do not let one noisy metric dominate the loop when the real target is multi-dimensional.

7. Calibrate loop timing.
   - Match feedback frequency to the speed of change. Fast loops suit retries and health checks; slower loops suit planning, quality review, and budget governance.
   - Avoid delayed feedback that arrives after irreversible side effects have already happened.
   - Avoid over-tight loops that consume budget, thrash plans, or starve execution.
   - Define when the controller should terminate, hand off, or move to a different loop.

8. Test the loop under disturbance.
   - Inject failed tools, misleading observations, delayed callbacks, budget pressure, changed user goals, and partial success.
   - Verify the controller observes the deviation, classifies it correctly, takes the intended bounded action, and records why.
   - Check for oscillation, runaway retries, stale state, silent failure, and controller conflicts.
   - Review whether the system returns to the target range or explicitly escalates when homeostasis is not achievable.

## Output Format / Deliverables

Return a closed-loop control contract with:

- `controlled_target`: system, regulated variables, acceptable bounds, and stop/escalation criteria.
- `loop_map`: environment, sensors, state estimates, comparator, policy, actuator, and feedback path.
- `signal_contract`: payload, cadence, owner, retention, trust level, confidence, and evidence for each signal.
- `control_policy`: deviation classes, allowed actions, thresholds, hysteresis/cooldowns, and arbitration.
- `noise_and_timing`: noise sources, corroboration, sampling cadence, delay risk, and termination rule.
- `disturbance_tests`: disturbances injected, expected observation, expected action, and audit record.

## Failure, Recovery, and Idempotency

- Re-running this skill should revise the same loop contract and preserve named variables, signals, and actuators unless the control boundary changes.
- If signals are missing, contradictory, or too noisy for action, classify the state as uncertain and require observation, corroboration, or human review.
- If an actuator fails or overshoots, record the deviation, suppress repeated unbounded action, and choose retry, replan, escalation, or stop according to policy.
- Corrective actions that create side effects must use the relevant idempotency or compensation contract.

## Failure Modes

- Treating cybernetics as a metaphor while leaving feedback, comparison, and corrective action unspecified.
- Measuring what is easy to log instead of what actually controls task quality, cost, safety, or progress.
- Letting the planner act as if its initial model is still true after tools, users, or external systems change state.
- Using noisy evaluator scores as direct actuators without confidence, thresholds, or corroborating evidence.
- Creating positive feedback loops where retries, replans, or escalations amplify failure instead of damping it.
- Responding to every small deviation, causing oscillation, flapping, budget waste, or inconsistent user experience.
- Hiding controller decisions in unstructured logs, making later diagnosis and audit impossible.
- Mixing multiple controllers over the same resource without priority, arbitration, or shared state.
- Assuming equilibrium means no change; a healthy orchestrator may keep adapting while maintaining bounded variables.

## Boundaries

- This skill designs feedback-control structure for auto-orchestrators; it is not a general history or philosophy of cybernetics.
- Use monitoring and observability patterns when the main task is instrumentation coverage rather than control-policy design.
- Use model checking when you need formal verification of finite-state safety properties.
- Use scheduling theory or queueing theory when the primary variable is resource allocation under load.
- Use requisite variety when the main question is whether the controller has enough response diversity for environmental complexity.
- Use engineering cybernetics when the work requires mathematical control modeling, transfer functions, or stability analysis.
- Do not add adaptive control loops to simple deterministic workflows unless feedback materially improves correctness, cost, safety, or recovery.
- Optional provenance trace is recorded in `references/source-notes.md`; do not load it during normal runtime execution.

## Hard Rules

- Do not prescribe corrective action without a named sensor, comparator condition, and bounded actuator.
- Treat missing or contradictory feedback as a controlled state, not as success.
- Add hysteresis, cooldown, or evidence thresholds where noisy signals can cause repeated action.
- Define arbitration when multiple controllers can act on the same variable.
- Record controller decisions as inspectable runtime artifacts, not only unstructured logs.

## Source Closure

This 33-cybernetics skill is self-contained for runtime use; its source basis is Norbert Wiener cybernetics sources and local control-feedback entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
