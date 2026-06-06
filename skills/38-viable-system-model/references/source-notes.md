# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Entry

- Entry id: 38
- Skill name: `38-viable-system-model`
- Title: `可生存系统模型 / Viable System Model`

## Assigned Source

The source states that Beer developed VSM in the 1950s while working in the Sheffield steel industry, grounded it in systems theory, Ashby's Law of Requisite Variety, cybernetics, recursive systems, and neural-network ideas, and used it as a practical tool for organizational structure. It describes VSM as applicable across scales from work groups to nation states.

## Core Source Extraction

- System 1 is the operation: autonomous operational units that interact with their environments.
- Systems 2, 3, 4, and 5 form the metasystem that helps operational elements cohere as a viable system.
- System 2 harmonizes interactions between autonomous units and prevents conflict from shaking the system apart.
- System 3 looks across operations from the inside-now perspective, creates synergy, and improves whole-system effectiveness.
- System 4 scans the outside-and-then environment, identifies threats and opportunities, and develops adaptive plans.
- System 5 creates identity, values, policy, and closure so the system does not fragment.
- A VSM diagnosis asks whether the systems are identified, properly connected, and fit for purpose.

## Supplemented Theory Metadata

The manifest and assigned source identify the theory, but they do not provide formal bibliographic metadata for Beer's books or the full VSM diagnostic method. Minimal supplemental theory context was added from established VSM lineage:

- Theory: Stafford Beer's Viable System Model.
- Representative author: Stafford Beer.
- Representative works: `Brain of the Firm`, `The Heart of Enterprise`, and `Diagnosing the System for Organizations`.
- Domain: management cybernetics, organizational diagnosis, recursive viable systems, and autonomy/coherence design.
- Added concept: System 3* audit channels, a standard VSM diagnostic element used to verify operational reality beyond routine reports.

## Auto-Orchestrator Mapping

For agent runtimes, VSM becomes a structural diagnosis for orchestrators that must combine autonomous execution with coherent governance:

- System 1 maps to operational agents, worker pools, tool-running units, product workflows, or subteams that directly do work.
- System 2 maps to coordination protocols, shared queues, locks, leases, schemas, rate limits, and conflict-resolution mechanisms.
- System 3 maps to internal control over current commitments, resources, budgets, risk, dependencies, and whole-system optimization.
- System 3* maps to selective audits: trace sampling, evaluator spot checks, security reviews, budget checks, and direct inspection of tool outcomes.
- System 4 maps to future-facing intelligence: external scanning, experiments, model/tool evaluations, simulations, and roadmap adaptation.
- System 5 maps to policy identity: mission, values, safety boundaries, escalation rules, final authority, and tradeoff doctrine.
- Recursion means each operational agent team may itself need a smaller viable-system design.

## Distillation Choices

The skill emphasizes executable design steps for auto-orchestrator architecture rather than VSM history. It translates the source's autonomy, metasystem, outside/inside, policy, and real-time information-flow ideas into checks an agent can use while designing or auditing orchestration systems.

## Sources Consulted

- Local assigned source file listed above.
- Stafford Beer, `Brain of the Firm`.
- Stafford Beer, `The Heart of Enterprise`.
- Stafford Beer, `Diagnosing the System for Organizations`.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Stafford Beer viable system sources and local VSM entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Systems 1-5: operations, coordination, control, intelligence, policy; viability comes from recursive organization.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use VSM as an org chart; it diagnoses missing functions and overloaded channels.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: A system survives by balancing present operations with future adaptation and identity-level policy.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Map operational units, coordination channels, control/accountability, environmental scanning, and policy identity; then test recursion at each organizational layer.
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
