---
name: 49-sowa-knowledge-representation
description: Use when designing, choosing, auditing, or explaining a knowledge representation for an agent, ontology, rules system, knowledge graph, semantic index, decision workflow, context-aware memory, or interoperable knowledge base. Triggers on requests involving logic/ontology/computation tradeoffs, KR notation choice, defaults and exceptions, process/change representation, semantic interoperability, or auditable reasoning traces.
---

# Sowa Knowledge Representation

## When To Use

Use this skill when the work depends on how knowledge is made explicit, computable, shareable, and explainable. Typical triggers:

- You need to choose between rules, frames, semantic networks, conceptual graphs, predicate logic, KIF, SQL, object models, Petri nets, ontologies, controlled language, or hybrid retrieval/KR designs.
- A system must explain why a conclusion follows, why a term means what it means, why a default was withdrawn, or why a conflicting source was rejected.
- Domain knowledge is currently trapped in prompts, comments, manuals, schemas, vector chunks, expert habits, or code branches and must become auditable structure.
- The design involves contexts, purposes, agents, modal/intentional claims, user-specific assumptions, temporal change, actions, events, processes, or state histories.
- You need semantic interoperability across schemas, ontologies, APIs, databases, agents, documents, languages, or knowledge representations.
- You are building an index-based knowledge engineering system where terms, concepts, sources, examples, evidence, rules, and explanations must stay linked.

Do not use this skill for a plain book summary, generic ontology naming, simple CRUD schema design, or a task where no explicit inference, semantic alignment, context scoping, or explanation is needed.

## R - Source Reading

This skill is distilled from the local Sowa source set under `site-sowa/books/knowledge-representation/` and `site-sowa/krbook/`. The available source is companion material: book landing page, preface, table of contents, index, and errata, not a full chapter-by-chapter text dump.

Core source claims:

- "Logic provides the formal structure and rules of inference."
- "Ontology defines the kinds of things that exist in the application domain."
- "Computation supports the applications that distinguish knowledge representation from pure philosophy."
- Sowa frames KR as "the application of logic and ontology to the task of constructing computable models for some domain."
- The book organization expands that triad through logic, ontology, representations, processes, purposes/contexts/agents, knowledge soup, acquisition, sharing, notation summaries, ontology bases, and extended examples.

Treat these claims as design constraints: a useful KR design must have inferential form, ontological content, and computable execution.

## I - Interpretation

Sowa's practical method is not "pick a formalism first." It is a three-way fit problem:

- Logic asks: what inferences, contradictions, defaults, quantifiers, contexts, and proofs must the system support?
- Ontology asks: what kinds of things, roles, relations, processes, times, purposes, agents, and abstractions exist in the domain?
- Computation asks: what representation can actually be stored, queried, transformed, maintained, indexed, exchanged, and explained in the target system?

The discipline is therefore representation engineering. Start from the knowledge task and its explanation obligations, then choose the lightest notation or hybrid that preserves the semantics that matter. A good design can survive elaboration: adding a new exception, context, source, schema, term, agent, or process should require a localized change, not a rewrite.

## A1 - Past Application Patterns From The Book

Use these patterns as evidence-backed examples, not as mandatory technologies:

- Logic and notation comparison: predicate calculus, conceptual graphs, and KIF are treated as semantically related ways to express logical structure.
- Structural KR: frames, rules, data, object-oriented systems, and natural language semantics are compared as ways to embody logic and ontology in computable languages.
- Dynamic KR: times, events, situations, procedures, concurrent processes, computation, constraint satisfaction, and change require process-aware representation rather than static taxonomies alone.
- Purpose and context: contexts, modal reasoning, intentional reasoning, encapsulated objects, and agents show that meaning depends on situation, goal, and point of view.
- Knowledge soup: vagueness, uncertainty, randomness, ignorance, fuzzy logic, nonmonotonic logic, theories, models, world, and semiotics show where pure monotonic logic is too brittle.
- Sharing and acquisition: ontology sharing, conceptual schemas, multiple paradigms, representation mapping, language patterns, and acquisition tools are treated as central engineering problems.
- Extended examples include hotel reservation, library database, and Attempto Controlled English to logic translation, which are all domain-to-computable-form exercises.

## A2 - Future Trigger

Invoke this skill when a user asks any of the following kinds of question:

