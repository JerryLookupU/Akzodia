---
name: 38-viable-system-model
description: >-
  Use when designing, diagnosing, or restructuring an auto-orchestrator as a viable recursive system: autonomous operational agent units, coordination to prevent interference, internal control and audit, future-facing adaptation, and policy identity. Trigger for Stafford Beer VSM, viable system model, metasystem design, recursive organization, agent-team governance, S1-S5 mapping, balancing autonomy with coherence, or diagnosing orchestration structures that fragment, over-centralize, miss environmental change, or lack policy closure.
source_files:
  - references/source-notes.md
---
# 38 Viable System Model

## Book-Derived Essence

- Core framework: Systems 1-5: operations, coordination, control, intelligence, policy; viability comes from recursive organi

zation.
- Deep idea: A system survives by balancing present operations with future adaptation and identity-level policy.
- Discovery method: Map operational units, coordination channels, control/accountability, environmental scanning, and policy identity; then test recursion at each organizational layer.
- Boundary: Do not use VSM as an org chart; it diagnoses missing functions and overloaded channels.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestrator must remain coherent and adaptive while delegating real autonomy:

- You need to map an agent runtime, tool system, product workflow, or organization into VSM Systems 1 through 5.
- Operational agent teams need autonomy but currently conflict, duplicate work, starve shared resources, or require too much central intervention.
- The system has coordination mechanisms, audits, planning functions, or policies, but they are not assigned to clear metasystem roles.
- The runtime must handle multiple recursive levels: one orchestrator managing agent teams, each team managing tools, subagents, queues, or local plans.
- You need to diagnose whether failure comes from weak operations, missing coordination, brittle internal control, poor environmental sensing, or unclear policy identity.
- You are designing governance for an auto-orchestrator and need to preserve local responsiveness without losing whole-system alignment.

## Non-Triggers

- Do not trigger for simple org-chart labeling, generic cybernetics history, or management summaries that do not redesign an orchestrator.
- Do not trigger for a closed-loop self-healing controller where MAPE-K is the more direct frame.
- Do not trigger for message formats, auctions, voting, or negotiation unless the request is about metasystem viability and policy closure.
- Do not trigger for ordinary task decomposition, WBS, DSM, or dependency mapping without autonomy/coherence/adaptation concerns.

## Standalone Runtime Contract

This SKILL.md contains the full runtime procedure. Do not read external webpages, original books, source reports, external source snapshots, distilled source material, or files outside this skill directory to execute the skill. `references/source-notes.md` is provenance-only: use it only when the user explicitly asks to audit source lineage, not as an execution dependency.

## Activation And Execution Gate

Before applying this skill, state the activation decision in one sentence. Proceed only if all gate conditions are true:

- A system boundary and at least one recursion level can be named.
- The design problem involves operational autonomy plus whole-system coherence, not just central task assignment.
- The request needs at least two VSM functions among operations, coordination, internal control/audit, future adaptation, and policy identity.

If a gate condition is missing, ask up to three targeted questions or recommend a simpler organizational, policy, MAPE-K, or multiagent-protocol approach.

## Workflow

1. Set the viable-system boundary and recursion level.
   - Name the system whose viability you are designing: one orchestrator, a multi-agent workspace, a product automation group, or a larger organization.
   - Define its environment: users, upstream systems, downstream tools, model providers, policies, markets, incident streams, compliance constraints, and competing priorities.
   - Choose the current recursion level. Treat each System 1 unit as a viable system in its own right when it has its own goals, environment, coordination, control, intelligence, and policy.

2. Identify System 1 operational units.
   - List the autonomous units that directly create value or execute work: planner agents, research agents, coding agents, QA agents, tool runners, deployment workers, data pipelines, customer workflows, or product squads.
   - For each unit, write its local mission, inputs, outputs, authority, local environment, decision rights, success metrics, and escalation paths.
   - Preserve local autonomy by default. Centralize only the constraints required for coherence, safety, shared resources, or cross-unit commitments.

3. Design System 2 coordination.
   - Add mechanisms that dampen conflict between System 1 units: shared protocols, queues, locks, leases, budgets, naming conventions, state schemas, handoff contracts, rate limits, and conflict-resolution rules.
   - Look for oscillation and interference: agents retrying the same tool, duplicate subtasks, policy races, incompatible memory writes, or competing fixes to the same resource.
   - Keep System 2 lightweight. It should harmonize interactions, not become a hidden command layer that removes System 1 autonomy.

4. Design System 3 internal control and synergy.
   - Define the inside-and-now management view: current capacity, commitments, constraints, risks, costs, tool health, queue pressure, task progress, and cross-unit dependencies.
   - Give System 3 authority to allocate resources, set internal priorities, enforce operating constraints, rebalance work, and create synergy between operational units.
   - Add System 3* audit channels for direct, selective verification of operational reality: trace sampling, evaluator spot checks, tool-result inspection, budget audits, security checks, and incident reviews.
   - Prevent System 3 from relying only on self-reports from System 1; audits should detect drift, gaming, blind spots, and unreported degradation.

