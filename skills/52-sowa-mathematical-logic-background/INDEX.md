# Index: Sowa Mathematical Logic Background Skill

## Skill

- `52-sowa-mathematical-logic-background`: Converts domain language into auditable knowledge models using sets, relations, graphs, lattices, controlled English, logic, model theory, and truth-semantics boundaries.
- Runtime contract: `SKILL.md` is self-contained for normal use. The book overview, candidates, rejected units, and audit file preserve source trace and distillation evidence; they are not required to execute the modeling workflow.

## Source Map

| Source | Role in skill |
|---|---|
| `BOOK.md` | Reading order and local source index |
| `source-map.json` | Chapter metadata and local HTML mapping |
| `references/source-notes.md` and `source-note section` | Mathematical structures, logic, grammars, model theory |
| `references/source-notes.md` and `source-note section` | Controlled English to typed logic, DRS, CG, constraints |
| `references/source-notes.md` and `source-note section` | Truth semantics, object language, metalanguage, semantic closure |

## Concept Link Graph

```mermaid
graph TD
  A[Universe of discourse] --> B[Sets: extension/intension]
  B --> C[Functions and operators]
  B --> D[Relations as truth-valued functions]
  D --> E[Tables and tuples]
  D --> F[Graphs and labeled arcs]
  D --> G[Hypergraphs and bipartite CGs]
  D --> H[Predicate logic]
  B --> I[Lattices and subtype partial orders]
  I --> J[Ontology refinement and FCA]
  H --> K[Proof theory]
  H --> L[Model theory]
  L --> M[Evaluation function Phi(p,M)]
  L --> N[Game-theoretic semantics]
  O[Controlled English] --> H
  O --> G
  P[Formal grammar] --> O
  Q[Object language] --> R[Metalanguage]
  R --> S[Truth and satisfaction definitions]
  S --> L
```

## Candidate And Rejection Audit

- Candidate extraction files live in `candidates/`.
- Rejected or merged units live in `rejected/`.
- Final quality and source checks live in `audit.json`.
- Closed-loop review notes in `audit.json` confirm the activation gate, machine-checkable gates, failure recovery protocol, standard output format, and test prompt coverage added during the 2026-06-06 optimization pass.

## Execution Surface

Use `SKILL.md` directly to produce:

- Universe, set, bag, and sequence boundaries.
- Function, operator, and relation inventories with arity/domain/range.
- Representation decisions across tables, labeled graphs, hypergraphs, bipartite conceptual graphs, formulas, and lattices.
- Controlled-English parsing commitments and first-order translations.
- Object-language/metalanguage boundaries, model definitions, truth statuses, witnesses, and counterexamples.
- Audit-ready tests and residual-risk notes.

## Related Existing Skills

- `07-ontological-engineering`
- `08-knowledge-representation-and-reasoning`
- `44-knowledge-engineering`

Use this skill before those when the domain language still lacks clear formal structure, truth conditions, or representation boundaries.
