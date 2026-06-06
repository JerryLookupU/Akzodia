---
name: 03-systems-engineering
description: Use when designing or repairing an auto-orchestrator that must turn ambiguous stakeholder goals into traceable requirements, component responsibilities, interfaces, verification evidence, validation scenarios, lifecycle gates, and risk-informed tradeoffs across many agents/tools.
source_files:
  - references/source-notes.md
---
# 03 Systems Engineering

## Book-Derived Essence

- Core framework: Need -> requirements -> functions -> interfaces -> verification -> validation -> transition. Keep traceability alive across the lifecycle.
- Deep idea: The unique insight is that complex work fails at interfaces and lifecycle transitions, not only inside components. Requirements are not a list; they are a contract that must survive design, integration, evidence, and handoff.
- Discovery method: Walk a stakeholder expectation forward into functions, interfaces, verification evidence, validation scenarios, risk owners, and transition criteria. Gaps in that trace are the defects.
- Boundary: Do not use full systems engineering for one-off execution where lifecycle, integration, or stakeholder traceability is not at risk.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestration problem is not just "pick the next tool" but "make a whole system behave correctly over time." Typical triggers:

- A user goal spans multiple agents, tools, data stores, handoffs, approvals, or operating phases.
- Requirements are vague, conflicting, or likely to drift as execution reveals new constraints.
- The orchestrator needs traceability from stakeholder intent to tasks, interfaces, evidence, and acceptance.
- You need to decide where to place boundaries between planner, executor, verifier, memory, policy, budget, and human review components.
- You are debugging orchestration failures caused by interface mismatch, missing validation, weak risk handling, unowned configuration, or late discovery of bad assumptions.

## Standalone Contract

This skill is self-contained. Use the workflow below to produce systems-engineering structure for an orchestration problem without reading the original source files.

Runtime dependency rule: do not load or depend on external files, webpages, original books, source reports, source snapshots, external source folders, or files outside this skill directory. Use `SKILL.md` as the executable contract; any local `references/`, `assets/`, or `examples/` are optional provenance/support only.

The skill should convert ambiguous stakeholder intent into traceable requirements, operational scenarios, functional decomposition, interfaces, risk-informed alternatives, verification evidence, validation scenarios, lifecycle gates, and transition criteria.

## Activation and Execution Gate

Activate only when the request has enough coupling, risk, lifecycle span, or stakeholder ambiguity to justify systems-engineering formality. Do not activate for simple tool selection, a small obvious implementation, or a glossary-style explanation.

Before running the workflow, identify the system-of-interest, mission need, lifecycle phase, and at least one stakeholder expectation. If any are missing, ask one focused clarification or declare a lightweight provisional pass with assumptions.

## Workflow

1. Define the system-of-interest and lifecycle.
   - Name the orchestrator boundary: what is inside, what is an external dependency, and what must be treated as environment.
   - Identify lifecycle phases for the work: concept, architecture, task decomposition, execution, integration, verification, validation, transition, operations, and closeout.
   - State the mission need in plain language before writing any task plan.

2. Convert stakeholder expectations into an operational concept.
   - Identify stakeholders: end user, system owner, downstream operators, policy/security owner, cost/budget owner, and affected services.
   - Write 3-7 operating scenarios, including off-nominal scenarios such as missing data, tool denial, budget exhaustion, unsafe request, stale memory, conflicting subagent results, and partial completion.
   - Define measures of effectiveness: what "useful orchestration" means from the user's perspective.

3. Derive technical requirements with traceability.
   - Transform expectations into measurable "shall" requirements for orchestration behavior.
   - For each requirement, record rationale, owner, lifecycle phase, verification method, and linked scenario.
   - Separate stakeholder validation criteria from internal verification criteria. Verification asks whether the orchestrator met the specified requirement; validation asks whether the orchestrator solved the intended user problem in the intended context.

4. Decompose by function, behavior, time, and interface.
   - Break the orchestrator into logical functions before assigning implementation components: intake, clarification, planning, delegation, tool policy, execution monitoring, integration, verification, reporting, memory/configuration, and recovery.
   - Allocate requirements to functions and identify derived requirements created by decomposition.
   - For every handoff, define interface contracts: inputs, outputs, authority, error semantics, timing, state ownership, and escalation path.

