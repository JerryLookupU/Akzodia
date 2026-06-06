---
name: 52-sowa-mathematical-logic-background
description: Use when turning domain language into auditable knowledge models that need sets, relations, graphs, lattices, first-order logic, model-theoretic truth conditions, controlled English, ontology refinement, or a clear object-language/metalanguage boundary.
source_files:
  - references/source-notes.md
---
# 52 Mathematical Logic Background

## Book-Derived Essence

- Core framework: Sets/functions -> relations/graphs -> lattices -> logic/model theory -> controlled language -> object-language/metalangauge boundary.
- Deep idea: The deepest method is representation discipline: choose the mathematical structure that matches the domain commitment, then keep truth conditions outside the language being evaluated.
- Discovery method: Classify the structure as set, relation, graph, lattice, rule, model, or controlled sentence; test arity, quantifiers, truth conditions, and whether metalanguage claims are mixed into object language.
- Boundary: Do not use formal notation to hide vague predicates, missing models, or semantically closed truth claims.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when a task needs ordinary domain language to become a precise, testable knowledge model. Typical triggers:

- You need to transform business rules, policies, database requirements, ontology notes, or controlled natural language into explicit predicates, relations, graphs, constraints, or models.
- A knowledge base is ambiguous because its universe of discourse, entity sets, relation arities, quantifier scope, or truth conditions are not stated.
- A domain taxonomy needs more than a tree: multiple inheritance, subtype joins/meets, attribute-based concept lattices, or ontology refinement.
- You need to explain whether two representations are equivalent: table vs graph, relation vs conceptual graph, hypergraph vs bipartite graph, natural language vs first-order formula.
- You need to decide whether a sentence is true in a model, provable from axioms, under-specified, paradox-prone, or merely syntactically well-formed.
- You are designing controlled English for knowledge entry and want it readable for people while translatable to logic.

Do not use this skill for general math tutoring, philosophical debate about truth, or casual prose editing unless the output must become a formal or semi-formal knowledge model.

## Activation Gate

Trigger only when the user request has both:

1. A domain modeling target, such as policies, rules, data schemas, ontology terms, knowledge-graph facts, controlled-language sentences, or truth-evaluation requirements.
2. A need for formal semantic structure, such as universe of discourse, set membership, functions, relation arity, graph/lattice representation, quantifier scope, first-order formulas, model-theoretic truth, or object-language/metalanguage separation.

If the request is only asking for a definition, biography, philosophical opinion, generic set calculation, UI implementation, or prose rewrite, do not activate this skill.

If the domain input is missing but the user clearly wants a formal model, ask up to three blocking questions before building the artifact:

- What individuals are in scope?
- Which statements, rules, or queries must be represented?
- Should unknown facts be treated as false, unknown, or outside scope?

Proceed with a provisional model only when the user explicitly asks for an example or accepts stated assumptions.

## Source Spine

This skill distills three connected Sowa-site texts:

- `Mathematical Background`: sets, functions, lambda calculus, graphs, relations, lattices, propositional logic, predicate logic, proofs, grammars, game graphs, and model theory.
- `Controlled English`: how a readable English-like notation maps domain words, quantifiers, events, states, and constraints to logic.
- Tarski's `The Semantic Conception of Truth`: why truth definitions require specified language structure, object-language/metalanguage separation, and material adequacy by T-sentences.

Short source anchors:

> "A relation is a function of one or more arguments whose range is the set of truth values"

> "A mathematical structure is a set together with one or more relations or operators defined over the set."

> "Pure logic, which has no built-in ontology, can be applied to any domain whatever."

> "The problem of the definition of truth obtains a precise meaning ... only for those languages whose structure has been exactly specified."

## Core Interpretation

Sowa's mathematical background is not a bag of definitions. It is a representation pipeline:

1. Choose the universe and membership conditions.
2. Build structures from sets, functions, relations, and operators.
3. Move between equivalent external forms: tables, graphs, hypergraphs, conceptual graphs, formulas, grammars, and controlled English.
4. Give those forms truth conditions by mapping formulas to a model.
5. Keep syntax, proof, model, and metalanguage apart so the system can be audited.

The practical lesson is that a knowledge model should not begin with class names. It should begin with the questions: what counts as an individual, what relations can hold, what syntax is allowed, what model makes a statement true, and what representation makes the answer inspectable.

