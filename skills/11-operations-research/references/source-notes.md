# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Local Sources

## Metadata

This entry represents the discipline of Operations Research rather than a single complete local book text.

Local metadata identifies representative commercial textbooks:
- Frederick S. Hillier and Gerald J. Lieberman, `Introduction to Operations Research`.
- Hamdy A. Taha, `Operations Research: An Introduction`.

The local metadata summarizes why this entry belongs in the auto-orchestrator theory set: Operations Research handles resource allocation, routing, constraints, optimization, inventory, and queues; for orchestration, it turns task coordination into explicit tradeoffs among cost, latency, success probability, and resource consumption.

## Supplemented Metadata

The provided Open Textbook Library cache is incomplete. It points to `operations-research-models-and-methods`, but the locally cached page says "Textbook not found" and then lists unrelated suggestions. Because the entry metadata already names representative commercial textbooks, I supplemented only public catalogue-level information:
- McGraw Hill page for Hillier/Lieberman describes `Introduction to Operations Research` as a classic operations research text with professional practice examples, organization, supporting software, business applications, and accessible mathematics.
- Pearson page title confirms Taha's `Operations Research: An Introduction` as a current representative catalogue item.

No long source text was copied. The skill uses the stable discipline-level OR modeling pattern rather than proprietary textbook content.

## Distilled Claims

- OR frames operational choices as variables, constraints, objectives, and policies.
- Resource allocation is central: limited agents, tools, budget, time, tokens, quotas, attention, or compute must be assigned among competing tasks.
- Optimization must preserve feasibility: capacity, precedence, assignment, time-window, flow, and policy constraints come before objective improvement.
- Different OR model families fit different orchestrator problems: linear/integer programming for allocation and assignment, network models for routing and flow, queuing for backlog and service capacity, inventory/reserve models for buffers, and simulation for uncertain systems.
- Multi-objective decisions require explicit handling through weights, priority ordering, or constraints plus optimization.
- Sensitivity and reoptimization matter because real workflows change after execution starts.

## Auto-Orchestrator Translation

- Decision variable: a controllable orchestrator choice such as which subagent runs, which tool is selected, how much budget is allocated, or whether a retry branch is launched.
- Objective: the metric the orchestrator optimizes, such as cost, latency, expected value, completed work, risk, or SLA compliance.
- Constraint: a hard limit or rule such as budget, API quota, approval requirement, deadline, capacity, dependency, or safety boundary.
- Binding constraint: the scarce resource or rule currently limiting better performance.
- Queue: a stream of tasks competing for limited service capacity.
- Network flow: work moving through tools, agents, review gates, environments, or dependency paths.
- Sensitivity check: testing whether the chosen policy changes when estimates or constraints shift.

## Distillation Choices

- Converted textbook-level OR topics into an executable modeling workflow for auto-orchestrator design.
- Emphasized decision framing, constraints, objectives, model-family selection, translation to runtime policy, and reoptimization triggers.
- Avoided solver-specific syntax because the target use is orchestration design; an agent can later choose a concrete solver if the local codebase supports one.
- Recorded the incomplete local source and metadata supplementation in `audit.json`.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Operations Research sources and local OR entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Decision variables + objective + constraints + solver/heuristic + sensitivity. Turn choices into an explicit optimization model.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use OR when values, constraints, or decision variables cannot be stated without pretending precision.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: OR forces preference and scarcity into the open. The insight is not to “optimize everything,” but to reveal which constraint or objective actually drives the policy.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: List decisions, measurable objective, hard constraints, soft penalties, resource limits, and alternative feasible policies; then test shadow prices or sensitivity to changed assumptions.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

ze choices under constraints: allocating agents/tools/budget, routing work, scheduling queued jobs, selecting portfolios of actions, trading off cost/latency/success probability/risk, or turning workflow decisions into variables, objectives, constraints, and sensitivity checks.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
