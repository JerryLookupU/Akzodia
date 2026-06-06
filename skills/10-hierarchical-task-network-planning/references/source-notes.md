# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Local Sources

## Metadata

This entry is a theory/system entry rather than a single book.

Primary paper represented by the JAIR/arXiv source:
- Dana Nau, Tsz-Chiu Au, Okhtay Ilghami, Ugur Kuter, J. William Murdock, Dan Wu, and Fusun Yaman.
- "SHOP2: An HTN Planning System."
- Journal of Artificial Intelligence Research, volume 20, pages 379-404, published December 2003.
- DOI: `10.1613/jair.1141`.

Supplementary project source:
- University of Maryland SHOP project page describing SHOP, SHOP2, and JSHOP2 as domain-independent automated planning systems based on ordered task decomposition, a form of HTN planning.

## Distilled Claims

- HTN planning starts from an initial world state and a task network, then recursively decomposes compound tasks into subtasks until primitive tasks can be performed by operators.
- Methods are schemas for decomposing compound tasks. A method has a task head, preconditions, and subtasks; multiple applicable methods create search branches.
- Operators perform primitive tasks and define preconditions and effects. The planner updates state as primitive actions are added to the plan.
- SHOP2 plans forward in the same order actions will execute, which lets method and operator preconditions be evaluated against the current state rather than an abstract future state.
- SHOP2 supports partially ordered subtasks, so subtasks from different compound tasks may interleave when constraints allow.
- Domain knowledge is central: HTN methods often represent standard operating procedures and can make planning practical for complex domains.
- Search control matters. SHOP2 can sort alternative variable bindings by a criterion and can use branch-and-bound to improve plan quality within a time limit.
- Axioms, numeric computations, and external function calls can keep the HTN model expressive without encoding every calculation as a decomposition method.
- Temporal and concurrent domains can be handled by maintaining bookkeeping state, such as read/write timing for dynamic properties.

## Distillation Choices

- Converted formal HTN/SHOP2 concepts into an auto-orchestrator design workflow: state facts, compound tasks, primitive operators, methods, preconditions, effects, branch ranking, and traceable decomposition.
- Emphasized ordered task decomposition because it maps directly to agent orchestration where tool actions mutate shared state.
- Kept optimization pragmatic: rank branches first, reserve branch-and-bound for cases where quality gains justify extra planning time.
- Treated temporal multi-timeline preprocessing as a reusable design pattern: track per-resource read/write conflicts or use explicit locks/versions.
- Avoided long quotations; all source content is paraphrased.

## Auto-Orchestrator Translation

- Compound task: a high-level agent objective that cannot be directly executed.
- Primitive task/operator: a command, API call, edit, message, test, review, deployment, or other executable action.
- Method: a reusable playbook selected when its preconditions match the current state.
- World state: facts about files, tools, user approvals, budget, resource locks, completed evidence, and failed branches.
- Preconditions: facts that must be true before selecting a method or executing an action.
- Effects: facts added, removed, or changed after an action.
- Partial order: constraints that allow safe interleaving or parallel work.
- Backtracking: abandon a failed method/binding and try the next ranked alternative while preserving failure evidence.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: HTN planning sources and local task-network entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Compound tasks decompose through methods into primitive tasks under ordering constraints. Domain procedure is the heuristic.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use HTN if there are no reusable methods or if the goal is better modeled as pure state-space search.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: HTN’s power is procedural knowledge: it narrows search by encoding how experts actually accomplish a class of goals.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Separate primitive actions from compound tasks, write alternative methods with preconditions, then inspect where backtracking, partial ordering, or no-op methods are needed.
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
