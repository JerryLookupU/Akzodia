# Candidate Cases

## C1. Library Database In Controlled English

Source:

- `source-note section`, Library Database section.

Method unit:

- Express rules and constraints in readable ACE.
- Translate rules to DRS.
- Map DRS to conceptual graphs.
- Translate to typed predicate calculus.
- Compile constraints to frames, SQL definitions, Java declarations, UML, or E-R diagrams.

Why retained:

This is the most concrete end-to-end example of readable language becoming executable knowledge representation.

## C2. Employee And Manager Sentences

Source:

- `source-note section`, opening ACE examples.

Method unit:

- Treat `every`, `a`, and content nouns/verbs as signals for typed variables and predicates.
- Demonstrate that content words are not predefined ontology; their meaning is determined by statements.

Why retained:

It is a compact example for quantifiers, types, and content-word introduction.

## C3. Beverage Lattice

Source:

- `source-note section`, Lattices section.

Method unit:

- Start with concept types and attributes.
- Build an FCA lattice from observed combinations.
- Add attributes such as `madeFromGrapes` and `madeFromGrain` to refine ambiguous nodes.
- Detect redundant attributes such as `nonalcoholic` as complement of `alcoholic`.

Why retained:

It shows ontology refinement as a concrete operation rather than a static hierarchy.

## C4. Relations As Graphs And Conceptual Graphs

Source:

- `source-note section`, Representing Relations by Graphs.

Method unit:

- Convert dyadic relations to graph arcs.
- Use labels for multiple relations.
- Use hypergraphs or bipartite graphs for n-adic relations.
- Interpret conceptual graphs as labeled bipartite graphs.

Why retained:

This drives representation selection for knowledge graphs, relational schemas, and conceptual graph modeling.

## C5. Game-Theoretic Model Evaluation

Source:

- `source-note section`, Model Theory section.

Method unit:

- Treat formula evaluation as a proposer/skeptic game.
- Universal quantifiers give choice to the skeptic; existential quantifiers give choice to the proposer.
- Boolean operators determine which side chooses subformulas.
- Atomic outcomes are checked against relation extensions.

Why retained:

It operationalizes model-theoretic truth for engineers who need a procedure, not only a definition.
