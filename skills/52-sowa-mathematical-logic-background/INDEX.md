# Index: Sowa Mathematical Logic Background Skill

## Skill

- `52-sowa-mathematical-logic-background`: Converts domain language into auditable knowledge models using sets, relations, graphs, lattices, controlled English, logic, model theory, and truth-semantics boundaries.

## Source Map

| Source | Role in skill |
|---|---|
| `BOOK.md` | Reading order and local source index |
| `source-map.json` | Chapter metadata and local HTML mapping |
| `chapters/01-mathematical-background.md` and `logic/math.htm` | Mathematical structures, logic, grammars, model theory |
| `chapters/02-controlled-english.md` and `logic/ace.htm` | Controlled English to typed logic, DRS, CG, constraints |
| `chapters/03-the-semantic-conception-of-truth.md` and `logic/tarski.htm` | Truth semantics, object language, metalanguage, semantic closure |

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

## Related Existing Skills

- `07-ontological-engineering`
- `08-knowledge-representation-and-reasoning`
- `44-knowledge-engineering`

Use this skill before those when the domain language still lacks clear formal structure, truth conditions, or representation boundaries.
