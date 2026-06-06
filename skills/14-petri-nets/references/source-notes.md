# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Assigned Source

- Captured page: PNML.org, "Petri Net Markup Language - Home Page", last update shown as April 1, 2026.
- Nature of source: standards and interchange-format supplement, not a full textbook chapter.

## What The Source Contributes

- PNML.org is presented as the reference site for Petri Net Markup Language under ISO/IEC 15909 Part 2.
- ISO/IEC 15909 Part 1 defines the semantic model of Petri nets and includes High-Level Petri Nets, Symmetric Nets, and Place/Transition Nets.
- Part 2 defines abstract and concrete syntax for those net types, with UML for abstract syntax and RELAX NG for concrete PNML grammar.
- PNML separates general Petri-net features from type-specific features.
- A Petri Net Type Definition (PNTD) is used for type-specific features, and each net type declares its own namespace URI.
- Convention documents can define features reused by more than one net type.
- User-defined extensions may not be standard-compatible unless recognized by the standard or the receiving tool.
- The site hosts metamodels, grammars, examples, tools, and papers for PNML.

## Supplemented Operational Model

The assigned source did not include enough basic Petri-net execution semantics to make an auto-orchestrator skill executable. The distilled skill therefore supplements the PNML source with standard Petri-net working concepts:

- Places hold tokens and represent conditions, resources, buffers, queues, or control states.
- Transitions are atomic events.
- A marking is the token distribution over places and acts as the current state.
- A transition is enabled when input places contain enough tokens and any guard is satisfied.
- Firing consumes input tokens and produces output tokens according to arc weights.
- Common orchestration checks include reachability, deadlock, liveness, boundedness, conservation, conflict, and concurrency.

Supplemental reference points used for this operational model:

- ISO/IEC 15909 listing for Petri net standards, as referenced from PNML.org.
- Public Petri-net teaching and overview materials that consistently define places, transitions, tokens, markings, enabling, and firing, including:

## Distillation Choices

- The skill is oriented toward auto-orchestrator design, not mathematical proof or historical survey.
- PNML details are kept as interchange and portability guidance, because the assigned source mostly concerns PNML standardization.
- The workflow uses Petri-net vocabulary only where it directly helps design, verify, or repair orchestrated execution.
- No long quotations were used; source facts are paraphrased.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Petri net theory sources and local Petri-net entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Places hold tokens; transitions fire when enabled; reachability, liveness, boundedness, and invariants expose concurrency defects.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use Petri nets when the process has no concurrency, resource sharing, or state-space risk.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Petri nets make concurrency concrete. They reveal where resources are consumed, produced, blocked, duplicated, or left unreachable.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Map states/resources to places and events/actions to transitions, then test enabling conditions, token conservation, reachable markings, deadlocks, and unbounded growth.
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