## Hard Rules

- This skill is self-contained for runtime use: apply the modeling procedure below without loading the original Sowa pages unless the user explicitly asks for source audit or deeper reconstruction.
- Do not require the agent or user to read original source files during normal use. This `SKILL.md` contains the executable modeling procedure; `references/source-notes.md` is the local trace artifact for provenance and audit.
- Do not introduce a predicate, relation, function, graph edge, lattice order, or controlled-English template without declaring its domain, range or arity, and intended interpretation.
- Do not call a sentence true unless the object language, model domain, relation extensions or interpretation rules, and evaluation status are stated.
- Do not treat proof, database presence, user assertion, confidence, or workflow approval as model-theoretic truth unless that status is explicitly defined.
- Do not accept a controlled-English sentence unless it can be parsed into a declared logical form or is reported as rejected/ambiguous.
- Do not model subtype as a tree when the domain requires multiple inheritance, meet/join behavior, or attribute-based concept refinement.
- Preserve source trace for modeling choices by tying each major symbol, rule, or assumption to a user sentence, data example, requirement, or explicit assumption.

## Workflow

Use the full workflow for formalization tasks. For small tasks, run only the relevant stages but still satisfy the gate and output contract.

1. Fix the universe of discourse.
   - Name the universal set for the task: all users, all assets, all documents, all workflow states, all events, all products, or another bounded domain.
   - Decide which sets are defined by extension, such as a finite enum, and which are defined by intension, such as a rule or predicate.
   - State whether duplicates matter. Use sets for unique membership, bags for counted occurrences, and sequences when order is semantically meaningful.
   - Record open-world vs closed-world assumptions. A closed-world assumption is acceptable only for bounded inventories or verified tables.
   - Gate: stop or ask questions if the domain boundary, unknown-fact policy, or individual identity rule is absent.

2. Inventory entities, functions, relations, and operators.
   - List individual types and constants.
   - List attributes as monadic predicates or functions only when they have a clear domain and range.
   - List relations with arity: monadic property, dyadic relation, triadic event relation, or n-adic relation.
   - For each relation, specify whether it is intensional, computed by a rule, or extensional, stored as tuples.
   - Mark relation properties when relevant: reflexive, irreflexive, symmetric, asymmetric, antisymmetric, transitive, partial ordering, linear ordering, equivalence relation.
   - Gate: no symbol is ready for formulas or diagrams until its kind, arity/domain/range, and source trace are recorded.

3. Choose a representation that matches the reasoning job.
   - Use relational tables when tuple storage, joins, constraints, and SQL-style queries dominate.
   - Use directed labeled graphs when dyadic relations and path questions dominate.
   - Use hypergraphs or bipartite conceptual graphs when n-adic relations, events, roles, or reified relationships matter.
   - Use lattices when concepts are ordered by subtype, attribute inclusion, generalization/specialization, meet, join, or ontology refinement.
   - Use formulas when quantifier scope, negation, implication, proof, or model-theoretic truth must be explicit.
   - State any intended isomorphism between forms, for example "this table and this graph carry the same tuples."
   - Gate: the chosen representation must name the queries or audits it supports and the information it would lose, if any.

4. Build the concept lattice when taxonomy alone is too weak.
   - Treat subtype as a partial ordering, not automatically as a tree.
   - For each concept, separate intension, the defining attributes, from extension, the individuals it applies to.
   - Use meet/intersection for combining attributes into more specific concepts.
   - Use join/union for least common generalization.
   - Look for impossible, redundant, or unattested attribute combinations. Prefer a compact formal concept analysis style lattice when only observed combinations matter; use a full Leibniz-style attribute lattice only when every possible combination must be considered.
   - When adding an attribute, describe the refinement it causes and which existing nodes split, merge, or remain unlabeled.
   - Gate: lattice output is valid only if the partial order and at least one meet/join or refinement operation are inspectable.

