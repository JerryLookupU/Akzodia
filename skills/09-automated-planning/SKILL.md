---
name: 09-automated-planning
description: Use when designing or auditing an auto-orchestrator that must convert goals, states, actions, constraints, observations, and execution feedback into adaptive plans. Trigger on requests to choose between task decomposition, state-space planning, hierarchical planning, temporal/resource planning, contingency planning, replanning, or learning-informed action policies for agent workflows.
source_files:
  - references/source-notes.md
---
# 09 Automated Planning

## Book-Derived Essence

- Core framework: State + goal + actions + preconditions + effects + search + execution feedback. Planning is choosing action sequences under observable change.
- Deep idea: The key distinction is between a plan as a search product and execution as a monitored loop. A plan that cannot sense violations is only a wish.
- Discovery method: Define state variables and goal tests, enumerate operators with preconditions/effects, choose decomposition/search style, then specify observation and replanning triggers.
- Boundary: Do not use automated planning for a static checklist with no state transition, alternative action, or replanning need.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestrator needs more than a static checklist:

- A goal must be achieved through actions whose preconditions, effects, ordering, or resources matter.
- The agent must decide what to do next from a current state, not merely follow a predetermined sequence.
- Actions can fail, reveal new facts, consume resources, or change the feasibility of later steps.
- The plan needs dependency reasoning, alternatives, partial ordering, time windows, costs, or safety constraints.
- A user asks for replanning, contingency handling, plan repair, task policy design, or integration of acting and learning.
- Multiple subagents/tools operate in an environment where execution state must be observed and fed back into planning.

Prefer this skill when the central question is "what action sequence or policy reaches the goal under these constraints?" Use WBS or ordinary task lists when scope decomposition is enough and action semantics do not matter.

## Standalone Contract

This skill is self-contained for designing or auditing an action planner for auto-orchestrators. `references/source-notes.md` is provenance only and is not required to execute the workflow.

Runtime dependency rule: do not open or depend on external files, webpages, original books, source reports, source snapshots, external source folders, or files outside this skill directory. Use `SKILL.md` as the executable contract; local `references/`, `assets/`, or `examples/` may be used only when present and only as optional in-skill support.

Activation gate: use this skill only when the request depends on goals, current state, actions, preconditions, effects, observations, constraints, contingencies, or replanning. Do not activate for pure deliverable breakdown, historical summaries, or short deterministic checklists where action semantics do not matter.

Execution gate: before planning, confirm the goal is testable, the current state or sensing step is defined, candidate actions have observable effects, and irreversible or externally visible actions have gates. If these are absent, add a sensing/clarification step before committing to execution.

## Workflow

1. Frame the planning problem.
   - Define the goal as verifiable target conditions, not vague intent.
   - Capture the current state: known facts, unknowns, resources, permissions, deadlines, environment assumptions, and active constraints.
   - Identify the planning horizon: one-shot plan, rolling plan, continuous controller, or policy for repeated decisions.
   - Decide whether the problem is deterministic, nondeterministic, probabilistic, partially observable, adversarial, or human-in-the-loop.

2. Model actions as operators.
   - For every candidate action/tool/subagent call, record its name, parameters, preconditions, effects, cost, duration, resource use, risks, observability, and failure signals.
   - Separate information-gathering actions from world-changing actions.
   - Mark irreversible, expensive, unsafe, or externally visible actions so the orchestrator can gate them.
   - Reject actions whose effects cannot be observed or verified unless the workflow can tolerate blind execution.

3. Select the planning shape.
   - Use forward state-space planning when current state is reliable and branching factor is manageable.
   - Use backward reasoning when goals are crisp and it is easier to work from required end conditions to supporting actions.
   - Use partial-order planning when independent subplans can be interleaved and premature sequencing would reduce flexibility.
   - Use hierarchical task network planning when the domain has reusable methods, recipes, or expert procedures.
   - Use temporal/resource planning when deadlines, concurrency, capacities, reservations, or cost tradeoffs dominate.
   - Use contingent or policy planning when observations during execution determine the next branch.

4. Generate a plan with explicit causal support.
   - For each step, state which goal or subgoal it supports.
   - Track causal links: which effects establish which later preconditions.
   - Expose threats: steps that could invalidate another step's preconditions or consume needed resources.
   - Keep independent steps unordered unless order is required by preconditions, resource conflicts, safety, or communication needs.
   - Prefer plans that preserve options when uncertainty is high.

