---
name: 50-sowa-ontology-engineering
description: Use when designing, auditing, or repairing concrete ontology, semantic schema, metadata vocabulary, agent/task model, process model, lexicon, taxonomy, role model, or interoperability mapping artifacts where category commitments, word senses, signs, agents, purposes, processes, causality, or top-level distinctions are causing ambiguity or brittle reasoning. Do not use for generic summaries of Sowa, Peirce, RDF, OWL, or philosophy unless the user also asks for an executable modeling artifact or audit.
source_files:
  - references/source-notes.md
---
# 50 Ontology Engineering

## Book-Derived Essence

- Core framework: Ontology as categories for a language and purpose; classify objects, processes, roles, purposes, histories, schemas, signs, and causal relations.
- Deep idea: Ontology work is an audit of commitments. A term is not understood until its category, identity condition, role, process participation, and purpose are clear.
- Discovery method: Start from purpose and competency questions, run top-level category tests, separate lexical sense from concept, model roles/processes/causes, and record what each distinction changes.
- Boundary: Do not treat ontology as a fashionable class list; categories must answer questions and prevent ambiguity.
- Source capsule: `references/source-notes.md#BDE-core-framework`

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

This skill is self-contained for execution. Do not require the user or agent to read Sowa's original pages before applying it. Use the audit trail files only for provenance checks or maintenance of this skill, not as runtime prerequisites.

### I - Interpretation

Treat ontology engineering as a staged audit of modeling commitments:

1. First decide what kind of entity each modeled thing is.
2. Then decide how language labels attach to those entities.
3. Then decide which agents use the signs, for what purpose, and under which context.
4. Then decide whether dynamic behavior is being modeled as process, event, state, script, history, situation, activity, or purpose.
5. Finally check whether the model is useful for its target reasoning task without pretending to be complete.

## Execution Gate

Before applying the workflow, establish the minimum modeling contract.

Proceed only when the request includes or permits you to infer:

- `artifact`: the ontology, schema, vocabulary, metadata field set, process model, agent model, taxonomy, mapping, or candidate term list to examine.
- `purpose`: the decision, query, validation, translation, explanation, routing, planning, or agent action the model must support.
- `scope`: the domain slice, system boundary, or process boundary being modeled.

If any required item is missing:

- If the user asks for a full design or high-confidence audit, ask up to three targeted questions and wait.
- If the user asks for a quick pass, proceed with explicit `Assumptions` and mark every inferred purpose, scope, or missing artifact as provisional.
- If there is no concrete artifact or candidate terms and the prompt is only educational or historical, do not run the workflow; answer as a normal explanation instead.

Required runtime behavior:

1. Always start by naming the artifact, purpose, agents/interpreters, world slice, and approximation level.
2. Always produce at least one actionable artifact: a category table, lexicon table, semiotic metadata map, role/process/causal model, or ontology audit.
3. When evidence is insufficient to classify something, record the uncertainty and the next discriminating question instead of inventing a category.
4. Do not force all terms through every pass. Run only the passes relevant to the user's artifact, but explain skipped passes.

## Workflow

### 1. Frame The Ontology As Language For A Purpose

Before adding classes or properties, write the modeling contract:

- `language`: the vocabulary, schema, DSL, API, ontology, metadata format, or controlled terminology being designed.
- `purpose`: the decisions, queries, translations, explanations, validations, or agent actions the model must support.
- `agents`: the humans, software agents, tools, organizations, or external systems that interpret or act on the signs.
- `world slice`: the physical, social, informational, process, or abstract domain being represented.
- `acceptable approximation`: the level of granularity, uncertainty, and incompleteness that is good enough.
- `competency questions`: the questions or checks the model must answer without hidden prose assumptions.

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

Top-level category method:

1. List each candidate term, field, class, relation, event, state, or role.
2. Decide whether it is independent, relative, or mediating.
3. Decide whether it is physical or abstract in the model's purpose-bound sense.
4. Decide whether it is continuant or occurrent.
5. Assign the nearest category and write the identity criterion: what makes one instance the same through time, or what bounds the occurrence.
6. Record modeling consequences: class, relation, role, event, state, tag, value, process run, process definition, log, purpose, or rationale.
7. Flag invalid `is-a` links where the child does not inherit the parent's identity and constraints.

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

Lexicon construction method:

1. Separate the spelling or field name from the intended sense.
2. Map the sense to the ontology concept or relation, not directly to a database column.
3. Add grammar hooks for how the term combines with arguments, modifiers, values, or slots.
4. Add semantic hooks that inference, validation, or translation can use.
5. Add pragmatic hooks for speaker, authority, jurisdiction, task, confidence, and intended user.
6. Add near-miss terms and translations that must remain distinct.
7. Test the entry against at least one ambiguity case: same word/different concept, different word/same concept, or context-dependent interpretation.

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

Sign and metadata method:

1. Treat every field name, enum, URI, icon, label, tag, code, record, and document reference as a possible `sign`.
2. For each sign, identify the represented `object` or abstract entity, the `interpretant/concept`, the interpreting `agent`, and the `ground`.
3. State which convention makes the sign valid: unit, authority file, schema version, legal context, measurement method, workflow state, or task purpose.
4. Define preservation rules for translation: which distinctions, units, identifiers, roles, contexts, or provenance must not be lost.
5. Reject mappings where two signs are declared equivalent but differ in object, interpretant, agent, ground, or purpose.

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

Role modeling method:

1. Start with the independent entity and the process or relation in which it participates.
2. Use `Participant` until evidence justifies a narrower role.
3. Specialize by evidence: initiation, control, enablement, affectedness, reception, source, product, goal, responsibility, or obligation.
4. Record each role as purpose-bound and context-bound; avoid making a permanent class such as `Customer` unless the identity conditions support it.
5. Define relation signatures with domain, range, cardinality, temporal scope, and inverse/converse only when needed by the competency questions.

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

Process and causality method:

1. Separate `Script` from `Process`: definition, plan, workflow, or protocol versus an actual run.
2. Separate `State`, `Event`, `Process`, and `History`: condition, change boundary, unfolding occurrence, and record/trace.
3. For each event type, write precondition state types, postcondition state types, participants, triggering signs, and expected outputs.
4. Represent causal edges as explicit influence claims with scope, confidence, and possible counterexample conditions.
5. Include abnormal paths: exogenous events, concurrency, delayed effects, partial completion, cancellation, retry, memory, and surprise.
6. Keep continuous phenomena continuous unless the purpose justifies discretizing them into events or states.

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

Agent audit method:

1. Separate actor labels from agentive capability.
2. Check whether the entity can interpret signs, select actions, pursue purposes, remember state, plan, and affect the environment.
3. Distinguish `Agent`, `Effector`, `Instrument`, `Resource`, `Patient`, `Recipient`, and `Goal` by evidence, not by grammar.
4. Record responsibility separately from causation: a component may cause an effect without being accountable for it.
5. For software or LLM agents, state whether agency belongs to the model call, runtime wrapper, policy, human operator, organization, or composed system.

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

Ontology audit method:

1. Inventory candidate terms and relations.
2. Classify each by top-level distinctions and identity criteria.
3. Check `is-a`, part/whole, role, participation, sign, representation, state/event, and purpose relations.
4. Test lexicon entries for word-sense ambiguity and missing grammar, semantic, or pragmatic hooks.
5. Test metadata signs for object, interpretant, agent, ground, and translation preservation.
6. Test process/agent models for states, events, participants, capabilities, purposes, preconditions, postconditions, causal claims, and abnormal paths.
7. Validate against competency questions and counterexamples.
8. Emit repairs as concrete edits: split, merge, rename, retype, demote to property/tag, promote to process/event/role, add relation signature, or add missing context.

## Output Format

Use this structure unless the user asks for a narrower artifact:

```markdown
## Modeling Contract
- Artifact:
- Purpose:
- Agents / interpreters:
- World slice:
- Approximation level:
- Competency questions:
- Assumptions:

## Findings
| Severity | Item | Ontological issue | Evidence | Repair |
| --- | --- | --- | --- | --- |

## Top-Level Categories
| Term | Category | Primitive distinctions | Identity / boundary criterion | Modeling consequence |
| --- | --- | --- | --- | --- |

## Lexicon Bridge
| Term | Sense | Concept / relation | Grammar hooks | Semantic hooks | Pragmatic hooks | Near misses |
| --- | --- | --- | --- | --- | --- | --- |

## Semiotic Metadata Map
| Sign | Object | Interpretant / concept | Agent | Ground | Preservation / translation rule |
| --- | --- | --- | --- | --- | --- |

## Role, Process, And Causality Model
| Process / event | States changed | Participants and roles | Preconditions | Postconditions | Causal influence / uncertainty |
| --- | --- | --- | --- | --- | --- |

## Repairs And Open Questions
- Repairs:
- Counterexamples to test:
- Unresolved primitives:
- Skipped passes and reason:
```

If a table is irrelevant, write `N/A` and explain why in one sentence. For lightweight answers, preserve the same section names but shorten rows.

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

## Recovery And Idempotency

- Repeat audits should preserve stable term IDs, category decisions, relation signatures, and explicit assumptions unless new evidence changes them.
- For incremental updates, diff new or changed terms against the last modeling contract before changing existing categories.
- If evidence conflicts, keep both candidate analyses and state the discriminating competency question or empirical check.
- If only partial data is available, produce a partial audit with `coverage`, `assumptions`, and `not reviewed` sections.
- If a formal ontology, database schema, or API already exists, propose edits in small patches rather than replacing the entire model.

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

## Source Closure

This 50-sowa-ontology-engineering skill is self-contained for runtime use; its source basis is John F. Sowa ontology materials: top-level categories, roles, processes, lexicon, signs, causality. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
