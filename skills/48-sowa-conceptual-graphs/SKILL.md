---
name: 48-sowa-conceptual-graphs
description: |
  Use when the user needs Sowa-style conceptual graphs for knowledge representation: extracting concepts/relations from text or requirements, mapping a statement to logic, comparing or transforming graphs with canonical CG operations, serializing or auditing CGIF/Common Logic interchange, or checking a model for type, referent, coreference, valence, context, and quantifier-scope errors. Do not use for generic diagram drawing, ordinary knowledge-graph marketing copy, pure bibliography/history questions, or graph database queries that do not need formal semantics.
source_book: "Conceptual Graphs Around the World - John F. Sowa"
source_files:
  - "site-sowa/books/conceptual-graphs/BOOK.md"
  - "site-sowa/books/conceptual-graphs/source-map.json"
  - "site-sowa/cg/cgexamp.htm"
  - "site-sowa/cg/cgif.htm"
  - "site-sowa/cg/cgdpans.htm"
  - "site-sowa/cg/cgstand.htm"
tags:
  - knowledge-representation
  - conceptual-graphs
  - common-logic
  - cgif
  - ontology-modeling
  - logic-mapping
related_skills: []
---

# Sowa Conceptual Graphs

Use this skill to turn ambiguous language, requirements, schema fragments, or ontology assertions into conceptual graphs that have explicit logical commitments. The working product may be a human-readable graph sketch, CGIF, a predicate-calculus/CLIF/KIF-style mapping, or a modeling audit.

## R - Reading Anchors

The source set repeatedly treats CGs as a logic-oriented graph representation that is readable by humans, translatable to formal logic, and usable for computer interchange.

Source anchors:

- `cgexamp.htm`: examples translate the same graph across display form, linear form, CGIF, KIF, and predicate calculus.
- `cgif.htm`: CGIF is tied to Common Logic dialects and warns that semantically equivalent translations may reorder or replace syntax.
- `cgdpans.htm`: abstract syntax defines concepts, conceptual relations, arcs, type/relation hierarchies, referents, contexts, coreference, and canonical formation rules.
- `cgstand.htm`: ISO/IEC 24707 Common Logic is the official semantic standard; old ANSI material is historical but useful for methodology.

## I - Interpretation

Conceptual graphs are not just node-link diagrams. They are a disciplined bridge between natural language, ontology design, and formal logic.

The core move is to model a statement as a bipartite graph:

- Concept nodes represent entities, events, propositions, situations, values, sets, or ranges.
- Conceptual relation nodes represent typed relations whose arcs have ordered argument positions.
- A concept has a type and a referent. The referent may include a quantifier, designator, and descriptor.
- A relation has valence and a signature. The signature constrains which concept types may fill each arc position.
- Coreference labels encode identity within scope.
- Contexts are concepts that contain nested graphs; they define scope for negation, conditionals, belief, desire, quotation, modalities, and metalevel claims.
- CGIF is the interchange syntax; DF/LF are review notations; CLIF/KIF/predicate calculus are logic targets.

The practical test is not whether the graph looks good. The test is whether a downstream reader can recover the same commitments about existence, identity, type, relation order, scope, and implication.

## A1 - Past Applications From The Source

1. Minimal assertion: "A cat is on a mat" becomes concepts for Cat and Mat plus an On relation. CGIF can either define concept labels and bind them in `(On ?x ?y)` or nest concepts directly in `(On [Cat] [Mat])`.
2. Universal quantification: "Every cat is on a mat" uses a defined quantifier such as `@every`, but the audit expands it to nested negations or an implication reading so scope is visible.
3. Event roles: "John is going to Boston by bus" uses a Go event concept linked by Agnt, Dest, and Inst relations to Person, City, and Bus concepts.
4. N-adic relation: "A person is between a rock and a hard place" demonstrates a triadic relation where arc order is part of the meaning.
5. Nested mental context: "Tom believes that Mary wants to marry a sailor" separates what is asserted in the outer world from what exists only inside Tom's belief and Mary's desired situation.
6. Actor/function modeling: algebraic functions are represented as actor nodes with input and output arcs, with limitations when translated to function-oriented target notations.

## A2 - Future Triggers

Use this skill when the user asks for any of the following:

- "Represent this sentence/requirement/domain as a conceptual graph."
- "Give me CGIF, CLIF, KIF, predicate calculus, or a Common Logic mapping."
- "Check whether these graph fragments are equivalent, more specific, or more general."
- "Merge these two concepts if they refer to the same thing."
- "Audit this knowledge representation for quantifier scope, coreference, relation arity, or type errors."
- "Model belief, desire, rule conditions, exceptions, nested claims, or quoted propositions."
- "Translate between human-readable graph notation and a machine interchange format."

Do not use it for:

- Generic graph visualization.
- Graph database query generation unless formal semantics are requested.
- RDF/OWL discussion unless the user asks for logical mapping or semantic subset boundaries.
- Current standards procurement, price, or legal compliance lookup.
- Biographical or historical summaries.

## E - Execution

### Step 1: Decide the output contract

Ask or infer the intended artifact:

