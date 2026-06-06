# Book Overview: Mathematical Background

## Identity

- Title: Mathematical Background
- Primary author/source compiler: John F. Sowa
- Included source texts: Sowa's `Mathematical Background`, Sowa's `Controlled English`, and Alfred Tarski's `The Semantic Conception of Truth`
- Local source package: `site-sowa/books/mathematical-background`
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

### 2. Controlled English

Key takeaways:

- A controlled natural language supports both readability and machine translation.
- ACE is intentionally ontologically light: function words are predefined, content words are introduced by the domain statements.
- Nouns map to type labels or monadic predicates; verbs map to state/event predicates; prepositions and adjectives contribute relations or state predicates.
- Indefinite noun phrases introduce variables; definite phrases and pronouns refer back to prior variables.
- Constraints and rules can compile to logic, frames, SQL definitions, Java declarations, UML, or E-R diagrams when the semantic commitments are explicit.
- Ordinary English implicatures, such as temporal ordering from `and`, must not be imported unless the controlled language specifies them.

### 3. The Semantic Conception of Truth

Key takeaways:

- Truth is treated semantically: a sentence is true in relation to what it says about a domain.
- Material adequacy requires instances of the T-schema: the name of a sentence is true if and only if the sentence itself holds.
- Natural language is too structurally vague for a rigorous general truth definition; formalized or exactly specified languages are required.
- Semantically closed languages that contain their own truth predicate can generate liar-style contradictions.
- The object language is the language being talked about; the metalanguage is the language used to define truth for it.
- Satisfaction is defined recursively, and truth for sentences follows from satisfaction.
- Truth and provability do not coincide in sufficiently rich formal systems.

## Skill Design Decision

This source bundle supports one broad executable skill rather than many narrow skills because the parts are meant to be used together in knowledge modeling:

- Sets/relations/graphs/lattices answer "what structure represents the domain?"
- Controlled English answers "how can people write valid domain statements?"
- Predicate logic/proof/model theory answers "what follows, and what is true in a model?"
- Tarski answers "how do we avoid semantic self-reference errors and define truth cleanly?"

The resulting skill is therefore organized as a modeling workflow with checklists, failure modes, and trigger tests.
