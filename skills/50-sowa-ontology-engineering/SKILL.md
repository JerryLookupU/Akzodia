---
name: 50-sowa-ontology-engineering
description: Use when designing, auditing, or repairing an ontology, semantic schema, metadata vocabulary, agent/task model, process model, lexicon, taxonomy, role relation model, or interoperability mapping where category commitments, word senses, signs, agents, purposes, processes, causality, or top-level distinctions are causing ambiguity or brittle reasoning.
---

# Sowa Ontology Engineering

## When To Use

Use this skill when a modeling task needs ontological discipline rather than another naming pass:

- A schema mixes objects, processes, roles, signs, metadata, and word senses without clear distinctions.
- A taxonomy has invalid `is-a` links, singleton subclasses, overloaded labels, or categories that confuse language with world entities.
- A process, workflow, event model, causal graph, or agent system needs explicit states, events, preconditions, postconditions, participants, goals, responsibilities, or failure conditions.
- A lexicon, controlled vocabulary, ontology, metadata standard, catalog, registry, or semantic layer must support translation across languages, teams, domains, tools, or databases.
- An agent model needs to separate animate/software agents, capabilities, purposes, intentions, plans, competence levels, roles, and causality.
- A metadata proposal assumes that tagging strings is enough to create meaning.

Do not use it for a generic explanation of ontology, RDF, Peirce, Whitehead, or Sowa. Use it to produce or review concrete modeling artifacts.

## Source Grounding

### R - Reading

Sowa's ontology notes are used here as an engineering method, not as a fixed grand ontology. The key source commitments are:

- Ontology is an inventory of categories for a language and purpose, not an uninterpreted symbol list.
- Top-level categories are generated from primitive distinctions such as independent/relative/mediating, physical/abstract, and continuant/occurrent.
- A lexicon bridges language and domain knowledge; word senses must carry enough hooks to build semantic representations.
- A sign relates a representing entity, a represented entity, and an interpreting agent.
- An agent does something on purpose; the definition is necessarily tied to capability, process, causality, and intention.
- Processes require distinctions among continuous/discrete change, states/events, participants, preconditions, postconditions, and histories.
- Models are purpose-bound approximations; systematic openness is a feature, not a flaw.

### I - Interpretation

Treat ontology engineering as a staged audit of modeling commitments:

1. First decide what kind of entity each modeled thing is.
2. Then decide how language labels attach to those entities.
3. Then decide which agents use the signs, for what purpose, and under which context.
4. Then decide whether dynamic behavior is being modeled as process, event, state, script, history, situation, activity, or purpose.
5. Finally check whether the model is useful for its target reasoning task without pretending to be complete.

## Workflow

### 1. Frame The Ontology As Language For A Purpose

Before adding classes or properties, write the modeling contract:

- `language`: the vocabulary, schema, DSL, API, ontology, metadata format, or controlled terminology being designed.
- `purpose`: the decisions, queries, translations, explanations, validations, or agent actions the model must support.
- `agents`: the humans, software agents, tools, organizations, or external systems that interpret or act on the signs.
- `world slice`: the physical, social, informational, process, or abstract domain being represented.
- `acceptable approximation`: the level of granularity, uncertainty, and incompleteness that is good enough.

If the purpose is unclear, stop modeling categories and ask for competency questions. A category without a supported question is probably decorative.

### 2. Run The Top-Level Category Pass

Classify each important candidate term with Sowa's top-level distinctions. Use this table as an audit surface:

| Question | Modeling Choice | Typical Engineering Signal |
| --- | --- | --- |
| Can it stand on its own, must it relate to another thing, or does it mediate others? | `Independent`, `Relative`, `Mediating` | Entity vs role/relation vs contract/situation/purpose |
| Is it located in space-time or is it pure information? | `Physical`, `Abstract` | Runtime artifact/object vs schema/script/proposition |
| Does it retain identity through time or unfold in time? | `Continuant`, `Occurrent` | Object/stateful resource vs process/event/history |

Use the twelve central categories as sanity checks:

- `Object`: independent physical continuant, such as a device, file instance, person, account, model run, or runtime resource.
- `Process`: independent physical occurrent, such as an execution, shipment, conversation, biological change, or service run.
- `Schema`: independent abstract continuant, such as a class definition, JSON schema, ontology module, grammar, or form.
- `Script`: independent abstract occurrent, such as a workflow definition, recipe, plan, protocol, program, or process template.
- `Juncture`: relative physical continuant, such as an enduring adjacency, attachment, membership, or physical dependency.
- `Participation`: relative physical occurrent, such as a participant's involvement in a process stage.
- `Description`: relative abstract continuant, such as a claim that characterizes an object or standing configuration.
- `History`: relative abstract occurrent, such as a trace, scenario, log, forecast, or narrative of a process.
- `Structure`: mediating physical continuant, such as an assembly, organization, network, or composed system.
- `Situation`: mediating physical occurrent, such as a meeting, transaction, accident, incident, or interaction among participants.
- `Reason`: mediating abstract continuant, such as an explanation, rationale, rule, invariant, or design intent.
- `Purpose`: mediating abstract occurrent, such as an intended outcome, goal episode, desired situation, or plan target.

