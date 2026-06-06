# Candidate Principles

## P1. State The Universal Set Before Modeling Subsets

If the universe is unstated, membership, complement, negation, and closed-world claims are ambiguous.

Status: accepted.

## P2. Arity Before Storage

Choose the arity and meaning of a relation before choosing a table, edge, property, or object representation. Dyadic relations can become graph arcs; n-adic relations need tuples, hyperedges, or reified relation nodes.

Status: accepted.

## P3. Intension And Extension Are Different Commitments

An extensional list states current members or true tuples. An intensional rule states the property or computation that determines membership. Do not silently substitute one for the other.

Status: accepted.

## P4. Diagrams Are Illustrations Until Formalized

A graph drawing is not the graph. The formal graph is the node set plus arc set, with direction and labels declared.

Status: accepted.

## P5. Quantifier Order Is Semantic

Changing `forall x exists y` to `exists y forall x` changes the claim, even when the English words look similar.

Status: accepted.

## P6. Controlled English Must Restrict Implicature

Natural English often imports conversational assumptions. Controlled English should admit only the implications its grammar and translation rules define.

Status: accepted.

## P7. Truth, Proof, And Assertion Are Distinct

A sentence may be true in a model, provable from axioms, asserted by a user, stored in a database, or believed by a system. These statuses should not be collapsed.

Status: accepted.

## P8. Avoid Semantic Closure Without Hierarchy

A language that contains its own truth predicate and enough ordinary logic can generate liar-style contradictions. Use object-language/metalanguage hierarchy or a restricted truth mechanism.

Status: accepted.
