# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
: Requisite Variety

## Manifest Metadata

- Entry id: `34`
- Title: `Ashby 控制论 / Requisite Variety`
- Skill name: `34-requisite-variety`
- Source files:

## Source Basis

The source is W. Ross Ashby's *An Introduction to Cybernetics* (1956), electronically republished by Principia Cybernetica. The manifest includes a short metadata page and a long OCR text of the book.

The skill is distilled mainly from Part III, chapters 10-12:
- Chapter 10 frames regulation as protecting essential variables from disturbances.
- Chapter 11 states the law of requisite variety and connects regulation to information channels.
- Chapter 12 turns the law into regulator design: given outcome variables, acceptable states, environment, and disturbances, form a regulator that keeps outcomes within bounds.

## Distilled Concepts

- `D`: disturbances. In orchestrator design these are task classes, input defects, hidden state, tool failures, policy conflicts, latency/cost pressure, and other external variation.
- `R`: regulator responses. These are route choices, specialist agents, tool choices, prompts, guardrails, retries, approval gates, refusals, and scope reductions.
- `T`: the transformation or environment through which disturbance plus response produces an outcome. This includes model limits, tool contracts, permissions, APIs, runtime state, and user constraints.
- `E`: essential outcome variables. For orchestrators these include correctness, safety, completion, cost, latency, data integrity, and trust.
- `h`: the acceptable region for `E`.

Ashby's core design claim for this skill: the variety reaching the outcome can be forced down only by corresponding regulator variety, unless the environment or passive constraints already block enough disturbance variety. For orchestration, this means failures are often caused by a mismatch between what the runtime can encounter and what the controller can observe and vary.

## Executable Interpretation For Auto-Orchestrators

Use the law as a design audit:

1. Define what must remain controlled (`E`) and the acceptable band (`h`).
2. Enumerate distinguishable disturbances (`D`) that threaten those outcomes.
3. Identify the regulator's actual response repertoire (`R`) and its sensing/motor channels.
4. Compare rows of disturbance cases with columns of responses.
5. If distinct disturbances require distinct responses, ensure the orchestrator can both distinguish and execute them.
6. Prefer reducing required variety before adding control machinery: schemas, constraints, standard task boundaries, input validation, and passive blocking.
7. Add branches, subagents, tools, or approvals only when tied to a named disturbance and a controlled outcome.

## Useful Source Anchors

- `01_pespmc1_vub_ac_be.txt`: identifies Ashby as a founder of cybernetics and systems theory, and lists the law of requisite variety among his fundamental ideas.
- `03_ashby_info.txt`, chapter 7: variety is a property of a set of distinguishable possibilities; constraint reduces possible variation.
- `03_ashby_info.txt`, section 10/6: a regulator blocks the flow of variety from disturbance to essential variables.
- `03_ashby_info.txt`, sections 11/6-11/7: only variety in the regulator can force down variety in outcomes; variety can destroy variety.
- `03_ashby_info.txt`, section 11/11: regulator capacity is bounded by communication capacity through the relevant channel.
- `03_ashby_info.txt`, sections 11/17-11/21: compound disturbances, noise, initial state, compound targets, and internal complexity can all be represented by vector forms of `D`, `E`, and related variables.
- `03_ashby_info.txt`, sections 12/1-12/2: regulator design begins with `E`, `h`, `T`, and `D`; sensory and motor restrictions make full regulation impossible.

## Metadata Completeness

Metadata was complete for distillation: the manifest entry provided id, title, skill name, skill directory, and source files. No supplemental web or external book lookup was required.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: W. Ross Ashby requisite variety sources and local Ashby entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Disturbance variety D, response variety R, acceptable outcomes E, and attenuation/amplification through channels.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not add response variety when simpler boundary changes or disturbance attenuation solve the problem.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Only variety absorbs variety: a controller must have enough distinguishable responses for the distinguishable disturbances that matter.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Enumerate disturbance classes, acceptable outcome bands, sensor distinctions, actuator options, policy states, and where variety is reduced or amplified.
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