- "What representation should we use for this knowledge base?"
- "Should this be a graph, ontology, rules engine, SQL schema, vector index, controlled language, or logic layer?"
- "How do we make an agent's knowledge auditable and explainable?"
- "How do we handle contexts, defaults, exceptions, uncertainty, or conflicting domain rules?"
- "How do we align several schemas, ontologies, APIs, documents, or agent memories?"
- "How do we turn a domain book/manual/policy into executable knowledge without flattening it into a prompt?"

## E - Execution

### 1. State The Knowledge Job

Write a compact KR brief before choosing any technology:

```text
goal:
users/agents:
domain scope:
questions to answer:
actions to support:
facts to store:
rules or constraints:
contexts:
expected explanations:
update/change pattern:
interoperability targets:
risk if wrong:
```

If the brief contains no inference, context, ontology, or explanation requirement, use ordinary software design instead of KR.

### 2. Build The Sowa Triad

Create a three-column design table:

| Dimension | Required Decisions | Evidence To Collect |
|---|---|---|
| Logic | Inference type, contradiction handling, proof/explanation shape, monotonic vs nonmonotonic behavior, open/closed world assumption | Example questions, rules, exceptions, false positives, conflict cases |
| Ontology | Entity kinds, relations, roles, processes, events, contexts, purposes, agents, measures, time, part-whole structures | Domain terms, schemas, forms, workflows, examples, source passages |
| Computation | Storage, query, update, indexing, translation, runtime cost, tooling, versioning, interoperability | Existing systems, APIs, DBs, graph stores, rule engines, vector stores, logs |

Reject any design that fills only one or two columns. Logic without ontology becomes empty form. Ontology without logic becomes vocabulary. Logic and ontology without computation become philosophy rather than an executable system.

### 3. Choose Representation By Reasoning Need

Use the smallest representation that preserves the required semantics:

| Need | Prefer | Avoid |
|---|---|---|
| Classification, inheritance, type constraints, term alignment | Taxonomy, ontology, description logic, frame-like schema | Flat keyword tags with no relations or constraints |
| Auditable rules, contradictions, proofs, eligibility, compliance | Predicate logic, conceptual graphs, KIF-like interchange, rules with provenance | Unstructured prompt rules or opaque classifier outputs |
| Defaults, exceptions, absence of evidence | Default logic, nonmonotonic rules, explicit open/closed/semi-open world policy | Treating missing data as false everywhere |
| Processes, actions, events, concurrency, state histories | Situation calculus, temporal logic, Petri nets, state-transition models, event schemas | Static entity ontology alone |
| Natural language semantics and controlled input | Lexicon, thematic roles, controlled natural language, semantic parsing to logic | Free text chunks with no concept/role mapping |
| Context, purpose, agents, beliefs, permissions, scopes | Context-labeled assertions, modal/intentional logic fragments, agent models | Global facts that silently apply to every user/time/source |
| Knowledge sharing and interoperability | Conceptual schema, ontology mapping, metamodels, translation rules, index crosswalks | One-off adapters with undocumented semantic losses |
| Vague or statistical reality | Fuzzy logic, probabilistic/statistical layer, calibrated ML plus symbolic boundaries | Forcing crisp Boolean rules where uncertainty is continuous |
| Retrieval-heavy knowledge work | Semantic index plus concept IDs, source provenance, admissibility rules, explanation templates | Vector search as the only representation |

When two needs are both central, design a hybrid deliberately. Example: a semantic index can retrieve source passages, an ontology can normalize terms, and a rule layer can produce auditable conclusions.

### 4. Model Ontology Before Rules

For each high-value domain term, record:

```text
term:
concept id:
definition:
kind/category:
relations:
roles:
attributes/measures:
allowed values:
contexts where valid:
source/provenance:
examples:
counterexamples:
owner:
change policy:
```

Check for common ontology failures:

- A term is lexical only: the word exists, but the underlying concept is unclear.
- A relation hides an event or process that needs time, participants, and effects.
- A class is really a role played in a situation.
- A property should be a measured value with unit, granularity, timestamp, and method.
- A domain distinction is encoded only in UI labels or code comments.

### 5. Make Context And Purpose First-Class

For every assertion or rule that can vary, attach a context label:

```text
assertion:
valid_for_user/org:
valid_for_time:
valid_for_source:
valid_for_task:
valid_for_jurisdiction/environment:
purpose:
agent_authority:
promotion_rule_to_global_truth:
```

Use context labels when claims differ by user, tenant, source, workflow stage, jurisdiction, experimental condition, agent belief, or time. Do not promote local working assumptions into global knowledge unless a promotion rule and reviewer/agent authority are explicit.

### 6. Handle Knowledge Soup Explicitly

Before implementing inference, classify uncertain material:

- Vague: boundaries are gradual or open-textured.
- Uncertain: the system lacks enough evidence.
- Random: outcomes have irreducible variability.
- Ignorant: the representation has no modeled concept or source yet.
- Inconsistent: sources or rules conflict.
- Defaulted: a conclusion is normally true but retractable.

Choose one policy per class:

```text
class:
representation:
admission criteria:
revision rule:
explanation wording:
escalation trigger:
test case:
```

Do not hide these under a single confidence score. Confidence, default status, context, provenance, and conflict status answer different questions.

### 7. Build An Index-Based Knowledge Engineering Layer

For practical agent systems, maintain indexes that connect text, concepts, rules, examples, and explanations:

| Index | Purpose |
|---|---|
| term index | Map words, aliases, acronyms, and source phrases to concept IDs |
| concept index | List definitions, categories, relations, owners, and source anchors |
| rule index | Store rules, defaults, blockers, priorities, provenance, and tests |
| context index | Track user, source, time, environment, authority, and validity scopes |
| process index | Link events, actions, preconditions, effects, histories, and invariants |
| evidence index | Connect claims to source passages, examples, counterexamples, and confidence |
| translation index | Record schema/ontology/notation mappings and known semantic losses |
| explanation index | Reusable templates for why, why-not, conflict, uncertainty, and revision answers |

This makes the knowledge base inspectable. A user should be able to ask "where did this concept come from?", "which rule used it?", "what changed?", and "what would make this conclusion false?"

### 8. Produce Auditable Explanations

Every important answer or action should expose:

```text
answer:
active context:
recognized concepts:
source facts:
rules/defaults applied:
inference type:
blocked alternatives:
conflicts:
unknowns:
confidence or uncertainty policy:
representation used:
provenance:
revision conditions:
```

For "why not" explanations, include the missing precondition, violated constraint, blocked default, unavailable context, or conflicting higher-priority source. For "what changed" explanations, include old support, new support, retracted conclusions, and affected downstream decisions.

### 9. Validate By Elaboration Tolerance

Run the representation through perturbation tests:

- Add a new exception to a default rule.
- Add a second source with a conflicting definition.
- Change context from one user, tenant, time, or jurisdiction to another.
- Add a new event type or process state.
- Translate the same domain fact into a different schema or notation.
- Ask for a why, why-not, and what-if explanation.
- Remove a source passage and check whether unsupported conclusions disappear.
- Introduce a vague term and require an uncertainty policy.

The design passes when the fix is localized to concepts, rules, contexts, mappings, or tests. It fails when small changes require rewriting prompts, code branches, indexes, and explanations together.

## B - Boundaries

- Do not overformalize low-risk, one-off, or purely operational tasks. A checklist or typed schema may be enough.
- Do not use ontology work as a substitute for domain validation. Subject matter experts still own high-impact legal, medical, financial, safety, or security rules.
- Do not pretend symbolic KR replaces retrieval or machine learning. Use KR to structure, constrain, revise, and explain; use retrieval for source access and ML for perception, ranking, language variation, and empirical prediction.
- Do not force one notation to carry every need. Sowa's source material repeatedly compares representations; hybrid designs are acceptable when translation and semantic loss are documented.
- Do not treat the source set as full book text. This skill is distilled from companion pages, preface, table of contents, index, and errata available in the local repository.

## Failure Modes

- Prompt-only knowledge: rules and concepts are embedded in instructions but cannot be queried, revised, tested, or cited.
- Vocabulary theater: a taxonomy exists, but no inference or explanation depends on it.
- Logic theater: formal notation exists, but the domain ontology is vague or not maintained.
- Vector-only knowledge: retrieval returns chunks, but no concept IDs, context labels, rule dependencies, or revision policy exist.
- Global truth leakage: local assumptions from one source, user, task, or time become universal facts.
- Closed-world abuse: missing information is treated as false outside a bounded and verified dataset.
- Default pileup: defaults have no blockers, priority, support tracking, or retraction history.
- Static ontology for dynamic work: processes, actions, histories, and effects are squeezed into timeless entity classes.
- Unexplained interoperability: mappings between schemas or representations omit semantic losses and conflict policy.

## Related Skills

- `07-ontological-engineering` for detailed ontology construction.
- `08-knowledge-representation-and-reasoning` for orchestration-focused KR/R reasoning.
- `44-knowledge-engineering` for broader CommonKADS-style knowledge modeling.
- `47-retrieval-augmented-generation` when the KR layer depends on source-grounded retrieval.
