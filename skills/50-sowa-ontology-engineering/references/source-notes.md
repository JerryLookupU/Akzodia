# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Source Basis
- Distilled source: Sowa Ontology Engineering.
- Source pages and local mirrors were used during generation, but no machine-local path is required or preserved as a runtime dependency.
- This note carries the portable source summary. Runtime execution uses `SKILL.md`.
## Key Concepts Internalized
- ontology as categories for a language and purpose
- independent relative mediating
- physical abstract
- continuant occurrent
- object process schema script
- juncture participation description history
- structure situation reason purpose
- lexicon as bridge from language to knowledge
- word sense versus concept versus object
- syntax semantics pragmatics
- sign object interpretant agent ground
- metadata as signs of signs
- role type and Has relation
- prehension intrinsic extrinsic
- participant stage attribute manner
- determinant immanent source product
- initiator resource goal essence
- agent effector instrument patient recipient
- process state event precondition postcondition
- continuous and discrete processes
- causal influence as directed acyclic graph
- process complexity distinctions
- purpose-bound approximation
- open systems
## Portable Overview
# Book Overview: Sowa Ontology Notes

## Bibliographic Frame

- Title: Ontology
- Author: John F. Sowa
- Source entry: `local source snapshot used during distillation`
- Local original entry: `local source snapshot used during distillation`
- Distilled output: `Akzodia/skills/50-sowa-ontology-engineering`
- Chapter wrappers: 15
- Primary source form: local mirrored HTML pages with Markdown reading wrappers

## Adler Stage 0

### 1. Structural Understanding

The source is not a single linear monograph. It is a connected set of Sowa ontology pages covering:

- Definition and scope of ontology.
- Agents and levels of agent competence.
- Processes, causality, time, Petri nets, and theory lattices.
- Glossary and metalevel conventions.
- Lexicon structure and semantic representation.
- Ontology, metadata, and semiotics.
- Roles, relations, thematic roles, and participant categories.
- Top-level categories of the KR Ontology.

The engineering center is the interaction among five layers:

1. Top-level categories define the structural backbone.
2. Lexicons connect language-specific signs to semantic concepts.
3. Semiotics explains why metadata must relate signs, objects, agents, and purposes.
4. Processes and causality explain dynamic reality as purpose-bound approximations.
5. Roles and thematic roles explain how entities participate in processes.

### 2. Interpretive Understanding

Sowa's practical method is not "build a complete ontology." It is:

- Start from primitive distinctions.
- Generate a lattice or matrix only where distinctions are meaningful.
- Treat categories as constrained by axioms, not always definable in closed form.
- Keep language, logic, and world knowledge connected through a lexicon.
- Treat metadata as signs interpreted by agents, not meaning in itself.
- Model processes through states, events, participants, preconditions, postconditions, and causal influence.
- Accept that engineering models are approximations for specific purposes.

### 3. Critical Understanding

Strengths:

- Strong safeguards against invalid `is-a` hierarchies.
- Rich tools for separating object, process, sign, role, purpose, script, history, and situation.
- Useful critique of superficial metadata and vocabulary standardization.
- Clear process/causality distinctions for systems engineering and agent modeling.

Risks:

- The full KR ontology is too broad for direct operational use.
- Some primitives are intentionally open and require domain-specific constraints.
- Formal logic, conceptual graphs, and Petri nets are useful but too heavy for many ordinary schema tasks.
- The source pages blend philosophy, linguistics, AI, and engineering; a skill must select executable checks rather than reproduce the theory.

### 4. Application Understanding

The distilled skill should trigger on real modeling work:

- Top-level category audits.
- Lexicon and vocabulary interoperability.
- Semantic metadata review.
- Process, causality, state/event, and workflow modeling.
- Agent, purpose, role, and responsibility modeling.
- Ontology quality review for brittle LLM/agent/task vocabularies.

It should not trigger on generic summaries, philosophy explanations, or simple schema edits.

## Core Concept Map

```mermaid
graph TD
## Runtime Coverage
- `SKILL.md` contains the executable method, triggers, gates, output formats, failure handling, and boundaries.
- `test-prompts.json` contains portability and compliance expectations.
- `audit.json` points to this local source note rather than external paths.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: John F. Sowa ontology materials: top-level categories, roles, processes, lexicon, signs, causality. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Ontology as categories for a language and purpose; classify objects, processes, roles, purposes, histories, schemas, signs, and causal relations.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not treat ontology as a fashionable class list; categories must answer questions and prevent ambiguity.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Ontology work is an audit of commitments. A term is not understood until its category, identity condition, role, process participation, and purpose are clear.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Start from purpose and competency questions, run top-level category tests, separate lexical sense from concept, model roles/processes/causes, and record what each distinction changes.
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