- Human review sketch: compact LF-like notation is acceptable.
- Machine interchange: produce CGIF.
- Formal reasoning: produce predicate-calculus, CLIF, KIF-style, or Common Logic mapping.
- Audit: produce findings with model corrections.
- Comparison: classify graph transformations as equivalence, specialization, or generalization.

Completion check: state the target artifact and the semantic commitments it must preserve.

### Step 2: Extract candidate propositions

Break the input into assertions, rules, questions, beliefs, desires, constraints, and exceptions.

For each proposition, record:

- Polarity: asserted, negated, hypothetical, disputed, quoted, desired, believed, possible, necessary.
- Quantification: some, every, no, exactly one, at least N, a certain one, generic set, sequence.
- Identity: same individual, possible same individual, different individuals, unknown.
- Time/modality/source if relevant.

Completion check: every clause that changes truth conditions or scope has its own line.

### Step 3: Build the abstract graph before syntax

Create concepts first:

```text
[Type: referent]
[EventType *e]
[Proposition: nested-CG]
[Situation: nested-CG]
```

Create conceptual relations second:

```text
(Relation argument1 argument2 ...)
(Agnt event agent)
(Thme event theme)
(Dest event destination)
(Inst event instrument)
(Attr entity attribute)
(Dscr situation proposition)
```

Rules:

- Use concept nodes for entities, events, propositions, situations, properties, literals, sets, and functions.
- Use relation nodes for roles and constraints.
- Keep the graph bipartite: relations connect to concepts, not directly to other relations.
- Treat events as concepts when they have participants, attributes, time, cause, modality, or provenance.
- Do not create a direct edge just because two words are adjacent in English.

Completion check: every relation has a named type, ordered arguments, and concept endpoints.

### Step 4: Assign type and relation signatures

For each relation type, define:

```text
Relation: valence N
Signature: (Type1, Type2, ...)
Reading: relation(argument1, argument2, ...)
```

Examples:

```text
Agnt: valence 2, signature (Act, Animate)
Dest: valence 2, signature (Act, Place)
Inst: valence 2, signature (Act, Entity)
Betw: valence 3, signature (Entity, Entity, Entity)
```

Checks:

- The number of arcs equals the relation valence.
- Argument order is stable across examples and serializations.
- Each argument type is the required type or a subtype.
- Defined relation labels can be expanded to lambda-style definitions if needed.
- Relation labels of different valence are not treated as the same relation.

Completion check: no relation appears without valence and intended argument order.

### Step 5: Resolve referents and coreference

Use referent fields deliberately:

- Blank referent: implicit existential, such as `[Cat]`.
- Name: conventional designator, such as `[Person: John]`.
- Literal: quoted value, such as `[String: "paid"]` or `[Amount: 5000]`.
- Individual marker: catalog identity, such as `[Invoice: #23846]`.
- Indexical: implementation-dependent pointer, such as `[Person: #you]`; avoid unless the resolution rule is specified.
- Descriptor: nested graph describing a referent.

Use coreference labels:

```text
[Cat: *x] [Pet: ?x]
(Attr ?x [Happy])
```

Rules:

- A defining label `*x` introduces the identity.
- A bound label `?x` must resolve to exactly one defining label in the same or containing context.
- Do not join two nodes because names look similar; join only when identity is asserted or supported.
- When importing graph fragments, rename labels that collide within overlapping scope.
- If identity is uncertain, keep two concepts and add an explicit relation such as `(PossibleSameAs ?a ?b)` rather than joining.

Completion check: every `?label` resolves uniquely, and every identity commitment is justified.

### Step 6: Place contexts and quantifiers

Use contexts when the nested graph is not simply asserted in the outer world.

Common context patterns:

```text
~[ CG ]                         # negation
[If CG [Then CG]]               # implication
[Either [Or CG] [Or CG]]        # disjunction
[Proposition: CG]               # quoted proposition
[Situation: CG]                 # situation described by CG
```

Scope discipline:

- Concepts outside a context are asserted in the containing context.
- Concepts inside a belief/desire/proposition context are not automatically real in the outer context.
- Moving a concept outside a context changes existence and knowledge commitments.
- `@every` normally scopes over default existentials in the same context.
- For ambiguous quantifier order, use explicit nested contexts rather than relying on precedence.
- In negative contexts, specialization/generalization effects reverse.

Audit question: "If this belief, rule, condition, or desire is false, which concepts still exist in the outer model?"

Completion check: each nested clause has an explicit context and a stated existence commitment.

### Step 7: Serialize in CGIF when interchange is needed

Preferred extended CGIF style for readability:

```text
[Go *x]
(Agnt ?x [Person: John])
(Dest ?x [City: Boston])
(Inst ?x [Bus])
```

Coreference-heavy style for direct logic mapping:

```text
[Go *x] [Person: John *y] [City: Boston *z] [Bus *w]
(Agnt ?x ?y) (Dest ?x ?z) (Inst ?x ?w)
```

Boolean/context style:

```text
[If
  (On [Cat *x] [Mat])
  [Then (Attr ?x [Happy])]
]
```

Conformance checks:

