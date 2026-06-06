# Rejected And Merged Units

## Rejected: Author Persona Skill

- Candidate: answer as John F. Sowa or imitate the author's style.
- Reason: book2skill boundary excludes author role-play. The user requested an executable Codex skill.
- Verification result: failed V2 for design utility.

## Rejected: Simple Book Summary Skill

- Candidate: summarize the book chapter by chapter.
- Reason: user asked for a rich executable skill, not a book review. Local source also lacks full chapter prose.
- Verification result: failed V2 and boundary fit.

## Rejected: Conceptual Graphs Only

- Candidate: always model knowledge with conceptual graphs.
- Reason: source highlights conceptual graphs but also compares predicate calculus, KIF, rules, frames, OO systems, SQL, Prolog, Petri nets, and natural language semantics.
- Verification result: failed V1 as exclusive recommendation; merged into representation selection.

## Rejected: Ontology Engineering Only

- Candidate: make the skill only about building ontologies.
- Reason: Sowa's frame is logic + ontology + computation. The TOC also emphasizes processes, contexts, agents, uncertainty, sharing, and representation mapping.
- Verification result: failed V1 coverage.

## Rejected: Pure Formal Logic Workflow

- Candidate: formalize every problem in predicate logic before implementation.
- Reason: chapter 6 explicitly addresses limitations of logic and real-world knowledge soup; preface includes multiple computational representations.
- Verification result: failed V1 and V2.

## Rejected: Generic Knowledge Management

- Candidate: organize documents, tags, and notes.
- Reason: too broad and too obvious; lacks Sowa-specific inference, ontology, computation, context, representation, and explanation machinery.
- Verification result: failed V3.

## Merged: Knowledge Acquisition Tooling

- Candidate: separate skill for acquiring knowledge from experts and documents.
- Reason: useful but overlaps with existing `44-knowledge-engineering`; retained as index-based knowledge engineering inside this skill.
- Verification result: accepted as subroutine, not standalone.

## Merged: Semantic Interoperability

- Candidate: separate skill for mapping schemas and ontologies.
- Reason: accepted but folded into the final execution workflow because representation choice and translation loss are inseparable.
- Verification result: accepted as subroutine.
