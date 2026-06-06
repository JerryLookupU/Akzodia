---
name: 10-hierarchical-task-network-planning
description: Use when designing or repairing an auto-orchestrator that must decompose high-level goals into reusable task methods, choose among alternative procedures, preserve execution-order state, plan around preconditions/effects, interleave partially ordered subtasks, or control backtracking with domain heuristics.
---

# Hierarchical Task Network Planning

## When To Use

Use this skill when the orchestration problem is best modeled as "how should this task be performed?" rather than "what flat list of actions reaches a goal?"

Strong triggers:
- A high-level objective has known operating procedures, playbooks, recipes, runbooks, or policy-specific decompositions.
- The orchestrator must choose among alternative methods for the same task based on current state, constraints, cost, risk, tool availability, or user preferences.
- A workflow has both abstract tasks, such as "ship release" or "triage incident", and primitive actions, such as "run test command" or "open ticket".
- Correctness depends on preconditions and effects: a step reserves a resource, changes a file, consumes budget, updates state, or invalidates another branch.
- Some subtasks must be ordered, while others can interleave or run in parallel under explicit constraints.
- The plan needs traceable decomposition, bounded backtracking, or branch ranking rather than opaque agent improvisation.

Prefer a simple checklist when the task is small, linear, and has no meaningful alternative decompositions.

## Workflow

1. Define the HTN planning frame.
   - State the initial world state: known facts, available agents/tools, file state, budgets, approvals, deadlines, locks, and constraints.
   - Replace a vague goal with an initial task network: one or more tasks to accomplish, plus any ordering constraints.
   - Separate task success from plan quality. First require a valid plan; then optimize for time, cost, risk, or user value.

2. Classify tasks.
   - Mark primitive tasks as actions the orchestrator can directly execute or delegate: commands, API calls, edits, reviews, messages, tests, deployments.
   - Mark compound tasks as activities that need decomposition: investigate bug, implement feature, migrate data, produce report, recover service.
   - For every primitive task, write its preconditions, effects, failure signal, and verification evidence.
   - For every compound task, write the expected output and the state facts it is allowed to depend on.

3. Encode methods as operating procedures.
   - For each compound task, define one or more methods: `task -> precondition -> subtasks`.
   - Make methods domain-specific enough to guide search. A method should capture a real procedure, not merely restate the task name.
   - Include ordered subtasks where state must be checked immediately before execution.
   - Include unordered or partially ordered subtasks where work can interleave without corrupting shared state.
   - Add explicit no-op methods for already-satisfied tasks, such as "if dependency is already installed, do nothing".

4. Plan forward in execution order.
   - Always evaluate a method or operator precondition against the current state that would exist at that point in the plan.
   - After a primitive action, update state facts immediately: files changed, resources reserved, tests passed, locks held, budget spent, artifact produced.
   - When a method decomposes into subtasks, continue down the leftmost executable branch far enough that preconditions are checked in the right state.
   - Use state flags for resource protection, such as `ticket-open`, `migration-lock-held`, `test-env-reserved`, or `user-approval-required`.

5. Control branching deliberately.
   - List all applicable methods and variable bindings at each compound task.
   - Rank alternatives with a local heuristic before search: cheapest, safest, highest evidence, least tool risk, most reversible, or fastest feedback.
   - If quality matters and time allows, keep the best valid plan found so far and continue branch-and-bound search until the time or budget limit.
   - When a branch fails, backtrack to the most recent method or binding choice; record the failed precondition so the planner does not retry blindly.

6. Handle partial order and interleaving.
   - Interleave subtasks only when their read/write effects do not conflict.
   - Use immediate adjacency when a check and action must remain coupled, such as verify lock then mutate resource.
   - For parallel agents, define shared-state contracts: which facts each agent may read, which facts it may write, and which writes require serialization.
   - If concurrency introduces temporal constraints, track per-resource read/write timestamps or a simpler equivalent lock/version model.

7. Produce the orchestration artifact.
   - Output the decomposition tree: root task, selected methods, primitive leaf actions, and ordering constraints.
   - Include the current-state assumptions used by each selected method.
   - Identify branch points not explored and the heuristic used to rank them.
   - State validation checkpoints, rollback points, and what evidence confirms each primitive action.

## Failure Modes

- Treating HTN as generic task breakdown. HTN requires methods with preconditions and subtasks, plus primitive operators with effects.
- Writing methods that are too abstract to reduce search, such as "solve problem -> solve subproblem".
- Evaluating preconditions against the initial state instead of the evolving execution state.
- Ignoring effects of primitive actions, causing resource reuse, stale assumptions, or unsafe interleaving.
- Overusing partial order. If subtasks share mutable state, force order, add locks, or create an immediate sequence.
- Letting backtracking become unbounded. Add branch ranking, time limits, failure memory, or a cheaper fallback method.
- Optimizing too early. A fast near-valid plan with clear repair points often beats exhaustive search under real orchestration budgets.
- Encoding every possible policy as a method. Use external functions or structured checks for computations better handled by tools.

## Boundaries

HTN planning is strongest when domain procedures are knowable and reusable. It is weaker for open-ended discovery where the useful tasks and methods are not yet known; run an exploration pass first, then convert findings into methods.

HTN methods express what parts of the search space should be explored. They are not a substitute for safety policy, formal verification, cost modeling, or human approval gates. Keep those as explicit preconditions, operators, or external checks.

Do not force HTN onto every workflow. For flat independent tasks, use a dependency graph or checklist. For hidden coupling, use a dependency-structure method first. For probabilistic choice under uncertainty, pair HTN with scoring, simulation, or evaluation loops.

When source state is volatile, plans must be treated as provisional. Insert recheck tasks before irreversible primitive actions and make stale-state failure an expected backtracking path.