5. Design System 4 intelligence and adaptation.
   - Define the outside-and-then function: scanning external change, emerging user needs, model/provider shifts, policy changes, new tools, competitive pressure, incidents, and long-horizon risks.
   - Give System 4 methods for experiments, simulations, scenario planning, roadmap proposals, model evaluations, dependency reviews, and future capability design.
   - Require System 4 proposals to interact with System 3 so future plans are grounded in current operating capability.

6. Design System 5 policy, identity, and closure.
   - State the system identity: what the orchestrator is for, what it must never do, whose goals it serves, and what values or policies override local optimization.
   - Encode closure through policy, not constant command: safety rules, budget doctrine, quality thresholds, privacy boundaries, approval rules, escalation principles, and acceptable risk.
   - Use System 5 to resolve unresolved tensions between System 3's inside-now view and System 4's outside-future view.

7. Check the information channels and requisite variety.
   - Verify that each subsystem receives information at the granularity and cadence needed for its role.
   - Add sensors, summaries, dashboards, event streams, memory indexes, or decision records where a subsystem is blind.
   - Add filters, abstractions, thresholds, policies, or delegation where a subsystem is overloaded by raw variety.
   - Confirm that real-time operational information can flow across System 1, System 2, System 3, System 4, System 5, and the environment without bypassing authority boundaries.

8. Diagnose and redesign.
   - Missing System 1: no accountable operational unit owns the actual work.
   - Missing System 2: autonomous units conflict, duplicate, deadlock, or require manual mediation.
   - Missing System 3: the whole cannot optimize across units or enforce internal constraints.
   - Missing System 3*: management believes reports that do not match operational reality.
   - Missing System 4: the system performs today's work but fails to adapt to future environmental change.
   - Missing System 5: policies, identity, and final authority are ambiguous, causing fragmentation or arbitrary escalation.
   - Overgrown metasystem: central management suppresses local response and creates bottlenecks.
   - For each diagnosis, propose the smallest structural change that restores viability at the current recursion level.

## Failure Modes

- Treating VSM as an org chart instead of a functional diagnosis of viability, autonomy, control, adaptation, and policy closure.
- Naming Systems 1 through 5 without specifying authority, information flow, decision rights, and feedback channels.
- Collapsing System 2 coordination and System 3 control into one overloaded manager.
- Over-centralizing decisions that System 1 units need to make quickly in their local environments.
- Building strong inside-now control while neglecting System 4 intelligence about outside-future change.
- Letting System 4 strategy drift away from System 3 operational reality.
- Defining policies as slogans without executable constraints, escalation rules, or override authority.
- Ignoring recursion: designing only the top orchestrator while subteams or worker agents lack their own viable structure.
- Using audit channels as constant surveillance that destroys trust and autonomy instead of selective reality checks.

## Output Format And Deliverables

Return the design or diagnosis in this order unless the user requests another format:

1. Activation decision, system boundary, environment, and recursion level.
2. System 1 through System 5 map with owner, authority, information inputs, outputs, and decision rights.
3. Variety and channel diagnosis: blind spots, overload, bypasses, missing filters, and feedback cadence.
4. Viability gaps ranked by impact, with the smallest structural change for each.
5. Recovery plan, validation checks, and remaining risks.

## Failure, Recovery, And Idempotency

- Treat VSM changes as governance/design recommendations until the user explicitly asks for implementation.
- Preserve local autonomy by default; repeated runs should refine the same recursion map rather than create duplicate metasystems.
- If boundary, environment, or recursion level is unclear, stop and clarify before assigning Systems 1 through 5.
- If current evidence is only self-report, mark diagnoses provisional and add System 3* audit checks before redesigning authority.
- On partial redesign, keep old authority paths visible until replacement channels, escalation rules, and policy closure are defined.

## Boundaries

- This skill is for auto-orchestrator design, diagnosis, and restructuring using Stafford Beer's Viable System Model; it is not a generic summary of management cybernetics.
- Use MAPE-K when the main task is a closed-loop autonomic controller with Monitor, Analyze, Plan, Execute, and Knowledge functions.
- Use requisite variety when the main issue is matching regulator capacity to environmental complexity rather than mapping the full metasystem.
- Use multiagent-systems patterns when the core challenge is agent communication protocols, negotiation, or distributed consensus without a metasystem diagnosis.
- Use WBS, DSM, or dependency mapping when the request is primarily task decomposition or dependency structure rather than organizational viability.
- Do not apply VSM to force every small workflow into five named roles; use it when autonomy, coordination, control, adaptation, and policy identity all matter.

## Hard Rules

- Do not label a component as System 1 through 5 without naming its authority, information inputs, outputs, and feedback channels.
- Do not centralize decisions that local System 1 units must make quickly unless a safety, coherence, resource, or policy constraint requires it.
- System 3 control must not rely only on System 1 self-reports; include selective System 3* reality checks for consequential claims.
- System 5 policy must be executable as constraints, escalation rules, or override authority, not slogans.
- Provenance files are not runtime inputs. `references/source-notes.md` may only be cited as source trace when provenance is requested.

## Source Closure

This 38-viable-system-model skill is self-contained for runtime use; its source basis is Stafford Beer viable system sources and local VSM entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
