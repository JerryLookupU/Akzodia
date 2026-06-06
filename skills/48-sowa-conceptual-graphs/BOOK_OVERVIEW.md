# Book Overview: Conceptual Graphs Around the World

Source set: `site-sowa/books/conceptual-graphs/BOOK.md`, `source-map.json`, chapter wrappers, and local originals in `site-sowa/cg/*.htm`.

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

- The old `cgdpans.htm` standard is obsolete; it is useful for methodology and graph operations, but ISO/IEC 24707 Common Logic is the semantic authority.
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
