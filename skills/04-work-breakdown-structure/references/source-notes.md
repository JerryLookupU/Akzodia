# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
: Work Breakdown Structure

## Sources Used

## Metadata

- NASA source: `NASA Work Breakdown Structure (WBS) Handbook`, NASA/SP-20210023927, November 2021. The NTRS record also points to a 2019 NASA/SP-3404 record acquired January 15, 2020; the full source text provided is the November 2021 revision.
- PMI source: Shelly A. Brotherton, Robert T. Fried, and Eric S. Norman, `Applying the work breakdown structure to the project management lifecycle`, PMI Global Congress 2008, published October 19, 2008.

## Distilled Principles

- WBS is a product or deliverable-oriented hierarchy for the total approved scope. It describes the "what" of the project, not the execution sequence.
- The top element represents the entire project. Descending levels provide increasingly detailed elements until work can be assigned, estimated, verified, and controlled.
- The 100% rule applies at every parent-child relationship: child scope must equal all parent scope and must not include unauthorized work.
- A WBS dictionary is a separate control artifact that defines each element, removes ambiguity, records interfaces, and links the element to requirements/specifications and reporting tags.
- A single WBS can support technical, schedule, cost, performance, risk, and communication management when those systems share WBS element codes.
- Schedules should be derived from the WBS by decomposing lowest-level work packages into activities, milestones, dependency networks, and schedule baselines.
- Ownership should be mapped to WBS elements through a responsibility matrix. Organizational structure should not determine the WBS hierarchy.
- Contractor, partner, or subagent work should extend and trace back to the project WBS rather than becoming a disconnected plan.
- WBS depth is contextual. High-risk, high-cost, complex, or management-critical branches may need more decomposition than simple branches.
- After scope baseline, WBS changes require change control and dictionary updates.

## Auto-Orchestrator Translation

- Treat the WBS as the orchestration spine. Every agent assignment, artifact, status update, risk, and acceptance check should reference a WBS code.
- Use nouns for agent work packages: `evaluation harness`, `data ingestion adapter`, `policy test corpus`, `deployment runbook`. Derive verbs later as tasks.
- Keep top-level branches focused on deliverables or enabling controls, not on subagent names, tools, repos, or calendar phases.
- Use a WBS dictionary to make each agent handoff inspectable: included scope, excluded scope, inputs, outputs, acceptance criteria, dependencies, owner, and review point.
- For multi-agent plans, use the 100% rule to detect missing deliverables and duplicated work before dispatching agents.
- Use scope relationship diagrams or parent-child plus dependency maps when a flat outline hides inclusion and sequence differences.

## Failure Signals From Sources

- Prior WBS templates can import old mistakes.
- Phase-oriented or function-oriented elements such as `Phase C`, `Engineering`, `Manufacturing`, or `Testing` obscure product scope.
- Breaking out centers, vendors, or teams too high in the hierarchy fragments deliverable rollups.
- Incorrect hierarchy occurs when parent-child structure does not reflect real inclusion; sequencing or shared ownership is not enough to make something a child.
- A WBS without a dictionary leaves content boundaries unclear and weakens scheduling, cost, risk, and performance controls.

## Short Source Anchors

- NASA describes WBS as a product-oriented family tree for hardware, software, services, data, and other deliverables.
- PMI emphasizes deliverable-oriented hierarchical decomposition and the 100% rule.
- PMI distinguishes WBS scope from processes, schedule, and timing.
- NASA emphasizes the WBS dictionary, coding, control accounts, change control, and integration with cost/schedule/risk systems.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Work Breakdown Structure practice sources and local theory-pack entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Deliverable tree + 100 percent rule + WBS dictionary. Decompose product scope, not calendar order.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not encode sequence, sprint timing, org chart, or dependency graph as the WBS hierarchy.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The WBS is a scope completeness device. Its deepest value is preventing hidden work, duplicated work, and unowned deliverables before scheduling begins.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Ask what final artifacts must exist, then recursively partition until each work package has acceptance criteria, owner, exclusions, interfaces, and risk notes. If a child is an activity rather than a deliverable, reframe it.
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
