# Candidate Frameworks

## F1: Abstract-Syntax-First Modeling

Evidence:

- `cgdpans.htm` defines CGs as notation-independent abstract syntax before concrete syntax.
- `cgexamp.htm` shows DF, LF, CGIF, KIF, and predicate calculus as multiple forms of one abstract graph.

Method:

1. Extract entities, events, properties, and relations from the source problem.
2. Model concepts and conceptual relations as a bipartite graph.
3. Add types, referents, valence, signatures, coreference, and contexts.
4. Only then choose DF/LF/CGIF/CLIF/KIF or another target notation.

Validation:

- V1: supported by standards material and worked examples.
- V2: predicts how to model new requirements without prematurely choosing syntax.
- V3: distinctive because it orders modeling around graph semantics, not display or storage form.

Disposition: accepted into `SKILL.md`.

## F2: Representation Ladder

Evidence:

- `cgexamp.htm` gives side-by-side DF, LF, CGIF, KIF, and predicate-calculus examples.
- `cgif.htm` explains CGIF/CLIF/XCL as Common Logic dialects and warns that translations preserve semantics, not syntax.

Method:

Use a ladder:

1. Human explanation in controlled natural language.
2. Display or linear CG sketch for review.
3. CGIF for interchange.
4. Predicate calculus, CLIF, KIF, RDF/OWL-adjacent subset, or validation rules for formal consumers.

Disposition: accepted into `SKILL.md`.

## F3: Canonical Graph Operations

Evidence:

- `cgdpans.htm` section 9.2 lists copy/simplify, restrict/unrestrict, join/detach.
- Section 9.3 maps those operations to inference effects.

Method:

- Equivalence: copy or simplify redundant subgraphs.
- Specialization: restrict types/referents or join identical concepts.
- Generalization: unrestrict types/referents or detach a concept into two nodes.
- In negative contexts, invert specialization/generalization effects.

Disposition: accepted into `SKILL.md`.

## F4: Context and Scope Discipline

Evidence:

- `cgexamp.htm` uses Tom/Mary/sailor to show nested belief and desire contexts.
- `cgif.htm` discusses Proposition, Situation, IKL, metalevel statements, and context boundaries.
- `cgdpans.htm` uses `If`, `Then`, `Either`, `Or`, negation, transparent contexts, and precedence levels.

Method:

Separate asserted reality from quoted, hypothetical, desired, believed, negated, or conditional graphs. Move concepts across context boundaries only when existence and knowledge commitments really change.

Disposition: accepted into `SKILL.md`.

## F5: CGIF Conformance and Interchange Audit

Evidence:

- `cgdpans.htm` describes conformance pairs, CGIF input/output equivalence, identifiers, labels, and knowledge-base contexts.
- `cgstand.htm` states ISO/IEC 24707 as the official Common Logic standard.

Method:

Validate labels, scopes, valence, type signatures, names/literals, context syntax, extended-feature reduction, and semantic equivalence under round-trip translation.

Disposition: accepted into `SKILL.md`.
