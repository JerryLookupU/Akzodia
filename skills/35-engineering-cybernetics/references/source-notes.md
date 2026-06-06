# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Entry

- id: 35
- title: 工程控制论 / Engineering Cybernetics
- skillName: 35-engineering-cybernetics
- sourceFiles:

## Bibliographic Metadata

## Distilled Theory

Tsien frames engineering cybernetics as engineering science: organize design principles for controlled and guided systems rather than discuss implementation gadgets. The practical move for an auto-orchestrator is to abstract runtime behavior into inputs, outputs, feedback links, transfer through components, and criteria such as stability, rapid response, accuracy, filtering, optimization, and reliability.

Key source-derived ideas used in the skill:

- System class determines the right question. Linear constant-coefficient systems invite stability and response analysis; variable-coefficient systems require purpose-specific performance design; nonlinear, relay, sampled, lagged, random, and error-prone systems require different methods.
- Transfer functions and block diagrams let a designer compose component behavior. For orchestrators, this becomes a diagram of planner, tools, agents, verifiers, memory, queues, and feedback signals.
- Feedback improves accuracy and response but can introduce instability. Design must check stability before increasing control gain.
- Bode/Nyquist/root-locus thinking is distilled into practical margin checks: delay, phase-like lag, gain, damping, and oscillation risk.
- Multi-variable control requires attention to interaction. The noninteraction-control chapter motivates channel matrices for agent outputs and settings, then decoupling unwanted cross-effects.
- Time lag requires lag-aware feedback. Late observations in an orchestrator are analogous to control signals based on delayed state.
- Random inputs and noise require filtering. Logs, eval scores, flaky tests, and LLM judgments should be treated as uncertain measurements.
- Optimalizing control motivates controlled probing when the plant is unknown, while accounting for hunting loss and interference.
- Ultrastability motivates changing controller characteristics when instability is detected, but only with safe boundaries.
- Error control and multiplexing motivate redundancy, restoration, and voting while emphasizing independence assumptions and reliability cost.

## Auto-Orchestrator Translation

- Plant: task execution system, agent pool, tool pipeline, queue, deployment run, or research loop.
- Controller: orchestrator policy, scheduler, planner, critic, or runtime supervisor.
- Actuator: tool invocation, task assignment, retry, rollback, escalation, prompt change, resource allocation.
- Sensor: logs, test results, verifier output, state checkpoint, user feedback, metric stream.
- Disturbance: flaky tool, latency spike, bad retrieval, model hallucination, changing user requirement, queue burst, budget pressure.
- Stability: bounded work, no runaway retries, no oscillating decisions, queue does not grow without limit.
- Gain: strength and speed of correction in response to an error signal.
- Lag: elapsed time between action and reliable observation of its effect.
- Noise: observation or evaluation error that should not produce strong correction.
- Hunting loss: cost of adaptive probing around an unknown optimum.
- Multiplexing: redundant independent checks plus restoration/voting, not blind duplicate work.

## Source Completeness

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Hsue-Shen Tsien, Engineering Cybernetics; Spivak category-theory fusion notes. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Model class -> transfer path -> feedback criterion -> stability/lag/noise/noninteraction -> optimizing or redundancy design; categorical wiring keeps module interfaces typed.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not apply categorical language to simple control tuning unless interface preservation or compositional schema translation is genuinely at stake.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Tsien’s deepest contribution is engineering classification: the right question changes with system class. Spivak adds that composed modules must preserve typed structure, not just be connected by names.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Identify plant/controller/sensors/actuators, classify dynamics as linear, sampled, delayed, nonlinear, random, multivariable, or error-prone; then check typed wiring, stability margins, hunting, and redundancy independence.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

ze, decouple, optimize, or recover during execution; do not trigger for generic cybernetics history or ordinary task planning without feedback/control behavior.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
