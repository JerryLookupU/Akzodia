# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
: Knowledge Engineering

## Manifest Metadata

- Entry id: `44`
- Title: `知识工程 / Knowledge Engineering`
- Skill name: `44-knowledge-engineering`
- Source files:

## Distillation Target

The useful auto-orchestrator move from CommonKADS is not "summarize expert knowledge." It is to model knowledge work before implementation:

1. Decide why the knowledge system should exist in an organizational context.
2. Identify the task, agents, knowledge structures, and communication exchanges.
3. Use reusable task templates where possible.
4. Validate behavior with scenarios and simulations before building large stores or committing to an implementation.
5. Preserve the conceptual structure in architecture.

## Core Concepts Extracted

### Knowledge Is Contextual and Action-Oriented

The book distinguishes data, information, and knowledge pragmatically. Knowledge is information used with purpose and competence to produce action or new information. The exact boundary is context-dependent, so a knowledge model must be scoped by task and domain.

For orchestrators, this means a memory store, RAG index, prompt, or rule base is not automatically "knowledge." It becomes operational knowledge only when tied to a task, roles, reasoning steps, and validation scenarios.

### From Mining to Modeling

CommonKADS rejects the old view of extracting knowledge directly from an expert's head. Knowledge engineering is a constructive modeling activity. A model is a purposeful abstraction of selected aspects of expert work.

For orchestrator design, interview transcripts, policy docs, logs, and examples should be used to construct task, domain, inference, and communication models. They should not be copied into a single undifferentiated prompt or rule file.

### Knowledge-Level Principle

Knowledge should first be modeled at a conceptual level using stakeholder vocabulary, independent of programming constructs. Implementation choices belong to the design phase.

For orchestrators, first name domain concepts, rule types, inferences, task control, agent responsibilities, and transactions. Only after validation choose whether they become tools, prompts, DSL rules, state machines, vector stores, graph stores, typed services, or workflow nodes.

## CommonKADS Model Suite Adapted to Auto-Orchestrators

### Organization Model

Purpose: identify problems, opportunities, feasibility, benefits, costs, and organizational impact.

Auto-orchestrator adaptation:

- What knowledge bottleneck is being automated or augmented?
- What decisions or workflows improve?
- What risks appear if the orchestrator is wrong?
- What approvals, compliance rules, or accountability paths constrain automation?

### Task Model

Purpose: model relevant tasks, inputs, outputs, preconditions, performance criteria, resources, competences, and dependencies.

Auto-orchestrator adaptation:

- Define the selected task before designing agents.
- Include task type and whether it is assessment, diagnosis, monitoring, classification, synthesis, configuration, assignment, planning, or scheduling.
- Identify leaf tasks that can become orchestrator steps or reasoning services.

### Agent Model

Purpose: model task executors, human or software, including competences, authority, responsibilities, constraints, and communication links.

Auto-orchestrator adaptation:

- Agents include humans, LLM agents, tools, APIs, databases, queues, schedulers, and external systems.
- Authority and responsibility should be explicit: who may decide, recommend, approve, override, or execute?

### Knowledge Model

Purpose: specify knowledge and reasoning requirements in an implementation-independent way.

Knowledge categories:

- Domain knowledge: concepts, relations, attributes, value types, rule types, constraints, cases, and knowledge bases.
- Inference knowledge: basic reasoning steps and their dynamic/static roles.
- Task knowledge: task goals, decomposition, control structure, loops, branch conditions, and transfer functions.

Auto-orchestrator adaptation:

- Domain schema maps to typed objects, ontologies, schemas, policy models, or knowledge graph shapes.
- Knowledge bases map to rule sets, policy versions, examples, cases, retrieval corpora, constraint stores, and preference models.
- Inferences map to callable reasoning units with explainable inputs and outputs.
- Task knowledge maps to orchestration control.

### Communication Model

Purpose: specify information exchange between tasks carried out by different agents.

Construction layers:

1. Communication plan: the overall dialogue between agents.
2. Transactions: exchange links between leaf tasks performed by different agents.
3. Information exchange specification: messages, content, form, medium, control, and intent.

Useful communication intent types:

- Information exchange: `ask`, `reply`, `report`, `inform`
- Task delegation: `request`, `require`, `order`, `reject-td`
- Task adoption: `propose`, `offer`, `agree`, `reject-ta`

