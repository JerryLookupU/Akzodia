---
name: 06-信息组织-the-discipline-of-organizing
description: Use when designing or repairing an auto-orchestrator's information organization: resource collections, task/agent taxonomies, metadata schemas, category systems, retrieval paths, supported interactions, versioned knowledge stores, or handoff structures. Trigger when resources are hard to find, categories overlap, metadata is inconsistent, agents use different naming schemes, or orchestration needs an explicit organizing system rather than an ad hoc folder/list.
---

# The Discipline of Organizing

## When To Use

Use this skill when orchestration work depends on how resources are named, described, classified, arranged, discovered, and acted on.

Strong triggers:
- A multi-agent workflow has files, prompts, tools, tickets, datasets, tasks, memories, or outputs that agents cannot reliably find or distinguish.
- The user asks for a taxonomy, ontology-lite structure, metadata model, folder/repo layout, tagging scheme, knowledge base, resource catalog, or information architecture for an orchestrator.
- Categories overlap, naming is inconsistent, duplicate resources appear, or different agents use incompatible descriptions for the same things.
- Retrieval quality is poor because resource descriptions, facets, relationships, or interaction paths were never designed.
- A plan needs to define which interactions the system supports: find, compare, combine, route, hand off, audit, reuse, update, archive, or personalize.
- The orchestration system must scale from a small collection to many resources without losing provenance, ownership, lifecycle state, or access control.

Prefer a simple checklist or naming convention when there are few resources, one actor, and no repeated retrieval or handoff risk.

## Workflow

1. Define the organizing system.
   - State the collection boundary: what counts as a resource, what is out of scope, and whether resources are physical, digital, conceptual, human, procedural, or mixed.
   - Name the primary users or agents and the interactions the system must support.
   - Capture the operating context: frequency of change, scale, access constraints, lifecycle states, regulatory/audit needs, and expected growth.
   - Treat the output as an intentionally arranged collection of resources plus supported interactions, not just a taxonomy.

2. Inventory resources and resource types.
   - List representative resources and group them by type only after seeing examples.
   - For each type, record identity rules, granularity, owner, source of truth, lifecycle states, and common failure cases.
   - Decide whether resources should be split, merged, versioned, linked, archived, or represented as metadata-only records.
   - Make hidden resources explicit: decisions, assumptions, prompts, evaluation results, schemas, credentials references, policies, and handoff contracts.

3. Choose organizing principles.
   - Select properties that matter for the required interactions: topic, function, user intent, dependency, source, lifecycle state, risk, ownership, authority, time, geography, format, or domain.
   - Separate stable intrinsic properties from contextual or task-specific properties.
   - Prefer multiple facets when one hierarchy would force arbitrary placement.
   - Define rules for category membership, allowed values, synonyms, aliases, deprecated terms, and conflict resolution.
   - Avoid categories that sound tidy but do not change routing, retrieval, validation, or action.

4. Design descriptions and relationships.
   - Specify a minimal metadata schema for each resource type: required fields, optional fields, controlled vocabulary, free-text fields, provenance, and update responsibility.
   - Model relationships that support orchestration: depends-on, produces, consumes, duplicates, supersedes, belongs-to, owned-by, validates, blocks, references, and derived-from.
   - Add identifiers that survive renaming and moving.
   - Define how descriptions are created: manual curation, extraction, LLM classification, tool output, user input, or hybrid review.
   - Include confidence and review status when classification is automated or ambiguous.

5. Map interactions to access paths.
   - For each supported interaction, describe the user/agent question, required metadata, retrieval path, ranking or filtering logic, and expected output.
   - Design paths for common tasks: locate the canonical resource, compare alternatives, find all dependencies, route work to an owner, trace provenance, audit changes, and identify stale resources.
   - Make interaction tradeoffs explicit: precision versus recall, speed versus completeness, rigid control versus flexible discovery.
   - Add feedback loops so failed searches, misroutes, duplicates, and stale categories improve the organizing system.

6. Produce the orchestration artifact.
   - Return the resource type model, taxonomy or facets, metadata schema, relationship model, naming rules, lifecycle policy, and interaction map.
   - Include examples of correctly described resources and at least two ambiguous cases with resolution rules.
   - Name ownership: who or what maintains each schema, vocabulary, category, and quality check.
   - Define migration steps from the current mess to the target structure without breaking active work.

7. Validate with retrieval and handoff scenarios.
   - Test whether a new agent can find the right resource from a realistic prompt.
   - Test whether two similar resources are distinguishable.
   - Test whether stale, duplicate, restricted, or superseded resources are handled correctly.
   - Revise categories and metadata only when the test failure reveals a real interaction failure, not just aesthetic dissatisfaction.

## Failure Modes

- Treating organization as folder naming only. Folders are one access path, not the whole organizing system.
- Building a single grand hierarchy for resources that need multiple facets, such as task type, domain, lifecycle state, and owner.
- Choosing categories before inspecting real resources and interactions.
- Optimizing for the curator's mental model while ignoring how agents and users actually search, route, compare, and update resources.
- Creating metadata fields no one can populate, maintain, or use in a decision.
- Letting automated classification silently overwrite human judgment, provenance, or exception handling.
- Hiding lifecycle state, so draft, current, deprecated, superseded, archived, and experimental resources look equally authoritative.
- Conflating resource identity with file path, display name, ticket title, or model-generated label.
- Over-normalizing early discovery work, which can freeze uncertainty before categories are stable.

## Boundaries

This skill designs information organization for orchestration. It is not a full database design method, search relevance algorithm, records-retention legal review, or knowledge graph engineering process. Pair it with those methods when the system requires implementation-level storage, ranking, compliance, or graph analytics.

Use WBS or DSM first when the central problem is scope decomposition or dependency sequencing. Use this skill when the central problem is how resources are described, categorized, retrieved, related, governed, and acted on.

Do not impose a heavyweight taxonomy on a small one-off task. The organizing effort should be proportional to resource count, change rate, reuse value, ambiguity, compliance burden, and coordination cost.

When source content is incomplete or contested, label the structure provisional and design feedback mechanisms. An organizing system should evolve from evidence of use, not from abstract neatness.