5. Translate controlled English into logical commitments.
   - Separate function words from content words. Function words include articles, quantifiers, connectives, pronouns, `is`, `has`, and selected prepositions.
   - Treat content words as domain vocabulary whose meaning comes from rules, constraints, and ontology definitions.
   - Convert common nouns to types or monadic predicates.
   - Convert verbs to event or state predicates. Reify events when time, participants, provenance, or later reference matters.
   - Convert adjectives and past participles to state predicates or attribute relations.
   - Convert indefinite noun phrases (`a`, `an`, `some`) to introduced variables; convert definite noun phrases and pronouns to resolved references.
   - Preserve quantifier order. `For every x, there exists y` is not equivalent to `There exists y for every x`.
   - Gate: every accepted sentence must have a parse note, resolved variables/references, and a formula or declared template.

6. Compile syntax before semantics.
   - Define terminal symbols, nonterminals, start symbol, and production rules for any controlled language.
   - Classify the grammar complexity needed: regular for simple patterns, context-free for nested structure, context-sensitive when agreement or distant dependencies matter.
   - Define formation rules for formulas: terms, atoms, Boolean combinations, and quantified formulas.
   - Reject sentences that parse in ordinary English but cannot be mapped to a declared logical form.
   - Gate: do not evaluate truth until the object-language syntax or controlled-English templates are fixed.

7. Define truth in a model.
   - Specify the object language: the formulas or controlled sentences being evaluated.
   - Specify the metalanguage: the language used to name expressions, define truth, describe syntax, and state evaluation rules.
   - Avoid semantically closed designs where the same language contains its own truth predicate without hierarchy or safeguards.
   - Define model `M = <D, R>` where `D` is the domain of individuals and `R` is the set of relations over `D`.
   - For each formula `p`, define or approximate an evaluation function `Phi(p, M)` that returns true or false relative to the individuals and relations in the model.
   - Treat truth in a model, provability from axioms, and assertability in a workflow as different statuses.
   - Gate: truth status must be one of `true_in_model`, `false_in_model`, `satisfiable`, `unsatisfiable`, `proved`, `disproved`, `ambiguous`, or `not_formalized`.

8. Validate with proof and model checks.
   - Use proof rules to derive consequences from axioms, definitions, and prior formulas.
   - Check that inference rules preserve truth for the intended semantics.
   - Use model tests to find counterexamples: construct a small domain where the premises hold and see whether the conclusion fails.
   - For formulas with quantifier alternation, run a game-semantics pass: skeptic chooses universal witnesses, proposer chooses existential witnesses, and the atom at the end is checked against the relation extension.
   - Record whether a claim is proved, true in a chosen model, false in a chosen model, satisfiable, inconsistent, or not yet formalized.
   - Gate: include at least one positive example and one counterexample or explain why the model lacks enough data for either.

9. Produce an audit-ready artifact.
   - Include the universe, vocabulary, relation table, representation choice, controlled-English templates, formal formulas, model assumptions, example evaluations, and open questions.
   - Keep every major modeling choice tied to a source sentence, domain example, or required query.
   - Add minimal test cases: one true positive, one false positive, one quantifier-scope trap, one missing-reference case, one ontology-refinement case, and one model counterexample.

## Output Format

For full runs, return this structure. For lightweight runs, include the same headings and mark skipped sections as `not_applicable`.

```markdown
## Modeling Artifact

### Scope And Source Trace
- User goal:
- Source statements or examples:
- Assumptions:
- Open-world/closed-world policy:

### Universe
- Domain `D`:
- Individual identity rule:
- Extensional sets:
- Intensional sets:
- Bags/sequences, if any:

### Vocabulary And Structures
| symbol | kind | domain | range/arity | interpretation | source/assumption |
|---|---|---|---|---|---|

### Representation Choice
- Selected form:
- Reasoning queries supported:
- Equivalent forms or isomorphisms:
- Known information loss:

### Controlled English, If Used
| template/sentence | parse commitments | variables/references | logical form | status |
|---|---|---|---|---|

### Formal Commitments
- Axioms/definitions:
- Constraints:
- Quantifier-scope notes:
- Relation properties:

### Model And Truth Checks
- Object language:
- Metalanguage:
- Model `M = <D, R>`:
- Evaluation rule `Phi(p, M)`:
| claim | formula | status | witness/counterexample | notes |
|---|---|---|---|---|

### Lattice Or Ontology Refinement, If Used
- Partial order:
- Meet/join or refinement operation:
- Split/merge/unlabeled concepts:

### Tests
- True positive:
- False positive:
- Quantifier-scope trap:
- Missing-reference case:
- Ontology-refinement case:
- Model counterexample:

### Residual Risks
- Ambiguities:
- Missing data:
- Toolchain limits:
```

