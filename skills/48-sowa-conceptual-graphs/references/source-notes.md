# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Source Basis
- Distilled source: Conceptual Graphs Around the World - John F. Sowa.
- Source pages and local mirrors were used during generation, but no machine-local path is required or preserved as a runtime dependency.
- This note carries the portable source summary. Runtime execution uses `SKILL.md`.
## Key Concepts Internalized
- conceptual graph
- abstract syntax
- concept
- conceptual relation
- arc
- type hierarchy
- relation hierarchy
- signature
- referent
- designator
- descriptor
- context
- coreference label
- CGIF
- Common Logic
- CLIF
- KIF
- canonical formation rules
- copy
- simplify
- restrict
- unrestrict
- join
- detach
- actor
- defined quantifier
## Portable Overview
# Book Overview: Conceptual Graphs Around the World

Source set: `local source snapshot used during distillation`, `source-map.json`, chapter wrappers, and local originals in `local source snapshot used during distillation`.

Author: John F. Sowa.

## Structural Reading

This source set is best treated as a standards-and-examples handbook, not a narrative monograph. Its central claim is that conceptual graphs provide a graph notation for logic that remains readable to humans, translatable to formal logic, and practical as an interchange format.

The material has five functional parts:

1. Entry and orientation: conceptual graphs as a bridge between Peirce's existential graphs, AI semantic networks, natural language, database design, expert systems, and logic-based formalisms.
2. Standards history: the old ANSI draft is obsolete, while ISO/IEC 24707 Common Logic is the authoritative semantic basis for CGIF.
3. Representation ladder: display form, linear form, CGIF, KIF, predicate calculus, CLIF, and XCL are treated as different concrete forms over compatible logical semantics.
4. Worked examples: simple existential statements, universal quantification, n-adic relations, thematic-role modeling, and nested contexts for belief/desire.
5. Operational semantics: abstract syntax, type and relation hierarchies, referents, contexts, coreference, canonical graph operations, and inference rules.

## Interpretive Reading

Key terms in Sowa's usage:

- Conceptual graph: a bipartite graph whose concept nodes and relation nodes encode logical structure.
- Concept: a node with type and referent; the referent may include a quantifier, designator, and descriptor.
- Conceptual relation: a relation node with valence, ordered arcs, and a signature constraining argument types.
- CGIF: the machine interchange syntax for conceptual graphs, using brackets, parentheses, coreference labels, contexts, and comments.
- Coreference label: `*x` defines a node identity; `?x` refers back to that identity within scope.
- Context: a concept containing a nested graph, used for negation, implication, quoted propositions, situations, modalities, and metalanguage.
- Type hierarchy: a partial order of concept type labels with `Entity` as universal type and `Absurdity` as absurd type.
- Relation hierarchy: a partial order of relation labels, each with valence and a signature.
- Canonical formation rule: graph operation used for equivalence, specialization, or generalization.
- Actor: a relation-like node representing a computable function or externally determined operation.

Core propositions:

- CGs should be designed at the abstract graph level before choosing a concrete notation.
- A useful CG model must make type, referent, relation valence, and argument order explicit.
- CGIF is the normative interchange representation; DF and LF are helpful human notations but can vary.
- Extended CGIF improves readability but must be reducible to core CGIF/Common Logic semantics.
- Translation may preserve truth conditions while losing layout, ordering, comments, or convenient syntax.
- Context boundaries determine quantifier scope and the ontology of asserted versus quoted or hypothetical entities.
- Canonical graph operations support disciplined inference: copy/simplify preserve equivalence, restrict/join specialize, unrestrict/detach generalize.

## Critical Reading

Important limitations:

- The old `source-note section` standard is obsolete; it is useful for methodology and graph operations, but ISO/IEC 24707 Common Logic is the semantic authority.
- The examples predate modern OWL/RDF tooling, SHACL, property graphs, LLM extraction pipelines, and contemporary knowledge graph engineering practice.
- Some research extensions, especially full context semantics, generalized quantifiers, indexicals, and natural-language pragmatics, are explicitly not fully standardized.
- Sowa's formalism is strong for logic-preserving representation but does not solve ontology governance, data quality, provenance, UI usability, or reasoning performance by itself.
- A translation can be logically equivalent while unsuitable for a downstream parser, database schema, or human review workflow.

## Skill Applicability

Skill-worthy units:

- Build a conceptual graph from text, requirements, ontology fragments, or schema assertions.
- Map CG structures to predicate calculus, CLIF, KIF, RDF/OWL-adjacent logic, or validation checks.
- Use canonical graph operations to compare, specialize, generalize, merge, or simplify models.
- Serialize a graph in CGIF while preserving scope, coreference, argument order, and type constraints.
- Audit a conceptual model for ambiguity, quantifier-scope errors, type-signature violations, and unsupported extensions.

Not suitable as standalone skills:

- The bibliography itself.
- Tool directories and conference links.
- Pure historical comparison between ANSI draft and ISO standard.
- Display-form styling variants independent of semantic constraints.

Priority decision: produce one integrated executable Codex skill, because the user's requested trigger is broad and the usable methodology depends on combining modeling, logic mapping, graph operations, interchange, and checks in one workflow.
## Runtime Coverage
- `SKILL.md` contains the executable method, triggers, gates, output formats, failure handling, and boundaries.
- `test-prompts.json` contains portability and compliance expectations.
- `audit.json` points to this local source note rather than external paths.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: John F. Sowa, Conceptual Graphs Around the World local mirror and examples. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Bipartite concept/relation graph -> referents/coreference -> contexts/scope -> CGIF/Common Logic translation -> canonical operations.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not treat conceptual graphs as ordinary diagrams; if type, relation order, identity, and scope are not checked, the method is not being used.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Sowa’s strongest move is to preserve logical commitments across human-readable graphs and machine-readable interchange. Notation is secondary to abstract graph semantics.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Extract concepts, relation valence, referents, identity labels, quantifier scope, contexts, and translation target; then test whether DF/LF/CGIF/logical form preserve the same commitments.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

zing or auditing CGIF/Common Logic interchange, or checking a model for type, referent, coreference, valence, context, and quantifier-scope errors. Do not use for generic diagram drawing, ordinary knowledge-graph marketing copy, pure bibliography/history questions, or graph database queries that do not need formal semantics.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
