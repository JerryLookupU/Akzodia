# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
: Ontological Engineering

## Entry Metadata

- Entry: `07 本体工程 / Ontological Engineering`
- Skill: `07-ontological-engineering`
- Source title: `Ontology Development 101: A Guide to Creating Your First Ontology`
- Authors: Natalya F. Noy and Deborah L. McGuinness
- Institution: Stanford University
- Supplemented metadata: publication/report year `2001`; report identifiers `KSL-01-05` and `SMI-2001-0880`

## Core Ideas From The Source

The source frames an ontology as an explicit formal description of domain concepts, their properties, and restrictions. In practical terms, ontology work defines classes, arranges them in a taxonomic hierarchy, defines slots/properties with allowed values, and creates instances.

Reasons to build an ontology:

- Share a common understanding of information structure across people and software agents.
- Reuse domain knowledge instead of rebuilding each application's vocabulary.
- Make domain assumptions explicit and easier to change.
- Separate domain knowledge from operational knowledge.
- Analyze and validate domain knowledge once it is declarative.

The recommended process is iterative:

1. Determine domain and scope.
2. Consider reuse of existing ontologies.
3. Enumerate important terms.
4. Define classes and hierarchy.
5. Define class properties/slots.
6. Define slot facets such as type, range, and cardinality.
7. Create instances.

Important modeling heuristics:

- There is no single correct ontology; the intended application and future extensions drive modeling choices.
- Classes should reflect domain objects and relationships, not code structure or method placement.
- A subclass must be a real "kind of" its superclass.
- Siblings should be at the same generality level.
- Synonyms name the same concept; they should not become separate classes.
- Introduce a class when it adds properties, restrictions, relationships, routing meaning, or an important expert distinction.
- Use slot values for distinctions that do not change behavior or relationships.
- Individual instances are the most specific items the knowledge base needs to represent.
- Limit scope to what the application needs, with only modest extra generality for maintainability.

## Translation For Auto-Orchestrator Design

For auto-orchestrators, the ontology is the declarative model that lets planners, routers, evaluators, and policy gates share a vocabulary.

Useful class candidates:

- `Task`, `TaskFamily`, `Capability`, `Agent`, `Tool`, `Artifact`, `KnowledgeSource`, `Policy`, `Constraint`, `ExecutionState`, `FailureMode`, `EvaluationCriterion`.

Useful slot candidates:

- `requiresInput`, `producesArtifact`, `canHandle`, `handledBy`, `allowedTools`, `blockedByPolicy`, `requiresApproval`, `hasRiskLevel`, `dependsOn`, `hasFallback`, `hasOwner`, `hasProvenance`.

Useful facets:

- Cardinality: exactly one owner, one or more required inputs, zero or more fallbacks.
- Value type: string, enum, number, boolean, instance reference.
- Range: `canHandle` should point to valid task classes; `producesArtifact` should point to artifact classes; `blockedByPolicy` should point to policy classes.
- Defaults: convenient initial values that can be overridden, not immutable constraints.

Competency questions for an orchestrator ontology:

- Which task class does this user request instantiate?
- Which agents or tools can handle that class?
- What input artifacts are required before dispatch?
- Which policies apply before execution?
- What output contract must be produced?
- What fallback is valid when the preferred capability is unavailable?
- Which distinctions matter for routing, and which should remain ordinary property values?

Validation checks:

- Can each competency question be answered using explicit model elements?
- Are task subclasses true kinds of their parents?
- Are capability names and task names deduplicated across synonyms?
- Are domains and ranges neither too broad nor too narrow?
- Are volatile states modeled as values rather than permanent classes?
- Are intentional omissions documented for future reuse?

## Distillation Notes

This skill emphasizes the source's executable modeling method, not Protege UI mechanics. The wine ontology examples were translated into orchestrator concepts: wine classes become task/capability classes; slots become routing-relevant properties; facets become dispatch constraints; instances become concrete tools, agents, policies, or task traces.

The source's warning that ontology design depends on intended use is critical for auto-orchestrators. A taxonomy optimized for evaluation reporting may differ from one optimized for live routing, even in the same product. The skill therefore starts with competency questions and validates the model against them.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Ontology Development 101 and local ontology-engineering notes. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Competency questions -> classes -> slots -> facets -> instances -> validation. Intended use chooses the ontology.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not confuse ontology with object-oriented implementation, UI labels, or an unrestricted glossary.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: There is no single correct ontology. The right ontology is the one that answers the competency questions and supports reuse, constraints, and inference without hiding procedural logic.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Write competency questions first, enumerate terms, reuse stable vocabularies, separate classes from slots and instances, then test with real examples and counterexamples.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
