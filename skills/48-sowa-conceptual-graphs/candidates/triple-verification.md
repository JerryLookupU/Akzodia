# Triple Verification

## Verified Unit: Integrated Conceptual Graph Modeling Skill

Type: framework plus execution checklist.

V1 cross-domain:

- Examples chapter demonstrates notation mapping across cat/mat, every-cat, go-to-Boston, triadic `Betw`, and nested belief/desire.
- Summary chapter ties CGIF to Common Logic, CLIF, XCL, RDF/OWL subset semantics, actors, and contexts.
- Old standard chapter defines abstract syntax, type/relation hierarchies, referents, CGIF syntax, canonical operations, and inference rules.

Passed: true.

V2 predictive power:

- Novel question: "How should an agent model 'Alice thinks every invoice over $10,000 requires CFO approval, but Bob disputes one invoice'?"
- Derived answer: create asserted actors/entities outside belief contexts only when committed as real; put Alice's policy in a Proposition context; represent `every invoice over 10000` with a defined quantifier or expanded implication; model Bob's dispute as another proposition with separate source; serialize coreference labels for the same invoice only if identity is asserted.

Passed: true.

V3 exclusivity:

- This is not generic "draw a knowledge graph" advice. The distinctive CG method uses bipartite concept/relation graphs, referent fields, contexts as nested concepts, canonical formation rules, CGIF coreference labels, and Common Logic translation discipline.

Passed: true.

Disposition: accepted into `SKILL.md`.