- Concepts use brackets; relations use parentheses.
- Defining labels use `*`; bound labels use `?`.
- Bound labels occur within scope of a matching defining label.
- Constants/names/literals are not confused with labels.
- Comments do not carry semantics.
- Node order in the same context is not semantically significant.
- Extended features are either accepted by the target or expanded to core CGIF/Common Logic.

Completion check: the CGIF can be read without relying on diagram layout or unstated arc order.

### Step 8: Map to logic when reasoning is needed

Mapping heuristics:

- Concept with blank referent becomes an existentially quantified typed variable.
- Name in a referent becomes a naming/designation constraint or a constant, depending on target notation.
- Relation node becomes a predicate over ordered arguments.
- Concepts in the same context are conjoined.
- `~[CG]` becomes negation.
- `[If A [Then B]]` becomes implication or nested negation expansion.
- `@every` becomes universal quantification or its core expansion.
- Proposition/Situation contexts may require IKL-like or metalevel treatment beyond core ISO CGIF.

Example shape:

```text
CGIF:
[Go *x] (Agnt ?x [Person: John]) (Dest ?x [City: Boston])

Predicate-calculus shape:
exists x:Go, y:Person, z:City.
  Name(y, John) and Name(z, Boston) and Agnt(x,y) and Dest(x,z)
```

Completion check: state whether the mapping is truth-condition preserving, syntax preserving, or only an approximate modeling aid.

### Step 9: Use canonical graph operations for comparison or repair

Classify the intended operation:

Equivalence-preserving:

- Copy: duplicate a subgraph without changing truth conditions.
- Simplify: remove a redundant copied subgraph.
- Double-negation/scoping equivalence: replace double negation with an equivalent scoping context when valid.

Specialization:

- Restrict by type: replace a concept or relation type with a subtype.
- Restrict by referent: replace a blank existential referent with a more specific referent.
- Join: merge two concepts with identical type and referent, combining arcs and coreference sets.

Generalization:

- Unrestrict by type: replace a type with a supertype.
- Unrestrict by referent: erase a specific existential referent to blank.
- Detach: split a concept into two copies and move one or more arcs to the copy.

Context rule:

- In a positive context, specialization makes stronger claims and generalization makes weaker claims.
- In a negative context, the inferential direction reverses.
- Equivalence rules remain equivalence rules in any context.

Completion check: label the result as equivalent, more specialized, or more generalized, and explain the implication direction.

### Step 10: Run the modeling audit

Use this checklist before finalizing:

- Bipartite graph: no concept-to-concept or relation-to-relation arcs disguised as relations.
- Types: every concept has a type, explicit or default `Entity`.
- Referents: blank/name/literal/marker/indexical/descriptor choices are intentional.
- Identity: every join/coreference has evidence.
- Relations: each relation has valence, signature, and stable argument order.
- Quantifiers: existential defaults, universals, counts, collections, and "certain" readings are explicit.
- Contexts: belief/desire/quotation/condition/negation boundaries are correct.
- Logic target: target notation can express the selected feature set.
- Interchange: CGIF labels, syntax, and scopes are valid for the target parser.
- Translation loss: formatting, node order, comments, and stylistic choices are not treated as semantics.
- Standards boundary: ISO/Common Logic features are separated from research extensions.

Output format for audits:

```text
Finding: <short defect>
Location: <graph fragment or label>
Why it matters: <semantic consequence>
Repair: <specific graph or CGIF change>
Status after repair: equivalent | specialization | generalization | changed commitment
```

## B - Boundaries

Do not over-apply this skill:

- If the user only needs a diagram, use a diagramming approach.
- If the user only needs a property graph schema or Cypher query, use graph database patterns unless formal semantics are requested.
- If the user asks about RDF/OWL, treat CGIF/Common Logic as a possible semantic mapping layer, not a replacement for RDF tooling.
- If the user needs current ISO licensing, legal, or procurement details, do current-source lookup rather than relying on the local source snapshot.
- If the model uses generalized quantifiers, indexicals, modalities, natural-language pragmatics, or rich Proposition/Situation contexts, explicitly mark which parts are beyond core ISO CGIF/Common Logic.
- If a translation must be byte-for-byte reversible, do not promise it. Sowa's materials emphasize logical equivalence, not preservation of all syntax, order, layout, or comments.

## Quick Templates

### Requirement to CG

```text
Input clause:
<sentence>

Concepts:
- [Type: referent] because ...

Relations:
- (Relation arg1 arg2) with signature (...)

Contexts:
- <outer/inner> because ...

CGIF:
<serialized graph>

Logic mapping:
<optional>

Audit notes:
<scope/coreference/type/valence concerns>
```

### Graph Comparison

```text
Graph A:
...

Graph B:
...

Operation path:
1. ...
2. ...

Classification:
equivalent | A specializes B | A generalizes B | changed commitment | incomparable

Reason:
...
```

### CGIF Audit

```text
Syntax:
- brackets/parentheses:
- labels:
- names/literals:

Semantics:
- concepts:
- relation signatures:
- quantifier scope:
- context boundaries:
- identity/coreference:

Repairs:
1. ...
```
