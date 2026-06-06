# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
: Knowledge Representation and Reasoning

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Metadata

- Source title: `Logic-Based Artificial Intelligence`.
- Source venue: Stanford Encyclopedia of Philosophy.
- First published: August 27, 2003.
- Substantive revision: February 27, 2024.
- Entry role for this skill: supplemental theory source for knowledge representation, logic-based AI, commonsense reasoning, nonmonotonic logic, and action/change reasoning.

## Distilled Concepts

The source frames knowledge representation as a distinct AI concern: declarative representations, retrieval, maintenance, and reasoning systems should be separable from the programs they serve. This distinction is central for auto-orchestrators because decisions, memory, policy, and explanations become difficult to maintain when knowledge is buried in procedural code or prompts.

Logic-based AI is treated as a way to make reasoning problems explicit, even when final implementations are incomplete, hybrid, or not purely theorem-proving based. For orchestration, this maps to using formal or semi-formal representations as design specifications and audit surfaces.

The strongest operational pattern is nonmonotonic reasoning. Practical agents often reason with defaults that can be defeated by later evidence. The source connects this to belief revision, closed-world reasoning, planning, default logic, circumscription, truth maintenance, and multiple possible extensions. The skill adapts these into explicit default rules, blockers, support dependencies, retraction, and conflict surfacing.

Reasoning about action and change is another core pattern. Planning requires actions with preconditions and effects, plus rules for persistence. The frame problem becomes an orchestrator design issue: after a tool call or subagent handoff, which facts changed, which remained stable, and which hidden qualifications or secondary effects matter?

The source also covers taxonomic representation, nonmonotonic inheritance, contextual reasoning, causal reasoning, spatial reasoning, multiagent knowledge, and practical reasoning. The skill converts these into representation choices for classification, policy inheritance, context-scoped assertions, source integration, and explanation.

Commonsense formalization is presented as difficult but methodologically useful. Benchmark problems and evaluation criteria such as reusability, usability, and elaboration tolerance were adapted into tests for whether an orchestrator knowledge design can absorb new exceptions, changed facts, and scenario variants without wholesale redesign.

## Adaptation Rationale

The skill is not a summary of logic-based AI. It translates the source into a runtime design method for auto-orchestrators:

- Declarative KR becomes a separate knowledge layer for facts, rules, defaults, contexts, provenance, and explanations.
- Nonmonotonic logic becomes a practical default/exception and belief-revision loop.
- Closed-world reasoning becomes a bounded assumption that must be declared rather than applied globally.
- Situation calculus and action/change reasoning become state transition modeling for plans and tool execution.
- Context logic becomes source, user, workspace, time, environment, and policy scoping.
- Taxonomic reasoning becomes task/tool/policy classification and inheritance.
- Commonsense methodology becomes elaboration-tolerance testing for orchestration scenarios.

## Supplementation

The provided source content and metadata were sufficient for this entry. No external web supplementation was needed. The requested `cangjie` skill was not available in this runtime, so distillation used local `book2skill` and `skill-creator` guidance.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Knowledge Representation and Reasoning sources; local KRR entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Facts + rules + defaults + contexts + change + explanation. Representation is chosen by the reasoning task.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not formalize everything; use symbolic KR when inference, explanation, retraction, or context boundaries matter.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The essence is elaboration tolerance: a knowledge design is good if new exceptions, contexts, and facts can be added without rewriting the whole system.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Identify the questions the system must answer, what counts as unknown, where defaults can be defeated, what context scopes a claim, and what explanation must be returned.
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
