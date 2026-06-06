# Source Notes

## Manifest Metadata

- Entry id: 33
- Title: 控制论 / Cybernetics
- Skill name: `33-cybernetics`
- Source file: `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/33_控制论__Cybernetics/supplement_mitpress_mit_edu.txt`

## Source Basis

The provided source is the MIT Press page for Norbert Wiener's **Cybernetics or Control and Communication in the Animal and the Machine**, reissuing the 1961 second edition. The page identifies the work as a classic foundation for cybernetics and information theory.

Core claims distilled:

- Cybernetics studies control and communication across systems with feedback loops.
- The theory applies across biological, mechanical, cognitive, and social systems.
- The central unit is the message or information flow, sent and responded to through feedback.
- System function depends on message quality.
- Noise corrupts information and can prevent homeostasis or equilibrium.
- The text connects technical control concerns with philosophical and social implications.

## Supplemented Theory Metadata

The source file is a publisher book page rather than a full technical excerpt. It contains enough metadata and summary material to identify the theory, but not enough operational detail for an executable auto-orchestrator skill. Minimal supplemental theory framing was therefore added:

- Primary author: Norbert Wiener.
- Primary work: *Cybernetics or Control and Communication in the Animal and the Machine*.
- First publication: 1948; second edition: 1961; MIT Press reissue metadata in source: 2019.
- Core design translation: an orchestrator should be treated as a closed-loop controller whose behavior depends on sensed state, communication quality, deviation detection, corrective action, and stability of the resulting feedback loop.
- Auto-orchestrator mapping: planner, executor, evaluator, monitor, tool gateway, human-review channel, budget governor, retry controller, and recovery policy can each be modeled as parts of a cybernetic loop.

## Distillation Notes

For auto-orchestrator design, cybernetics is most useful when it forces explicit loop design:

1. define the variable to keep within bounds;
2. observe the variable through sensors and messages;
3. estimate current state from raw signals;
4. compare that estimate to the target;
5. select bounded corrective action;
6. act on the environment;
7. observe whether the action restored the desired state.

The skill therefore emphasizes control contracts, signal quality, noise handling, comparator logic, actuator design, loop timing, and disturbance tests. It avoids broad historical summary and converts the source concept into a runtime design procedure.

## Auto-Orchestrator Heuristic

If an orchestrator can continue executing after the world changes, its control loop must be explicit. Require at least:

- a target state or bounded operating range;
- named signals and state estimates;
- a comparator that classifies deviation;
- bounded actuators with preconditions and expected effects;
- noise handling for corrupted, missing, stale, or contradictory information;
- tests showing the loop recovers from disturbance or escalates when homeostasis is impossible.

Without these, the system is a static plan executor rather than a feedback-controlled orchestrator.
