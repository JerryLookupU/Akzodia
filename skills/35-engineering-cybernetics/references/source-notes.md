# Source Notes

## Manifest Entry

- id: 35
- title: 工程控制论 / Engineering Cybernetics
- skillName: 35-engineering-cybernetics
- sourceFiles:
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/35_工程控制论__Engineering_Cybernetics/00_local_hathitrust_uc1_b3734950_full_ocr.txt`
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/35_工程控制论__Engineering_Cybernetics/03_onlinebooks_library_upenn_edu.txt`

## Bibliographic Metadata

The UPenn Online Books source identifies the book as *Engineering Cybernetics* by Qian, Xuesen, 1911-2009, published by McGraw-Hill in 1954, with page images at HathiTrust. The HathiTrust OCR title page identifies the author as H. S. Tsien of the Daniel and Florence Guggenheim Jet Propulsion Center, California Institute of Technology.

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

Metadata is sufficient: title, author, publisher/year, HathiTrust identifier, and local OCR are present. No additional external lookup was required.
