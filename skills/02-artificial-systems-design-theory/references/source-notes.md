# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Entry Metadata

- Entry: `02 设计科学 / Artificial Systems / Design Theory`
- Representative work: Herbert A. Simon, `The Sciences of the Artificial`
- Local metadata identifies the entry as a book/theory source for treating an auto-orchestrator as a goal-directed artificial artifact.
- MIT Press metadata used for supplementation: `The Sciences of the Artificial`, reissue of the third edition, Herbert A. Simon, introduction by John E. Laird, MIT Press, published August 13, 2019. The MIT Press page describes it as the expanded and updated third edition from 1996 and as a work arguing for a science of designed systems.

## Local Source Assessment

The assigned source file, `supplement_designresearchsociety_org.txt`, contains mostly Design Research Society navigation, login, footer, news, events, and organizational contact material. It does not provide usable book content for Simon's theory. It was therefore not sufficient by itself for distillation.

Supplementation came from:

- Local `metadata.json` in the same entry directory.
- Stable, widely attributed Simon design-science concepts from `The Sciences of the Artificial`.

## Distilled Theory

Simon reframes design as a science of purposeful artifacts. Natural sciences mainly explain how things are; design sciences reason about how things can be arranged to satisfy goals. This matters for auto-orchestrators because they are not neutral natural objects. They are artificial systems built to transform user intents, environmental constraints, and available tools into preferred outcomes.

Core ideas used in the skill:

- **Artifact as interface:** analyze the orchestrator as an interface between an inner environment and an outer environment.
- **Inner environment:** the artifact's organization, mechanisms, control policies, prompts, memory, code, models, and evaluators.
- **Outer environment:** user goals, task distribution, tool affordances, APIs, files, budgets, latency, permission rules, organizational constraints, and failure costs.
- **Fit:** success depends on whether the inner mechanism is adapted to the outer environment and intended purpose.
- **Design as change:** design work devises actions that move from current conditions to preferred ones.
- **Bounded rationality:** real designers and agents cannot optimize with perfect information, so they need thresholds, heuristics, stopping rules, and feedback.
- **Means-ends decomposition:** complex goals should be converted into subgoals, operators, preconditions, resources, and verification points.
- **Near-decomposability:** complex systems become manageable when split into parts with stable interfaces and limited coupling.

## Auto-Orchestrator Translation

For auto-orchestrator work, the theory becomes a practical diagnostic:

1. If the orchestrator fails, do not only inspect the model or code. Inspect the fit among goals, environment, interface, and mechanism.
2. If goals are vague, do not optimize. Define the preferred situation and measurable thresholds first.
3. If the environment is unstable, build feedback and adaptation rather than hard-coding a static plan.
4. If the system is too complex to reason about, decompose around observable interfaces and independent failure domains.
5. If exhaustive planning is impossible, choose satisficing rules with clear escalation and revision triggers.

## Short Attribution

This skill is a paraphrased operationalization of Simon's artificial-systems and design-science framing for agent/orchestrator architecture. It avoids long quotation and uses only compact theory labels in the executable workflow.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Herbert Simon, The Sciences of the Artificial; local artificial-systems design entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Inner environment / outer environment / interface / purpose. Design is search through possible artifacts under bounded rationality.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not turn it into generic brainstorming; use it when the artifact, environment, and fitness criterion can be named.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: An artificial system is judged by fit: does its internal structure mediate between purpose and environment? The skill should discover the interface where a better artifact can change the situation.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Name the desired state, the current environment, and the artifact interface. Then ask what constraints are real, what are design choices, and what satisficing threshold is enough to move forward.
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