Audit rules:

- A subtype must inherit real constraints from its parent. If not, make it a property, role, tag, or example.
- Do not model a role as an object just because it is expressed by a noun.
- Do not model a process as an object merely because the database stores a row for it.
- Do not confuse a `Script` with a `Process`: the workflow definition is abstract; a workflow run is occurrent.
- Do not confuse a `History` with a `Process`: a log or scenario describes an occurrent; it is not the occurrent.
- Keep the system open. Record unresolved primitive assumptions instead of forcing closed-form definitions.

### 3. Build The Lexicon Bridge

For each label that users or systems will exchange, create a lexical entry that connects word form, syntax, sense, concept, and context.

Recommended entry:

| Field | Meaning |
| --- | --- |
| `term` | The surface label, API field, UI label, table name, event name, or domain word. |
| `partOfSpeechOrForm` | Noun, verb, adjective, adverb, relation name, event name, class name, slot name, code enum, etc. |
| `sense` | The intended word sense, not just the spelling. |
| `conceptType` | The ontology class or relation the sense maps to. |
| `topLevelCategory` | Object, Process, Role, Participation, Purpose, History, Schema, etc. |
| `grammarHooks` | Argument structure, case frame, allowed modifiers, cardinality, tense/aspect, or slot syntax. |
| `semanticHooks` | Required relations, constraints, preconditions, postconditions, identity conditions, units, or value types. |
| `pragmaticHooks` | Speaker/user, domain, jurisdiction, task, purpose, authority, confidence, and intended interpretation. |
| `contextDependencies` | Background facts required for correct interpretation. |
| `synonymsAndNearMisses` | Terms to merge, distinguish, or translate with caveats. |

Lexicon checks:

- If two teams use the same term, test whether they share the same concept, only the same word, or only a family resemblance.
- If two terms translate to the same target label, check whether information is being lost.
- If a word sense requires context, represent the context instead of pretending the term is self-contained.
- If an entry uses only monadic features, check whether relations are being hidden in prose.
- If an application needs inference, the lexical entry must link to logical or structured semantic hooks, not just a dictionary gloss.

### 4. Separate Signs, Objects, Concepts, And Metadata

Use the semiotic triangle whenever metadata or interoperability is involved:

- `sign`: the string, URI, field name, icon, tag, code, document, record, or symbol.
- `object`: the thing, process, state, value, person, organization, event, or abstraction being represented.
- `interpretant/concept`: the meaning constructed by an agent when interpreting the sign.
- `agent`: the human, software agent, organization, model, or system interpreting the sign.
- `ground`: the respect, context, convention, measurement, task, or purpose under which the sign stands for the object.

Metadata audit:

1. Pick one important metadata field.
2. Ask what sign it stores.
3. Ask what object it is supposed to represent.
4. Ask which agent interprets it.
5. Ask under what convention or purpose it is valid.
6. Ask which translations, units, identifiers, authority files, or context rules preserve meaning.

Reject metadata that only tags signs with more signs. Meaning must connect to world entities, abstract entities, agent purposes, and conventions.

### 5. Model Roles And Relations With `Has`

When natural language gives you role nouns such as `owner`, `driver`, `mother`, `author`, `customer`, `reviewer`, or `agent`, do not immediately turn each into a dyadic predicate. Model the role type and the relation that connects a prehending entity to a prehended entity.

Role audit:

- Identify the independent entity being viewed by itself.
- Identify the role it plays relative to another entity or process.
- Identify whether the relation is intrinsic or extrinsic.
- For continuants, distinguish pieces, attributes, and enduring correlatives.
- For occurrents, distinguish participants, stages, and manners.
- Define relation signatures: `HasRole(domain, range)`, with domain and range constraints.
- Add inverse or converse relations only when they preserve meaning and help the task.

Use the role hierarchy to avoid false precision:

- If evidence only says someone is involved in a process, use `Participant`.
- If evidence says the participant is present throughout but not controlling, use `Immanent`.
- If evidence says the participant determines direction from the start, use `Initiator`.
- If evidence says voluntary animate initiation, specialize to `Agent`.
- If evidence says involuntary initiation, specialize to `Effector`.
- If evidence says the participant enables the action without initiating it, specialize to `Instrument` or `Resource`.

### 6. Model Processes, Agents, And Causality Together

A process model is incomplete if it only lists steps. Audit it as a causal structure:

| Surface Question | Ontological Check |
| --- | --- |
| What changes? | State variables, continuants affected, and event types. |
| What persists? | States, identity conditions, resources, and participants. |
| What starts or stops? | Initiations, cessations, continuations, completions. |
| Who or what acts? | Agent, effector, instrument, resource, patient, recipient, goal. |
| Why does it happen? | Purpose, reason, intention, script, policy, or external cause. |
| What must be true before? | Preconditions and input states. |
| What becomes true after? | Postconditions and output states. |
| What can surprise the model? | Exogenous events, branching, concurrency, delayed effects, memory, abnormal flows. |

Classify process complexity:

