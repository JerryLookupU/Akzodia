---
name: 44-knowledge-engineering
description: Use when designing, auditing, or refactoring an auto-orchestrator whose behavior depends on domain knowledge, expert rules, reusable task templates, human/agent communication, or knowledge-base reuse. Triggers on requests to turn tacit expertise, policies, domain rules, decision workflows, or agent memory into an executable orchestration design.
---

# Knowledge Engineering

## When To Use

Use this skill when an orchestrator must do knowledge work rather than simple control flow:

- Experts, policies, runbooks, books, logs, or prior cases must become reusable agent behavior.
- The task involves assessment, diagnosis, monitoring, classification, configuration, assignment, planning, scheduling, or another reasoning pattern.
- The design must separate domain knowledge, inference steps, task control, and agent communication before implementation.
- The system needs explainable traces, maintainable rule sets, domain schemas, or reusable knowledge assets.
- A proposed agent looks like a single flat prompt or rule dump and needs a structured knowledge model.

## Workflow

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

## Failure Modes

- Mining trap: treating expertise as text to extract verbatim instead of constructing purpose-specific models.
- Flat knowledge base: storing all rules together without domain schemas, rule types, inference roles, ownership, or validation scenarios.
- Premature implementation: choosing vector stores, prompts, rules engines, or workflow engines before modeling task, knowledge, and communication structure.
- Template mismatch: forcing diagnosis, planning, or assessment labels onto a task because names sound similar instead of checking inputs, outputs, and reasoning behavior.
- Missing agent constraints: ignoring authority, responsibility, permissions, latency, privacy, or human approval boundaries.
- Unvalidated communication: specifying internal reasoning but not how information, intent, exceptions, and explanations move between agents.
- Over-modeling: building broad ontologies or detailed theories that are not needed for the selected task or scenarios.
- No maintenance path: failing to assign ownership, versioning, test cases, and change impact checks for knowledge assets.

## Boundaries

This skill is for auto-orchestrator design work where knowledge, expertise, and reasoning structure matter. It is not needed for simple scripts, CRUD applications, purely numeric optimization, generic prompt writing, or ordinary backend routing unless domain knowledge and agent reasoning are central.

Do not use it to summarize knowledge-engineering literature. Use it to produce design artifacts: context/task/agent models, knowledge models, communication models, validation traces, and implementation mappings.

Keep the conceptual model implementation-independent until validation shows it explains required behavior. Then map it into concrete architecture without flattening the task, inference, domain, and communication boundaries.