5. Execute through a monitor-plan-act loop.
   - Before each action, check that its preconditions still hold.
   - After each action, update the state model from observations, logs, tool outputs, user messages, or environment telemetry.
   - Compare observed effects with expected effects; classify mismatch as harmless drift, recoverable failure, assumption break, or goal change.
   - Replan from the new state when a precondition fails, an effect is missing, a better route appears, or constraints change.
   - Escalate to the user only when no valid action remains, approval is required, or the goal/constraints are ambiguous.

6. Add learning feedback without letting it override contracts.
   - Record which actions worked, failed, or required repair under which state features.
   - Improve action models, method choices, cost estimates, and branch priorities from evidence.
   - Preserve hard constraints, safety gates, and user approvals even if learned heuristics suggest a shortcut.
   - Distinguish domain learning from incidental session memory; only durable patterns should update the orchestrator.

7. Audit the resulting orchestrator.
   - Verify every planned action has preconditions, effects, and an observation path.
   - Verify every goal condition has causal support.
   - Verify high-risk actions have gates and rollback or recovery paths.
   - Verify replanning triggers are concrete enough to run automatically.
   - Verify plan traces can explain why an action was chosen and what state change it was expected to cause.

## Failure Modes

- Checklist masquerading as planning: steps are ordered, but no state, preconditions, effects, or repair logic exists.
- Goal vagueness: the planner cannot test success, so it keeps expanding tasks instead of choosing actions.
- Unmodeled effects: an action changes files, resources, permissions, user state, or external systems in ways the planner did not account for.
- Premature total ordering: independent actions are forced into a sequence, reducing parallelism and adaptation.
- No sensing action: the plan depends on facts that are unknown but never observed.
- Stale-state execution: actions run from the original plan even after observations invalidate assumptions.
- Replanning thrash: every minor mismatch triggers full replanning because tolerances and repair scopes were not defined.
- Overfit learned policy: previous successes bias action choice even when the current constraints differ.
- Hidden resource conflict: subagents/tools consume shared budget, rate limits, locks, credentials, or user attention without arbitration.
- Unsafe autonomy: irreversible or externally visible actions lack approval, simulation, or rollback gates.

## Output Format

Return a plan or audit with:

- `Goal Conditions`: verifiable target state and unacceptable outcomes.
- `Current State`: known facts, unknowns, resources, permissions, and constraints.
- `Action Operators`: parameters, preconditions, effects, cost/duration, risks, observation path, and failure signals.
- `Plan Trace`: selected steps, causal links, threats, unordered steps, and resource conflicts.
- `Monitor-Plan-Act Loop`: pre-action checks, post-action observations, replanning triggers, and escalation gates.
- `Verification`: evidence that every goal condition and high-risk action is supported.

## Failure, Recovery, And Idempotency

If an expected effect is missing, classify the mismatch before replanning: harmless drift, recoverable failure, assumption break, or goal change. Replan from the latest observed state rather than replaying the original plan.

Repeated runs should preserve verified state facts and completed evidence, avoid re-running irreversible actions, and update action models only from durable evidence. If no valid action remains, report the blocked precondition, attempted alternatives, and required user decision.

## Hard Rules

- Do not execute from a stale plan after observations invalidate preconditions.
- Do not model risky actions without approval, rollback, simulation, or explicit recovery gates.
- Do not treat a numbered checklist as a plan unless actions include preconditions, effects, and observation paths.
- Do not let learned heuristics override user instructions, safety policies, or hard constraints.

## Boundaries

- Automated planning is not the same as project scheduling. Use scheduling once the action set and dependencies are clear.
- Automated planning is not a WBS. Use WBS to define deliverable scope; use planning to choose state-changing actions that achieve goals.
- Do not force a planner when a direct deterministic command or short checklist is sufficient.
- Classical planning assumptions break when state is partially observable, action outcomes are uncertain, or other actors change the environment; add sensing, contingencies, or replanning.
- Learned heuristics can prioritize search and improve models, but they do not replace explicit constraints, safety policies, or user instructions.
- If goals, permissions, or unacceptable risks are unclear, stop to clarify or design a guarded exploratory step rather than inventing authority.

## Source Closure

This 09-automated-planning skill is self-contained for runtime use; its source basis is Automated Planning sources and local planning-theory entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
