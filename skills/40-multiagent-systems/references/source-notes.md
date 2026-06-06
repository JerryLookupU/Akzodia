# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Source

- Michael Wooldridge, `An Introduction to MultiAgent Systems`, Second Edition, Wiley, 2009.
- Yoav Shoham and Kevin Leyton-Brown, `Multiagent Systems: Algorithmic, Game-Theoretic, and Logical Foundations`, Cambridge University Press, 2009/2010, Revision 1.1 manuscript.
- Local source files:

## Distillation

The sources frame multiagent systems as systems containing multiple autonomous entities with diverging information, diverging interests, or both. For auto-orchestrator design, the useful transfer is not "many services" but "many decision makers": components choose local actions under local observations, and group behavior depends on interaction protocols.

Shoham and Leyton-Brown organize the field around coordination, competition, algorithms, game theory, and logic. That structure maps to orchestrator design choices:

- Cooperative distributed problem solving when agents share a global goal but no central controller or complete global view is feasible.
- Distributed constraint satisfaction when each agent owns a local variable and must communicate with neighbors to satisfy global constraints.
- Distributed optimization when the system needs not just feasibility but a best feasible assignment under shared or local objectives.
- Game-theoretic reasoning when agents have distinct preferences, private information, or strategic incentives.
- Communication, social choice, mechanism design, auctions, and coalitions when group protocols must elicit information, allocate resources, or aggregate preferences.

## Key Transfer Patterns

Distributed CSP is the clearest engineering pattern for cooperative orchestration with local ownership. Each agent owns a variable or assignment, communicates with constrained neighbors, tracks a local view, and sends conflict evidence when an assignment cannot work. The asynchronous backtracking pattern adds a priority order, `ok` messages carrying assignments, and `nogood` messages carrying inconsistent partial assignments. For orchestrators, this becomes a design for specialist agents negotiating task ownership, resource allocation, or compatibility constraints without a full central search.

Distributed optimization extends this from "find a feasible assignment" to "optimize a global objective." The source examples include distributed dynamic programming, distributed MDP action selection, auction-like optimization, and social laws. For orchestrators, the practical choice is whether to solve centrally then delegate, let local agents improve assignments through messages, or use market-like bidding to allocate scarce capabilities.

Game theory enters when agents are not perfectly aligned. The source emphasizes self-interested agents, rationalizability, equilibria, correlated signals, congestion games, social choice, mechanism design, auctions, and coalitions. The engineering lesson is that a multiagent protocol must state what agents know, what they prefer, what they can misreport, and why following the protocol is stable enough for the task.

## Auto-Orchestrator Implications

Use multiagent systems theory to design the interaction layer between planners, executors, verifiers, reviewers, retrievers, and tool specialists. The central design questions are:

- What does each agent decide locally?
- What information is private, stale, expensive, or unreliable?
- Are incentives cooperative, competitive, mixed, or unknown?
- Which protocol coordinates local decisions into a global outcome?
- What prevents cycling, deadlock, manipulation, duplicate work, or unbounded communication?
- What evidence explains the final group decision or failure?

The skill deliberately keeps mathematical solution concepts lightweight. In implementation work, protocol contracts, convergence rules, incentives, and failure evidence are usually more valuable than proving a full equilibrium unless the user explicitly asks for formal analysis.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Multiagent systems sources and local MAS entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Autonomous agents interact through protocols, incentives, coordination mechanisms, and local knowledge.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use MAS when one centralized controller has full authority and no meaningful autonomous participants.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The central issue is emergence from local decisions. Global behavior must be shaped through protocol, incentives, and constraints, not assumed.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Identify agent goals, information, action sets, message protocol, conflict points, coalition/competition structure, and convergence or failure modes.
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