5. Generate alternatives and make risk-informed tradeoffs.
   - Produce at least two viable architectures or operating policies when the decision affects correctness, cost, schedule, safety, or maintainability.
   - Compare alternatives against effectiveness, cost, schedule, technical risk, policy risk, and human burden.
   - Make tradeoffs explicit. Lower cost may require accepting more risk or reducing performance; lower risk may require more cost, time, or scope reduction.

6. Realize bottom-up and integrate deliberately.
   - Implement, buy, reuse, or delegate the lowest-level functions only after their requirements and interfaces are clear enough.
   - Integrate from lower-level products upward: subagent output schemas, tool outputs, task state, evidence bundles, then user-facing orchestration result.
   - Run interface checks before end-to-end checks so integration failures are localized.

7. Verify, validate, and transition.
   - Verification evidence should map requirement-by-requirement using test, analysis, inspection, demonstration, or a combination.
   - Validation should replay the operational scenarios with realistic users, data, policies, budgets, and failure modes.
   - Transition only when the receiving user/system has the result, evidence, known limitations, configuration state, and any required follow-up actions.

8. Run crosscutting technical management continuously.
   - Maintain a technical plan, requirements trace, interface register, risk register, configuration baseline, technical data/evidence store, progress assessment, and decision log.
   - Tailor formality to system size and risk. A single-session orchestration may need compact tables; a persistent multi-agent runtime needs explicit baselines, reviews, and change control.
   - Re-enter the workflow when new capabilities, new constraints, or operational anomalies change the system.

## Output Format

Return a systems-engineering brief with:

- `System-of-interest`: boundary, environment, lifecycle phase, mission need.
- `Operational concept`: stakeholders, nominal scenarios, off-nominal scenarios, measures of effectiveness.
- `Requirements trace`: requirement, rationale, owner, phase, verification method, linked scenario.
- `Functional decomposition`: functions, allocated requirements, derived requirements.
- `Interfaces`: inputs, outputs, authority, timing, state ownership, error semantics, escalation.
- `Tradeoffs and risks`: alternatives, decision criteria, accepted risks, mitigations.
- `V&V and transition`: verification evidence, validation scenarios, readiness criteria, known limitations.

## Failure Modes

- Treating decomposition as a task list without preserving the stakeholder expectation each task serves.
- Verifying "all subtasks completed" while failing to validate that the user's real operating scenario was solved.
- Discovering interface contracts only during integration, causing schema drift, duplicated work, or unowned state.
- Optimizing one component, agent, or tool path at the expense of whole-system effectiveness.
- Deferring risk analysis until execution, when changes are more expensive and failures have already propagated.
- Ignoring human/system integration: approval flow, operator workload, handoff clarity, training, and situational awareness.
- Letting requirements, plans, prompts, tool policies, or memory mutate without configuration control.

## Failure, Recovery, and Idempotency

If requirements are vague, conflicting, or unstable, do not force a final baseline. Mark the pass as concept, preliminary, or baselined, and record what evidence is needed to advance. If integration fails, localize the failure to requirement, interface, configuration, evidence, or validation mismatch before changing architecture.

On re-run, preserve requirement IDs, interface names, risk IDs, and decision records unless explicitly superseded. Report added, changed, retired, and still-open items so repeated execution behaves like controlled revision, not a fresh unrelated plan.

## Hard Rules

- Do not equate task completion with stakeholder validation.
- Do not allocate work to agents or tools before functions, requirements, and interfaces are clear enough.
- Do not hide configuration, requirement, or interface changes; record them as changes with rationale.
- Do not impose heavyweight documentation when a lightweight pass satisfies the risk, but keep intent, interfaces, evidence, and decisions traceable.

## Boundaries

- This skill is for complex orchestrator/system design, not for simple one-step tool selection or ordinary task prioritization.
- It does not replace domain-specific safety, security, legal, medical, financial, or compliance review; it helps expose where those reviews must attach.
- It should be tailored. Do not impose NASA-scale documentation on a low-risk local task, but do preserve intent, interfaces, evidence, and decisions.
- It assumes enough uncertainty or coupling to justify systems thinking. If the problem has a stable, obvious implementation path, use a lighter engineering workflow.

## Source Closure

This 03-systems-engineering skill is self-contained for runtime use; its source basis is Systems engineering source notes and local theory-pack entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
