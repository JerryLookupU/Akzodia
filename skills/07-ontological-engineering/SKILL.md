---
name: 07-ontological-engineering
description: Use when designing or repairing an auto-orchestrator that needs an explicit task/domain vocabulary, capability taxonomy, typed agent/tool registry, routing schema, slot constraints, competency questions, or a clean separation between domain knowledge and operational execution logic.
---

# 07 Ontological Engineering

## When To Use

Use this skill when orchestration decisions depend on a shared conceptual model rather than another prompt rule. Typical triggers:

- A multi-agent system needs a vocabulary for task types, roles, tools, resources, policies, artifacts, states, or handoffs.
- Routing is brittle because labels overlap, synonyms are treated as different concepts, or capabilities are buried in code.
- You need to decide whether something should be modeled as a task class, capability property, runtime instance, constraint, or relation.
- You are designing an auto-orchestrator registry, planner, delegation layer, policy gate, evaluation taxonomy, or tool-selection schema.
- You need competency questions such as "which agent can handle this?", "what must be known before dispatch?", "what makes this task unsupported?", or "which policy constrains this route?"

## Workflow

1. Define the domain and scope.
   - State the domain the orchestrator must cover and what it must not cover.
   - Name the users and maintainers of the model.
   - Write competency questions that the ontology must answer. For orchestrators, include routing, eligibility, required inputs, fallback behavior, output contracts, and policy constraints.

2. Reuse before inventing.
   - Check existing task taxonomies, tool schemas, policy vocabularies, product concepts, logs, and registry formats.
   - Reuse or extend stable concepts when interoperability matters. Create new concepts only when the existing vocabulary cannot answer the competency questions.

3. Enumerate terms without modeling too early.
   - List task intents, agent roles, tools, resources, artifacts, states, constraints, risks, policies, output types, ownership boundaries, and failure conditions.
   - Keep synonyms together. Do not create separate concepts merely because the system has multiple names for the same thing.

4. Convert terms into ontology elements.
   - Classes are durable concepts: `Task`, `Capability`, `Tool`, `Artifact`, `Policy`, `Agent`, `KnowledgeSource`, `ExecutionState`.
   - Slots/properties describe classes: `requiresInput`, `producesArtifact`, `allowedTools`, `riskLevel`, `handledBy`, `blockedByPolicy`, `dependsOn`.
   - Facets constrain slots: value type, allowed class/range, cardinality, required/optional status, default value, and whether a value is inherited or overrideable.
   - Instances are concrete runtime or registry items: a specific tool, agent profile, policy rule, run state, or task example.

5. Build the class hierarchy around "is-a".
   - Use top-down, bottom-up, or mixed development depending on what is clearest for the domain.
   - A subclass must be a real kind of its parent. If every `CodeReviewTask` is a `Task`, the relation is valid; if `UrgentTask` changes minute by minute, model urgency as a slot.
   - Keep siblings at the same level of generality. Do not place `ResearchTask` and `FindRecentSEC10K` as direct siblings unless both are intended to be route-level categories.
   - Use multiple inheritance only when both parents contribute real inherited meaning, such as `HighRiskDataTask` being both `DataTask` and `PolicySensitiveTask`.

6. Attach properties at the most general valid class.
   - Put a slot on the highest class where every instance can validly have that property.
   - Keep domains and ranges general enough to cover valid fillers, but not so general that anything fits.
   - Add inverse relations where orchestration benefits from both directions, such as `handledBy` / `canHandle`, `requiresArtifact` / `satisfiesRequirement`, or `delegatesTo` / `receivesDelegation`.

7. Decide class vs property vs instance by orchestration consequences.
   - Create a class when the distinction changes required properties, constraints, routing, relationships, validation, or expert communication.
   - Use a property value when the distinction does not change orchestration behavior.
   - Use an instance for the most specific item the system must select, execute, log, or evaluate.
   - Avoid classes for unstable runtime states unless the state itself has durable behavior and constraints.

8. Separate domain knowledge from operational knowledge.
   - Keep the vocabulary, relations, and constraints declarative.
   - Keep algorithms, retries, scheduling, tool invocation, and runtime execution outside the ontology.
   - The same planner or router should be able to operate over a changed ontology without code changes when the domain changes but the orchestration method does not.

9. Validate and iterate.
   - Answer each competency question against the model. If the answer requires hidden assumptions, add explicit classes, slots, or facets.
   - Check for cycles, synonym duplication, singular/plural duplicates, singleton subclasses, overly flat sibling lists, overly deep hierarchies, and invalid "is-a" links.
   - Review with domain owners and run the ontology against real task traces.
   - Record design decisions that intentionally omit plausible facts, so future reuse does not mistake scope limits for truth.

Recommended output for orchestrator design:

| Element | Parent/Type | Key Slots | Facets/Constraints | Routing Implication |
| --- | --- | --- | --- | --- |
| Task class | superclass | required inputs, outputs, risk | cardinality, allowed values | route eligibility |
| Capability | superclass | handles, requires, produces | allowed task classes | agent/tool matching |
| Policy | superclass | appliesTo, blocks, requiresApproval | severity, jurisdiction | guardrails |
| Artifact | superclass | format, owner, provenance | required metadata | handoff contract |

## Failure Modes

- Treating the ontology as object-oriented implementation design, centered on methods rather than domain structure.
- Hard-coding domain assumptions in router code instead of making them explicit in the model.
- Modeling every possible domain fact instead of the facts needed for the orchestrator's applications.
- Creating separate classes for synonyms, spelling variants, singular/plural names, or presentation labels.
- Using invalid hierarchy links where the child is not truly a kind of the parent.
- Creating classes for volatile states such as priority, recency, availability, or user preference when a property value is enough.
- Adding subclasses that introduce no new properties, restrictions, relationships, routing behavior, or domain-expert distinction.
- Defining slot ranges so broad that validation becomes meaningless, or so narrow that valid future fillers are excluded.
- Failing to use competency questions, leaving the ontology unable to prove it supports routing decisions.

## Boundaries

This skill produces an executable conceptual model for orchestrator design; it is not a full OWL, RDF, description-logic, or Protege modeling tutorial.

Use a formal ontology tool, reasoner, or domain standard when the system needs machine-checked logical consistency, regulatory interoperability, or integration with established semantic-web vocabularies.

Do not invoke this skill for a one-off task that can be solved by direct execution without a reusable task/capability vocabulary.

The ontology should guide routing and validation, not replace runtime policy enforcement, security review, human approval, testing, observability, or incident handling.
