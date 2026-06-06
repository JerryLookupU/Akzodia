# Candidate Principles

## P1: Preserve semantics before notation

Do not optimize for pretty diagrams, English-like phrasing, or compact CGIF until the graph's logical commitments are explicit.

Accepted.

## P2: Make existential defaults explicit during audit

Blank referents normally carry existential force. During review, rewrite implicit existentials so hidden commitments are visible.

Accepted.

## P3: Treat types as constraints, not just labels

A relation signature constrains the types that can fill each argument position. A type mismatch is a modeling defect even when a loose logical representation could simply evaluate false.

Accepted.

## P4: Coreference is identity under scope

`*x` and `?x` are not decorative variables. They encode identity links between concepts and must resolve uniquely in the same or containing context.

Accepted.

## P5: Extended syntax is a readability layer

Extended CGIF features such as type labels, universal quantifiers, Boolean contexts, and nested concepts make models readable, but their semantics should be reducible to core CGIF/Common Logic.

Accepted.

## P6: Translation equivalence is not round-trip identity

Moving between CGIF, CLIF, KIF, predicate calculus, and display forms can preserve truth conditions while reordering nodes, replacing subexpressions, and losing formatting or stylistic choices.

Accepted.

## P7: Negative contexts reverse operational direction

Specialization/generalization rules operate normally in positive contexts, but negation reverses their inferential direction.

Accepted.
