# Candidate Frameworks

## F1. Prose To Model Pipeline

Candidate:

1. Bound the universe of discourse.
2. Define sets by extension or intension.
3. Identify functions, relations, and operators.
4. Choose table, graph, lattice, formula, or controlled-language representation.
5. Define a model and evaluation function.
6. Test truth, proof, and counterexamples separately.

Evidence:

- `source-note section` starts with sets and proceeds through relations, graphs, logic, grammars, games, and model theory.
- `source-note section` shows controlled English rules compiling to DRS, conceptual graphs, and predicate calculus.
- `source-note section` supplies the truth-definition boundary for formalized languages.

Triple verification:

- V1 cross-source: supported by all three source texts.
- V2 predictive: answers new modeling tasks by forcing a sequence from domain boundary to truth check.
- V3 distinctiveness: more specific than "be precise"; it names representation layers and semantic checks.

Status: accepted.

## F2. Representation Equivalence Framework

Candidate:

When two notations appear different, compare their underlying individuals, tuple sets, relation labels, and isomorphisms. Tables, graphs, hypergraphs, bipartite graphs, conceptual graphs, and formulas may preserve the same information if the mapping is explicit.

Evidence:

- `source-note section` states that graphs and dyadic relations can represent the same information in logically equivalent ways.
- It also explains hypergraphs and bipartite graphs as isomorphic representations for n-adic relations.
- `source-note section` maps ACE to DRS, conceptual graphs, and predicate calculus.

Triple verification:

- V1 cross-source: supported by math and controlled English chapters.
- V2 predictive: helps decide whether a graph database schema preserves an n-ary relation.
- V3 distinctiveness: avoids surface-format arguments by checking information preservation.

Status: accepted.

## F3. Object-Language / Metalanguage Boundary

Candidate:

Any system that defines or evaluates truth for its own expressions must separate the language being evaluated from the language doing the evaluation.

Evidence:

- `source-note section` rejects semantically closed languages and defines object language and metalanguage.
- `source-note section` model theory section points to Tarski and evaluation functions.
- Controlled English requires a parser/translator outside the accepted object sentences.

Triple verification:

- V1 cross-source: supported by Tarski, math model theory, and ACE translation architecture.
- V2 predictive: catches unsafe rule languages with unrestricted self-truth predicates.
- V3 distinctiveness: a precise semantic safety rule, not generic caution.

Status: accepted.

## F4. Lattice-Based Ontology Refinement

Candidate:

When concept types depend on multiple attributes, represent them as a partial order or lattice, then refine the lattice as attributes are added.

Evidence:

- `source-note section` defines lattices, bounded lattices, meet/join, subtype partial ordering, Leibniz attribute products, bit strings, and formal concept analysis.
- The beverage example shows redundant attributes and compact FCA lattices.

Triple verification:

- V1 cross-source: strongly supported in mathematical background; adjacent support from ACE content-word ontology.
- V2 predictive: decides whether a taxonomy needs tree, DAG, or lattice treatment.
- V3 distinctiveness: concrete ontology operation with meet/join and refinement behavior.

Status: accepted.
