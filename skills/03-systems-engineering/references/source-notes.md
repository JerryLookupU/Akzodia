# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
: Systems Engineering

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Metadata

- Main work: NASA Systems Engineering Handbook.
- NASA web page title: `Systems Engineering Handbook - NASA`.
- NASA page date: updated February 6, 2019.
- Handbook identifier found in source: `NASA SP-2016-6105 Rev2`, superseding `SP-2007-6105 Rev 1`.
- INCOSE source role: professional association context and current resource/certification ecosystem, not the substantive process source.

## Distilled Concepts

NASA defines systems engineering as a methodical, multidisciplinary approach for designing, realizing, technically managing, operating, and retiring systems. A system includes hardware, software, facilities, people, processes, and procedures; the whole-system result comes from how parts relate, not just from the parts themselves.

The central executable pattern is the SE engine:

- System design flows downward through stakeholder expectations, technical requirements, logical decomposition, and design solution definition.
- Product realization builds upward through implementation, integration, verification, validation, and transition.
- Technical management runs across the entire lifecycle through planning, requirements management, interface management, technical risk management, configuration management, data management, technical assessment, and decision analysis.

NASA emphasizes recursive and iterative use of these processes. The engine is applied repeatedly down the product structure to reach implementable elements, then up the product structure to integrate, verify, validate, and transition the system.

The handbook distinguishes verification from validation:

- Verification proves conformance to specified requirements.
- Validation proves the realized product accomplishes the intended purpose in the intended environment.

For orchestrator design, this distinction prevents a common failure: completing subtasks while failing the user's real operational need.

The NASA lifecycle phases were converted into an orchestrator lifecycle:

- Concept and feasibility: clarify mission need, stakeholders, scenarios, rough risks.
- Architecture and requirements: baseline expectations, requirements, interfaces, plans.
- Detailed design and implementation: allocate functions and implement or delegate components.
- Integration and test: assemble subagent/tool outputs and prove requirements.
- Operations and sustainment: monitor behavior, manage change, handle anomalies.
- Closeout: transition results, preserve evidence, retire or archive state.

The source also emphasizes cost and risk timing: early design decisions commit much of lifecycle cost, and late changes are expensive. For auto-orchestrators this maps to early decisions about memory model, tool policy, approval routing, state ownership, verification gates, and interface schemas.

## Adaptation Rationale

The skill was not written as a generic systems engineering summary. It translates the NASA process model into an auto-orchestrator design routine:

- Stakeholder expectations become user goals, owner policies, budget limits, and operational success criteria.
- ConOps becomes normal and off-nominal orchestration scenarios.
- Technical requirements become traceable behavioral requirements for agents, tools, evidence, state, and handoffs.
- Interfaces become contracts between planner, subagents, tools, memory, verifier, and user reporting.
- Verification and validation become separate evidence loops.
- Technical management becomes compact but continuous tracking of requirements, risks, configurations, data, assessments, and decisions.

## Supplementation

The provided source content was sufficient for this entry after extracting metadata from the NASA page and handbook front matter. No external web supplementation was needed.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Systems engineering source notes and local theory-pack entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Need -> requirements -> functions -> interfaces -> verification -> validation -> transition. Keep traceability alive across the lifecycle.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use full systems engineering for one-off execution where lifecycle, integration, or stakeholder traceability is not at risk.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The unique insight is that complex work fails at interfaces and lifecycle transitions, not only inside components. Requirements are not a list; they are a contract that must survive design, integration, evidence, and handoff.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Walk a stakeholder expectation forward into functions, interfaces, verification evidence, validation scenarios, risk owners, and transition criteria. Gaps in that trace are the defects.
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