## Failure And Recovery Protocol

- If the universe, unknown-fact policy, or individual identity rule is missing, ask blocking questions before full formalization.
- If a controlled-English sentence has multiple parses, list the competing parses and do not choose silently.
- If relation arity is unclear, prefer an n-adic event/reified relation placeholder over collapsing roles into binary relations.
- If a taxonomy cannot supply meet/join behavior, report it as a partial order or DAG rather than a lattice.
- If model data is incomplete, mark truth checks as `ambiguous` or `not_formalized`; do not infer closed-world falsity unless declared.
- If the requested formalism exceeds first-order logic, state the higher-order/modal/default requirement and hand off to a more specialized skill or toolchain after preserving the first-order boundary.

## Modeling Checklists

### Set And Relation Checklist

- What is the universal set?
- Which sets are extensional lists and which are intensional rules?
- Does order matter? Do duplicates matter?
- What is each relation's arity?
- Is each relation stored, computed, or derived?
- Which relation properties are intended and which are accidental?
- Are equivalence classes, partial orders, or subtype lattices implied?

### Graph Checklist

- Are arcs directed or undirected?
- Are arcs labeled by relation type?
- Are relationships binary, or do they require hyperedges/reified relation nodes?
- Are paths, reachability, cycles, connected components, or cutpoints meaningful queries?
- Is the drawing only an illustration, or is it the formal representation?
- Can the same information be converted to tuples and back without loss?

### Logic Checklist

- Which predicates are properties, relations, events, or states?
- What are the domains and ranges of functions?
- Which variables are bound, and which remain free?
- Does quantifier order match the intended English reading?
- Are implications material implications, rules with operational triggers, or causal claims?
- Which equivalences are definitions, and which are theorems?
- Can the target reasoner handle the chosen expressiveness?

### Truth-Semantics Checklist

- What is the object language?
- What is the metalanguage?
- What names expressions of the object language?
- Does the metalanguage contain enough structure to define satisfaction/truth?
- Is truth being confused with proof, database presence, confidence, user assertion, or current belief?
- Could a self-referential truth claim create a liar-style problem?

### Controlled-English Checklist

- Is every content word introduced by rules or constraints?
- Are function words restricted enough to parse deterministically?
- Are pronouns and definite descriptions resolved to prior variables?
- Are events/states reified when later rules need to refer to them?
- Are conversational implicatures excluded unless explicitly represented?
- Can every accepted sentence be translated to a logical form?

## Failure Modes

- Starting with a class hierarchy when the domain really needs n-adic relations, events, or role-labeled graphs.
- Treating a diagram as the formal graph without specifying node and arc sets.
- Assuming a taxonomy is a tree when multiple inheritance or lattice joins are required.
- Treating database rows as truth without stating closed-world assumptions and source validity.
- Letting controlled English inherit ordinary English implicatures such as temporal order from `and` without explicit rules.
- Confusing a proof with a model evaluation: a formula may be true in a model, provable from axioms, both, or neither.
- Defining truth in the same unrestricted language that contains its own truth predicate.
- Losing quantifier scope during translation from English to logic.
- Overformalizing a low-risk task where a simple schema and examples would be sufficient.

## Boundaries

- This skill gives a practical knowledge-modeling workflow inspired by Sowa and Tarski; it is not a complete theorem prover or model checker.
- It favors first-order and controlled-language representations. Use higher-order logic only when quantification over predicates/functions is essential and the toolchain supports it.
- It does not decide domain truth by itself. Domain experts or authoritative data must supply the intended model.
- It complements ontology engineering, knowledge representation, and database design skills; use those for deeper implementation details once the representation boundary is clear.

## Related Skills

- `07-ontological-engineering` for building and governing ontologies after the logical structure is chosen.
- `08-knowledge-representation-and-reasoning` for orchestrator-level belief, defaults, exceptions, and action reasoning.
- `44-knowledge-engineering` for eliciting domain knowledge and maintaining knowledge-base workflows.

## Source Closure

This 52-sowa-mathematical-logic-background skill is self-contained for runtime use; its source basis is John F. Sowa mathematical logic background: sets, relations, graphs, lattices, controlled English, truth semantics. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
