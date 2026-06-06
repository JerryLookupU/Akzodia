# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Source Basis
- Distilled source: Sowa Mathematical Logic Background for Knowledge Modeling.
- Source pages and local mirrors were used during generation, but no machine-local path is required or preserved as a runtime dependency.
- This note carries the portable source summary. Runtime execution uses `SKILL.md`.
## Key Concepts Internalized
- universe of discourse
- extension and intension
- sets, bags, and sequences
- functions, mappings, operators, domain and range
- relations as truth-valued functions
- relation arity and relation properties
- graphs, labeled graphs, hypergraphs, bipartite graphs, conceptual graphs
- partial orders, lattices, subtype hierarchies, meet and join
- duality of intension and extension
- formal concept analysis and ontology refinement
- propositional and predicate logic
- quantifier scope and bound variables
- axioms, proof, soundness, completeness
- formal grammars and recursive definitions
- model theory and evaluation functions
- game-theoretic semantics
- controlled English and function/content words
- object language and metalanguage
- semantic closure and liar-style antinomy
- truth versus provability
## Portable Overview
# Book Overview: Mathematical Background

## Identity

- Title: Mathematical Background
- Primary author/source compiler: John F. Sowa
- Included source texts: Sowa's `Mathematical Background`, Sowa's `Controlled English`, and Alfred Tarski's `The Semantic Conception of Truth`
- Local source package: `local source snapshot used during distillation`
- Chapter count: 3

## Adler Stage 0 Reading

### 1. Structural Reading

The source bundle is organized as a mathematical and logical background for knowledge representation:

1. `Mathematical Background` supplies the formal substrate: sets, functions, lambda calculus, graphs, relations, lattices, propositional logic, predicate logic, axioms/proofs, formal grammars, game graphs, and model theory.
2. `Controlled English` shows how English-like statements can be restricted enough to translate into typed predicate calculus, discourse representation structures, conceptual graphs, SQL-like constraints, frames, or programs.
3. `The Semantic Conception of Truth` explains why truth definitions require an exactly specified language, object-language/metalanguage separation, non-semantic primitives in the metalanguage, satisfaction, and material adequacy by T-style equivalences.

The reading order moves from representation primitives to controlled human notation to semantics:

```text
sets/functions -> relations/graphs/lattices -> logic/proofs/grammar -> model theory
             -> controlled English -> object-language/metalanguage truth semantics
```

### 2. Interpretive Reading

The central argument for a knowledge modeler is:

- A domain must first be bounded as a universe of discourse.
- Concepts and facts become sets, functions, and relations.
- Relations can be stored as tuples, drawn as graphs, generalized into hypergraphs, or reified as conceptual graph relation nodes.
- Type systems and ontologies are partial orders, and often lattices rather than trees.
- Natural-language requirements can be made usable by restricting grammar and vocabulary, then translating function words and content words into logical forms.
- Syntax and proof do not settle truth by themselves; truth is evaluated relative to a model.
- Any system that talks about the truth of its own sentences must distinguish the language being described from the language doing the describing.

In engineering terms, the book teaches a disciplined conversion from prose to an auditable semantic artifact.

### 3. Critical Reading

Strengths:

- The text repeatedly connects abstract definitions to implementable representations: tables, pointers, graphs, grammars, logic formulas, and database constraints.
- It emphasizes representation equivalence, especially relation/table/graph conversions and hypergraph/bipartite graph isomorphism.
- It keeps syntax, proof theory, and model theory separate, which is essential for debugging knowledge systems.
- Controlled English is treated as an interface layer, not as magic natural-language understanding.

Limitations:

- The source is introductory and does not provide complete algorithms for theorem proving, model checking, ontology alignment, or CNL parser construction.
- Some implementation examples reflect older systems and notations, so the skill should extract durable modeling moves rather than copy surface syntax.
- Tarski's text is philosophically and technically dense; the operational takeaway should be object-language/metalanguage discipline and satisfaction-based truth, not a full reconstruction of formal semantics.

### 4. Applied Reading

The distilled skill should help Codex:

- Convert domain requirements into explicit sets, relations, graphs, lattices, controlled English, and formulas.
- Detect ambiguity in quantifier scope, relation arity, pronoun/reference resolution, and truth conditions.
- Decide whether an ontology needs a tree, DAG, lattice, or formal concept analysis pass.
- Avoid confusing stored facts, asserted facts, provable formulas, model truth, and user belief.
- Produce artifacts that a knowledge engineer can test: vocabulary, grammar, formulas, model, examples, counterexamples, and audit notes.

## Chapter Notes

### 1. Mathematical Background

Key takeaways:

- Set definitions by extension and intension are the entry point for domain boundaries.
- Recursive definitions support infinite or generated sets, including formal grammars.
- Functions require explicit domain and range; isomorphisms let different physical or data representations carry the same abstract structure.
- Relations are truth-valued functions and can be represented by tuples, predicates, or graphs.
- Labeled graphs, hypergraphs, and bipartite graphs support multiple or n-adic relations.
- Lattices capture partial orderings, subtype relations, meet/join, and ontology refinement.
- Predicate logic adds quantifiers and internal proposition structure; proof theory derives formulas, while model theory evaluates formulas in a model.
- Game-theoretic semantics offers an operational way to evaluate quantified formulas by alternating choices between proposer and skeptic.
## Runtime Coverage
- `SKILL.md` contains the executable method, triggers, gates, output formats, failure handling, and boundaries.
- `test-prompts.json` contains portability and compliance expectations.
- `audit.json` points to this local source note rather than external paths.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: John F. Sowa mathematical logic background: sets, relations, graphs, lattices, controlled English, truth semantics. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Sets/functions -> relations/graphs -> lattices -> logic/model theory -> controlled language -> object-language/metalangauge boundary.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use formal notation to hide vague predicates, missing models, or semantically closed truth claims.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The deepest method is representation discipline: choose the mathematical structure that matches the domain commitment, then keep truth conditions outside the language being evaluated.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Classify the structure as set, relation, graph, lattice, rule, model, or controlled sentence; test arity, quantifiers, truth conditions, and whether metalanguage claims are mixed into object language.
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
