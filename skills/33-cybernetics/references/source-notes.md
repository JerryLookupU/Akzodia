# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Metadata

- Entry id: 33
- Title: 控制论 / Cybernetics
- Skill name: `33-cybernetics`

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

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Norbert Wiener cybernetics sources and local control-feedback entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Sensor -> comparator -> controller -> actuator -> controlled process -> feedback under disturbance and noise.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not call any iterative workflow cybernetic unless feedback changes future action.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Cybernetics abstracts control across machines, organisms, and organizations: behavior is regulated by information loops, not by isolated commands.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Name the target band, sensed variable, comparator, control action, loop delay, noise, disturbance, and how the system learns from error.
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