Auto-orchestrator adaptation:

- Each handoff, tool call, human approval, notification, bid, or reply should have content, sender, receiver, constraints, and intent.
- Support information such as explanations and error messages belongs in the communication model when it affects task support.

### Design Model

Purpose: convert conceptual requirements into technical architecture, implementation platform, modules, representational constructs, and mechanisms.

Auto-orchestrator adaptation:

- Preserve structure: tasks to orchestration units, inferences to reasoning services, domain schema to typed models, knowledge bases to versioned stores, transactions to protocols, and communication plan to workflow/API contracts.
- Add traces for task state, inference roles, knowledge-base versions, transaction status, and explanation paths.

## Knowledge Model Construction Process

### Stage 1: Knowledge Identification

Activities:

- Survey information sources for the selected task.
- Build a domain glossary.
- Construct representative scenarios.
- List reusable task templates and domain components.

Guidelines adapted:

- Talk to knowledgeable non-experts who understand the domain but are not primary experts.
- Avoid detailed theories until their usefulness is proven.
- Create typical scenarios that can be understood at a global level.

### Stage 2: Knowledge Specification

Activities:

- Choose a task template.
- Construct an initial domain schema.
- Complete domain, inference, and task knowledge.

Template choice criteria:

- Nature of output: category, fault, plan, schedule, design, assignment, recommendation.
- Nature of input: observations, requirements, preferences, constraints, cases, events.
- Nature of the target system: process, artifact, human organization, software system, domain entity.
- Environmental constraints: certainty, cost of observations, latency, safety, reversibility.

Modeling routes:

- Middle-out: start with inference structure from a suitable template, then map roles to domain and task knowledge.
- Middle-in: refine task decomposition and domain schema in parallel when templates are too coarse.

### Stage 3: Knowledge Refinement

Activities:

- Validate the model.
- Complete knowledge bases only after validation is at least partly successful.

Validation techniques:

- Paper simulation with `domain step`, `model action`, and `explanation`.
- Mock-up or prototype simulation.
- Internal consistency checks.
- Communication plan walk-through.
- Wizard-of-Oz validation for human-system interaction.

## Reusable Task Templates for Orchestrators

- Classification: map observations to predefined classes.
- Assessment: judge a case against norms, criteria, or decision categories.
- Diagnosis: explain symptoms by hypothesizing and verifying faults or causes.
- Monitoring: detect discrepancy in an ongoing process by comparing findings to norms.
- Synthesis: generate structures from requirements, hard constraints, and soft preferences.
- Configuration design: assemble predefined components under constraints and preferences.
- Assignment: allocate objects or resources to targets.
- Planning: construct a sequence or structure of future actions.
- Scheduling: assign activities to time/resources under constraints.

For LLM or multi-agent systems, task names in the application are not enough. Check actual inputs, outputs, constraints, and reasoning behavior before selecting a template.

## Failure Patterns Noted for Skill Design

- A "knowledge base" implemented as a flat pile of rules or text.
- A tool-centric architecture selected before task and knowledge modeling.
- No separation between domain concepts, inference roles, and task control.
- Communication treated as generic messages rather than typed transactions with intent and constraints.
- Expert interviews conducted without scenario-based validation.
- Knowledge bases completed before the model has proven it can generate required behavior.
- Design failing to preserve conceptual structure, making the system hard to explain and maintain.

## Supplemental Metadata Assessment

The manifest and local source files provide enough metadata for distillation: entry id, title, skill name, skill directory, and source files are present. The book source includes full bibliographic and methodological context: *Knowledge Engineering and Management: The CommonKADS Methodology* by Guus Schreiber, Hans Akkermans, Anjo Anjewierden, Robert de Hoog, Nigel Shadbolt, Walter Van de Velde, and Bob Wielinga, MIT Press, 2000. The website source identifies CommonKADS as a structured knowledge engineering methodology.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: CommonKADS knowledge engineering sources and local KE entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Organization, task, agent, knowledge, communication, and design models; expertise is elicited into reusable structures.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not build a broad ontology when the task model only needs a narrow inference pattern.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Knowledge engineering is not dumping expert facts; it models the task that uses knowledge, the agents who hold it, and the communication that moves it.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Elicit task goals, inferences, domain concepts, roles, communication acts, examples, edge cases, and validation scenarios; then map them to implementation artifacts.
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
