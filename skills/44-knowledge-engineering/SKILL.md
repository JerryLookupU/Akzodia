---
name: 44-knowledge-engineering
description: Use when designing, auditing, or refactoring an auto-orchestrator whose behavior depends on domain knowledge, expert rules, reusable task templates, human/agent communication, or knowledge-base reuse. Triggers on requests to turn tacit expertise, policies, domain rules, decision workflows, or agent memory into an executable orchestration design.
source_files:
  - references/source-notes.md
---
# 44 Knowledge Engineering

## Book-Derived Essence

- Core framework: Organi

zation, task, agent, knowledge, communication, and design models; expertise is elicited into reusable structures.
- Deep idea: Knowledge engineering is not dumping expert facts; it models the task that uses knowledge, the agents who hold it, and the communication that moves it.
- Discovery method: Elicit task goals, inferences, domain concepts, roles, communication acts, examples, edge cases, and validation scenarios; then map them to implementation artifacts.
- Boundary: Do not build a broad ontology when the task model only needs a narrow inference pattern.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestrator must do knowledge work rather than simple control flow:

- Experts, policies, runbooks, books, logs, or prior cases must become reusable agent behavior.
- The task involves assessment, diagnosis, monitoring, classification, configuration, assignment, planning, scheduling, or another reasoning pattern.
- The design must separate domain knowledge, inference steps, task control, and agent communication before implementation.
- The system needs explainable traces, maintainable rule sets, domain schemas, or reusable knowledge assets.
- A proposed agent looks like a single flat prompt or rule dump and needs a structured knowledge model.

## Standalone Contract

This `SKILL.md` contains the complete runtime procedure. Do not rely on external books, webpages, source reports, source snapshots, original source paths, or parent-directory materials to execute it. `references/source-notes.md` is provenance-only and may be read only for source trace audits.

Required task inputs are the target knowledge-intensive task, domain objective, stakeholders or agents, available knowledge sources, expected outputs, constraints, and validation scenarios. If the user has not provided enough information, ask for the smallest missing item that changes the knowledge model, or proceed with explicit assumptions.

## Activation And Execution Gate

Trigger only when the request asks to design, audit, or refactor an orchestrator whose behavior depends on domain expertise, policies, reusable reasoning patterns, agent communication, explainable knowledge assets, or maintainable task/agent/knowledge models.

Do not trigger for simple CRUD, generic prompt writing, deterministic transformations, literature summaries, basic RAG setup, or backend routing unless domain knowledge and agent reasoning structure are central.

Before executing the workflow, verify all gate conditions:

- The task involves specialized judgment, domain concepts, heuristic rules, explanation, reusable reasoning, or agent handoffs.
- The user needs a design artifact, audit, validation trace, or implementation mapping rather than a prose summary.
- There is enough context to identify at least one task, one agent or actor, and one knowledge source or domain rule family.

If the gate fails, state why knowledge engineering is not the right frame and suggest the simpler software, retrieval, rules, or workflow approach.

## Workflow

Execute the steps in order. Keep organization, task, agent, knowledge, communication, and design models distinct until validation shows how they should connect.

1. Frame the knowledge task in context.
   - Identify the business or user objective, the knowledge-intensive task, expected benefits, costs, risks, and organizational constraints.
   - Write the task boundary as `goal`, `inputs`, `outputs`, `preconditions`, `quality criteria`, `resources`, and `failure impact`.
   - Name the agents involved: humans, software agents, tools, stores, APIs, and external systems. Record each agent's competence, authority, responsibility, and constraints.

2. Decide whether this is a knowledge-engineering problem.
   - Treat it as knowledge engineering when success depends on specialized judgment, domain concepts, heuristic rules, explanation, or reusable reasoning.
   - Treat it as ordinary software flow when the task is only CRUD, deterministic transformation, formula application, or simple routing.
   - If unsure, build three concrete scenarios and ask whether an expert must explain why the right result follows.

3. Build the CommonKADS-style model suite.
   - Organization model: why the orchestrator should exist, where knowledge bottlenecks or opportunities sit, and what changes if automation succeeds.
   - Task model: the relevant tasks, decomposition, inputs, outputs, constraints, performance criteria, and dependencies.
   - Agent model: who or what performs each task, with capabilities, authority, communication links, and constraints.
   - Knowledge model: domain knowledge, inference knowledge, and task knowledge for the selected knowledge-intensive task.
   - Communication model: information exchanges between agents, including messages, intent, control, and support information.
   - Design model: implementation architecture that preserves the conceptual knowledge and communication structure.

4. Construct the knowledge model.
   - Identify sources: expert interviews, manuals, policies, examples, logs, ontologies, schemas, prior workflows, and benchmark cases.
   - Create a small glossary and three to seven representative scenarios before modeling details.
   - Choose or adapt a task template. Prefer proven templates for classification, assessment, diagnosis, monitoring, synthesis, configuration design, assignment, planning, or scheduling.
   - Define domain knowledge as concepts, relations, attributes, value types, rule types, constraints, cases, and knowledge bases. Avoid one flat rule store.
   - Define inference knowledge as the smallest explainable reasoning steps. Use role names that describe how data is used, such as `finding`, `hypothesis`, `norm`, `difference`, `constraint`, `preference`, or `candidate`.
   - Define task knowledge as goals, decomposition, control structure, loops, branch conditions, and transfer functions that obtain or deliver information through other agents.

