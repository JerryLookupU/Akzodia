# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Source Basis
- Distilled source: Sowa Knowledge Representation.
- Source pages and local mirrors were used during generation, but no machine-local path is required or preserved as a runtime dependency.
- This note carries the portable source summary. Runtime execution uses `SKILL.md`.
## Key Concepts Internalized
- logic as formal structure and inference
- ontology as domain categories and commitments
- computation as executable model
- representation selection by reasoning need
- predicate calculus
- conceptual graphs
- Knowledge Interchange Format
- rules, frames, semantic networks, object-oriented systems, SQL, Prolog
- processes, events, situations, change, Petri nets
- purpose, context, modal reasoning, intentional reasoning, agents
- vagueness, uncertainty, randomness, ignorance
- fuzzy logic and nonmonotonic logic
- open, closed, and semi-open world assumptions
- knowledge acquisition and ontology sharing
- conceptual schema and multiple paradigms
- language patterns and controlled natural language
- index-based knowledge engineering
- auditable explanations with provenance and revision conditions
## Portable Overview
# Book Overview

## Bibliographic Frame

- Book: `Knowledge Representation: Logical, Philosophical, and Computational Foundations`
- Author: John F. Sowa
- Publisher/source note from local landing page: Brooks Cole, copyright 2000, actual publication date 16 August 1999
- Local source scope: companion page, preface, table of contents, index, errata, and generated Markdown wrappers

## Source Scope

The local repository does not contain full prose for all printed chapters. It contains:

- `BOOK.md` as the generated book entry and reading order.
- `source-map.json` with five local source wrappers.
- `references/source-notes.md` generated from landing page, errata, index, preface, and table of contents.
- `local source snapshot used during distillation` originals for the same pages.

This overview therefore distills the book's explicit architecture, preface claims, topic map, examples, and index evidence. It avoids pretending to have read unavailable chapter prose.

## Adler Stage 0

### 1. Structural Reading

Sowa organizes KR as a bridge among logic, ontology, and computation:

1. Logic: history, representing knowledge in logic, varieties of logic, names/types/measures, unity across notations.
2. Ontology: categories, philosophical background, top-level categories, physical entities, abstractions, sets/collections/types/categories, space and time.
3. Knowledge representations: knowledge engineering, frames, rules/data, object-oriented systems, natural language semantics, levels of representation.
4. Processes: times, events, situations, procedures, concurrency, computation, constraints, change.
5. Purposes, contexts, and agents: purpose, context syntax/semantics, first-order and modal reasoning in contexts, encapsulated objects, agents.
6. Knowledge soup: vagueness, uncertainty, randomness, ignorance, limits of logic, fuzzy logic, nonmonotonic logic, theories/models/world, semiotics.
7. Knowledge acquisition and sharing: ontology sharing, conceptual schema, multiple paradigms, mapping representations, language patterns, acquisition tools.
8. Appendices: predicate calculus, conceptual graphs, KIF, ontology base, hotel reservation, library database, controlled English to logic.

### 2. Interpretive Reading

The book's operational thesis is that knowledge representation is not one notation. It is the engineering of a computable surrogate for real-world knowledge, constrained by:

- Formal inference: what follows, what contradicts, what defaults, what changes under new facts.
- Ontological commitment: what kinds of entities, roles, relations, processes, contexts, and purposes the system recognizes.
- Computational realization: what can be stored, queried, transformed, executed, shared, and audited.

This makes representation choice a design decision rather than a taste preference.

### 3. Critical Reading

Strengths:

- The triad of logic, ontology, and computation prevents both vocabulary-only ontologies and formalism-only logic.
- The table of contents forces dynamic and contextual issues into KR rather than leaving them outside the model.
- The index shows broad comparison across paradigms: rules, frames, SQL, Prolog, object systems, conceptual graphs, KIF, Petri nets, controlled language, fuzzy and nonmonotonic logic.
- The preface emphasizes informal specification analysis and ontology selection, which maps well to modern agent and knowledge-base design.

Limits:

- The available local source set is a map, not the full printed book.
- Some technologies in the index are historical, so the skill should preserve design principles rather than recommend legacy tools by default.
- The book's symbolic and ontological center must be complemented by modern retrieval, ML ranking, observability, and governance when building current agent systems.

### 4. Applied Reading

For Codex use, the book distills into one executable capability:

Choose and audit a knowledge representation by starting from reasoning and explanation needs, modeling domain ontology and context, deciding how uncertainty/defaults/change are handled, and building indexes that connect terms, concepts, rules, sources, examples, mappings, and explanations.

## Distilled Skill Direction

The final skill focuses on:

- Knowledge representation selection.
- Semantic and logical modeling.
- Ontology and context scoping.
- Process/change representation.
- Knowledge soup: vagueness, uncertainty, defaults, inconsistency.
- Interoperability across paradigms.
- Index-based knowledge engineering.
- Auditable explanations and revision conditions.

## Evidence Anchors
## Runtime Coverage
- `SKILL.md` contains the executable method, triggers, gates, output formats, failure handling, and boundaries.
- `test-prompts.json` contains portability and compliance expectations.
- `audit.json` points to this local source note rather than external paths.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: John F. Sowa, Knowledge Representation local book materials. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Logic + ontology + computation. A representation must support inference, name what exists, and run in a computable medium.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not choose notation before knowing the reasoning task, context, change model, and interoperability needs.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Sowa’s triad prevents three failures: empty formalism, vocabulary-only ontology, and unexecutable philosophy.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: For any KR proposal, ask what inference it enables, what ontological commitments it makes, and how computation realizes or approximates those commitments.
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