- discrete or continuous
- linear or branching
- independent or ramified
- immediate or delayed
- sequential or concurrent
- predictable or surprising
- normal or equinormal
- flat, hierarchical, or recursively hierarchical
- timeless or time-bound
- forgetful or memory-bound

For causal modeling:

- Represent discrete processes as state/event graphs when possible.
- Keep states and events distinct unless the target notation has a deliberate reason to merge them.
- Treat causal links as claims of influence, not proof of ultimate causation.
- Model event signatures: precondition state types and postcondition state types.
- Embed discrete models in continuous reality only to the precision required by the task.
- Prefer useful approximations over universal theories.

### 7. Audit Agentive Behavior

Use this pass for human, robot, softbot, autonomous workflow, or LLM-agent models.

An agentive entity must be checked against:

- `capability`: can it perform the action, not merely be named as actor?
- `purpose`: what intended situation or preferred state guides the action?
- `perception`: what signs or inputs can it interpret?
- `desire/preference`: what states does it prefer or avoid?
- `locomotion/action`: how can it affect the environment or host system?
- `imagery/memory`: what internal representations can it retain or manipulate?
- `thought/planning`: can it reason, plan, evaluate, or revise behavior?
- `responsibility`: can success, failure, praise, blame, obligation, or accountability attach to it?

Do not overclaim agency. A scheduler, script, or model call may be a process or instrument rather than an agent if it lacks autonomy, goals, or interpretation.

### 8. Validate With Competency Questions And Counterexamples

Run these checks before accepting the model:

- Can it answer the competency questions without hidden prose assumptions?
- Can it distinguish object, role, sign, and word sense for the same label?
- Can it distinguish workflow definition, workflow run, log, purpose, and explanation?
- Can it represent both normal and surprising process paths?
- Can it say what information would justify specializing a role?
- Can it translate across vocabularies without losing the agent, purpose, unit, or context?
- Can it explain why a category exists and what would break if it were removed?
- Does it record which primitives remain open rather than pretending to define everything?

Recommended output:

| Artifact | Required Content |
| --- | --- |
| Top-level category table | Term, category, primitive distinctions, identity criteria, reason. |
| Lexicon table | Term, sense, concept, grammar hooks, semantic hooks, pragmatic hooks. |
| Semiotic metadata map | Sign, object, interpretant, agent, ground, translation rules. |
| Process/causal graph | States, events, preconditions, postconditions, participants, causal influences. |
| Role matrix | Participants by initiator/resource/goal/essence and determinant/immanent/source/product. |
| Open-system notes | Purpose limits, approximation level, unresolved primitives, future distinctions. |

## Failure Modes

- Treating ontology as a list of fashionable class names.
- Assuming metadata creates meaning because every field has a tag.
- Confusing a word with a concept, a concept with an object, or a record with the thing recorded.
- Using `is-a` where the relation is role, part, attribute, stage, participant, sign, representation, or purpose.
- Modeling agent as any component that appears in subject position.
- Ignoring purpose and context in lexicon entries.
- Flattening processes into CRUD status enums without states, events, preconditions, postconditions, and causal links.
- Choosing a single universal causal theory when the engineering task only needs a purpose-bound approximation.
- Closing definitions for primitive categories that should be constrained by axioms and examples.

## Boundaries

This skill produces engineering artifacts for ontology and semantic-model review. It is not a full tutorial on conceptual graphs, Peirce, Whitehead, RDF, OWL, PSL, Petri nets, or formal logic.

Use a formal reasoner, theorem prover, ontology editor, or domain standard when the model must support machine-checked consistency, regulatory exchange, scientific simulation, or production semantic-web interoperability.

Use simpler taxonomy or schema design when there are no contested categories, no process/agent/role ambiguity, and no cross-vocabulary translation problem.

### A1 - Past Application

Sowa uses the framework to reinterpret many modeling cases: top-level KR categories, lexicon entries, role relations, thematic roles, process classifications, metadata vocabularies, RDF-style signs, Petri nets, Pearl causal structures, and engineering approximations to continuous reality.

### A2 - Future Trigger

Invoke this skill when a user asks to design or audit ontology categories, lexicons, semantic metadata, process models, causal graphs, role relations, thematic roles, agent capability models, controlled vocabularies, schema interoperability, or LLM/agent task vocabularies where meaning depends on context, purpose, and interpretation.

### E - Execution Summary

1. Frame language, purpose, agents, world slice, and approximation.
2. Classify core terms by top-level category and reject invalid `is-a` links.
3. Build lexicon entries that bridge word senses to concepts and context.
4. Map signs, objects, interpretants, agents, and grounds for metadata.
5. Model roles, participants, processes, states, events, and causal influence.
6. Validate with competency questions, ambiguity cases, and open-system notes.

### B - Boundaries

Use the method for modeling commitments and review. Do not use it to summarize Sowa's website, to role-play Sowa, or to force a complete axiomatization where the right engineering move is an explicit approximation.

## Related Skills

- `07-ontological-engineering`: broader task/capability ontology construction.
- `44-knowledge-engineering`: knowledge task, agent, and communication modeling.
- `08-knowledge-representation-and-reasoning`: formal KR notation and reasoning choices.