5. Pick a modeling route.
   - Use middle-out modeling when a task template already provides an inference structure close to the target behavior. Start from inferences, then map roles to domain concepts and task control.
   - Use middle-in modeling when the template is too coarse. Refine task decomposition and domain schema in parallel until they meet at concrete inferences.
   - A good inference structure explains the reasoning at the level stakeholders need and usually maps each inference to one primary static knowledge type.

6. Model agent communication.
   - For each leaf task or transfer function, list information objects that cross agent boundaries.
   - Create one transaction for each distinct information object exchange between a pair of tasks carried out by different agents.
   - For each transaction, specify sender, receiver, information object, constraints, message content, message control, and communication type.
   - Use intent labels deliberately: `ask`, `reply`, `inform`, `report`, `request`, `require`, `order`, `propose`, `offer`, `agree`, and rejection variants.
   - Add supporting information items such as explanations, help text, confidence, provenance, and error recovery when they affect user or agent task performance.

7. Validate before implementation.
   - Run paper simulations against the representative scenarios. Use a table with columns `domain step`, `model action`, and `explanation`.
   - Check that every scenario step maps to a task, inference, domain role, transaction, or explicit out-of-scope decision.
   - Walk through the communication plan with a reviewer who was not involved in the design.
   - Validate that the model can generate required problem-solving behavior before completing large knowledge bases.
   - Revise the task template, inference roles, domain schema, or communication transactions when the trace has gaps.

8. Map to implementation with structure preservation.
   - Preserve the analysis structure in code: tasks become orchestration units, inferences become callable reasoning services, domain schemas become typed models or ontologies, knowledge bases become versioned stores, and transactions become protocol/API contracts.
   - Keep implementation details out of the conceptual model until the design phase.
   - Add observability for task state, selected template, inference inputs/outputs, knowledge-base version, transaction status, and explanation trace.
   - Document maintenance ownership for each domain schema, rule type, template, and knowledge base.

## Output Format And Deliverables

Return a knowledge-engineering design or audit with these sections:

- `task_boundary`: goal, inputs, outputs, preconditions, quality criteria, resources, constraints, and failure impact.
- `model_suite`: organization, task, agent, knowledge, communication, and design model summaries.
- `knowledge_model`: domain concepts, relations, attributes, rule types, inference roles, task control, and reusable templates.
- `communication_model`: transactions with sender, receiver, information object, intent, constraints, support information, and recovery behavior.
- `validation_trace`: representative scenarios mapped to domain steps, model actions, explanations, and gaps.
- `implementation_mapping`: orchestration units, reasoning services, schemas, stores, protocols, traces, and maintenance ownership.
- `open_risks`: missing expertise, weak scenarios, unclear authority, unvalidated templates, or maintenance gaps.

For audits, report findings by severity and identify which model layer or transaction is affected.

## Failure Modes

- Mining trap: treating expertise as text to extract verbatim instead of constructing purpose-specific models.
- Flat knowledge base: storing all rules together without domain schemas, rule types, inference roles, ownership, or validation scenarios.
- Premature implementation: choosing vector stores, prompts, rules engines, or workflow engines before modeling task, knowledge, and communication structure.
- Template mismatch: forcing diagnosis, planning, or assessment labels onto a task because names sound similar instead of checking inputs, outputs, and reasoning behavior.
- Missing agent constraints: ignoring authority, responsibility, permissions, latency, privacy, or human approval boundaries.
- Unvalidated communication: specifying internal reasoning but not how information, intent, exceptions, and explanations move between agents.
- Over-modeling: building broad ontologies or detailed theories that are not needed for the selected task or scenarios.
- No maintenance path: failing to assign ownership, versioning, test cases, and change impact checks for knowledge assets.

## Failure, Recovery, And Idempotency

- If sources are incomplete, build a minimal model from known scenarios and mark missing expert, policy, or case evidence explicitly.
- If the task template does not fit, do not force it; return to task decomposition and choose a narrower template or custom inference structure.
- If agent authority is unclear, stop before implementation mapping and request the decision, approval, override, or execution boundary.
- If an existing model exists, preserve stable names for tasks, agents, domain concepts, transactions, and rule families unless evidence requires a rename.
- Re-running this skill should refine the same model suite, add validation scenarios, or update mappings without flattening the conceptual layers.
- If validation fails, keep the failed trace as evidence and revise the task template, inference roles, domain schema, or communication transactions before proposing implementation.

## Boundaries

This skill is for auto-orchestrator design work where knowledge, expertise, and reasoning structure matter. It is not needed for simple scripts, CRUD applications, purely numeric optimization, generic prompt writing, or ordinary backend routing unless domain knowledge and agent reasoning are central.

Do not use it to summarize knowledge-engineering literature. Use it to produce design artifacts: context/task/agent models, knowledge models, communication models, validation traces, and implementation mappings.

Keep the conceptual model implementation-independent until validation shows it explains required behavior. Then map it into concrete architecture without flattening the task, inference, domain, and communication boundaries.

## Hard Rules

- Do not collapse expert knowledge into a single flat prompt, rule dump, or undifferentiated knowledge base.
- Do not choose vector stores, rules engines, workflow engines, or agent frameworks before modeling task, knowledge, agent, and communication structure.
- Every implementation mapping must preserve the validated conceptual structure or explain why a layer is intentionally omitted.
- Every knowledge asset must have ownership, versioning, validation evidence, and a change-impact path.
- Keep runtime execution self-contained in this `SKILL.md`; provenance notes are not required to perform the workflow.

## Source Closure

This 44-knowledge-engineering skill is self-contained for runtime use; its source basis is CommonKADS knowledge engineering sources and local KE entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
