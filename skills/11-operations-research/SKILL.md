---
name: 11-operations-research
description: Use when designing or auditing an auto-orchestrator that must optimize choices under constraints: allocating agents/tools/budget, routing work, scheduling queued jobs, selecting portfolios of actions, trading off cost/latency/success probability/risk, or turning workflow decisions into variables, objectives, constraints, and sensitivity checks.
source_files:
  - references/source-notes.md
---
# 11 Operations Research

## Book-Derived Essence

- Core framework: Decision variables + objective + constraints + solver/heuristic + sensitivity. Turn choices into an explicit optimi

zation model.
- Deep idea: OR forces preference and scarcity into the open. The insight is not to “optimize everything,” but to reveal which constraint or objective actually drives the policy.
- Discovery method: List decisions, measurable objective, hard constraints, soft penalties, resource limits, and alternative feasible policies; then test shadow prices or sensitivity to changed assumptions.
- Boundary: Do not use OR when values, constraints, or decision variables cannot be stated without pretending precision.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestration problem is a constrained decision problem, not just a decomposition problem.

Strong triggers:
- Multiple feasible actions, agents, tools, routes, retries, schedules, or resource allocations compete for limited capacity.
- The user asks to optimize cost, latency, throughput, quality, success rate, risk, budget, token spend, queue time, SLA compliance, or utilization.
- Workflow correctness depends on capacities, time windows, precedence, mutually exclusive choices, quotas, inventory, batching, routing, or service queues.
- A planner needs a defensible policy for selecting among alternatives rather than ad hoc ranking.
- The orchestrator should expose tradeoffs and sensitivity: what changes if a budget, deadline, failure rate, or resource capacity shifts?

Prefer simpler planning or HTN when the main issue is task decomposition, preconditions, or action semantics. Use Operations Research when the core question is "which feasible choice is best under constraints?"

## Standalone Contract

This skill is self-contained for turning orchestration choices into variables, objectives, constraints, and executable allocation policies. `references/source-notes.md` is provenance only.

Runtime dependency rule: do not open or depend on external files, webpages, original books, source reports, source snapshots, external source folders, or files outside this skill directory. Use `SKILL.md` as the executable contract; local `references/`, `assets/`, or `examples/` may be used only when present and only as optional in-skill support.

Activation gate: use this skill only when multiple feasible choices compete under scarce capacity, budgets, quotas, deadlines, service levels, risk limits, or explicit tradeoffs. Do not activate for pure decomposition, a glossary explanation, or a linear runbook with no alternatives or resource constraints.

Execution gate: before optimizing, identify the decision owner, controllable choices, hard constraints, objective policy, input estimates, and planning horizon. If tradeoff weights or priorities are missing, surface the missing objective policy before ranking alternatives.

## Workflow

1. State the decision frame.
   - Name the operational decision: assign agents, route tasks, schedule work, choose tools, size a queue, allocate budget, select retries, batch jobs, or reserve capacity.
   - Identify the decision owner, planning horizon, replanning cadence, and whether the decision is one-shot, rolling, or continuous.
   - Separate hard requirements from preferences. Hard requirements become constraints; preferences usually become objective terms.

2. Define decision variables.
   - Use binary variables for yes/no choices: choose tool, launch subagent, include task, retry branch, open escalation.
   - Use integer variables for counts: number of workers, retries, batches, parallel calls, reserved slots.
   - Use continuous variables for divisible quantities: budget share, token share, time allowance, traffic fraction.
   - If a variable cannot be observed or controlled by the orchestrator, replace it with a measured parameter or remove it.

3. Build the objective.
   - Choose the primary objective explicitly: minimize cost, minimize makespan, maximize expected value, maximize completed work, minimize risk, or balance utilization.
   - For multiple goals, use one of these patterns:
     - Weighted score when tradeoff weights are accepted and stable.
     - Lexicographic priority when one requirement dominates, such as safety before speed.
     - Constraint plus optimization when a metric has a minimum acceptable level, such as quality >= threshold, then minimize cost.
   - Keep units visible. Do not add dollars, minutes, risk scores, and success probability without normalization or a stated weighting rule.

4. Encode constraints.
   - Capacity: agents, API quotas, tokens, budget, locks, compute, reviewer attention, or rate limits.
   - Precedence: task A must finish before task B, or a verification step must precede an irreversible action.
   - Assignment: each task gets exactly one owner/tool, at most one branch executes, or a required role must be covered.
   - Time: deadlines, maintenance windows, queue service time, retry delay, cooldowns, or parallelism limits.
   - Risk and policy: approval gates, data boundaries, unsafe action exclusions, rollback availability, or maximum blast radius.
   - Conservation/flow: work enters, moves through states, and exits; no task should disappear or be double-counted.

5. Choose the OR model family.
   - Linear or integer programming: assignment, portfolio selection, capacity allocation, batching, scheduling with clear constraints.
   - Network flow or shortest path: routing tasks across tools, environments, review stages, data pipelines, or dependency paths.
   - Queuing model: arrival rates, service rates, backlog, wait time, concurrency, escalation thresholds, and SLA risk.
   - Inventory or reserve model: cached artifacts, warm workers, budget buffers, token reserves, fallback capacity, or retry stock.
   - Simulation: nonlinear, uncertain, or high-variance workflows where formulas are brittle but policy comparison is still possible.
   - Heuristic or greedy rule: use only when exact optimization is unnecessary, too expensive, or blocked by uncertain inputs; document the approximation.

6. Solve at the right fidelity.
   - Start with a small hand-checkable model before adding detail.
   - Validate dimensions, bounds, and constraint direction before trusting the result.
   - If exact solving is unavailable, produce a ranked feasible policy with the objective, violated alternatives, and known approximation risk.
   - Prefer robust decisions when parameter estimates are weak: leave slack, cap exposure, and avoid plans that only work at a single optimistic point.

7. Translate the result into orchestration rules.
   - Convert variable values into executable policies: who does what, when, with which tool, under what quota, and when to replan.
   - Add monitoring metrics tied to model assumptions: queue length, service time, failure rate, budget burn, utilization, SLA misses.
   - Add reoptimization triggers: backlog above threshold, capacity loss, new deadline, failure-rate shift, quota exhaustion, or objective-weight change.
   - Report shadow tradeoffs in plain language: which constraint is binding, which resource is scarce, and which extra capacity would matter most.

## Failure Modes

- Optimizing before defining feasibility. A low-cost plan that violates capacity, approval, or safety constraints is not a plan.
- Hiding value judgments inside arbitrary weights. If weights drive the answer, surface them and test sensitivity.
- Mixing incompatible units in one score without normalization.
- Treating uncertain estimates as facts. Use ranges, scenarios, simulation, slack, or robust constraints.
- Over-modeling a small decision that a direct rule can handle faster and more transparently.
- Under-modeling queues. High utilization can create long waits even when average capacity appears sufficient.
- Ignoring integer effects: one half-agent, partial approval, or fractional tool call may be mathematically convenient but operationally impossible.
- Returning a solver answer without translating it into executable orchestrator policy and monitoring triggers.
- Freezing the model after execution starts. OR policies need replanning when arrivals, service rates, constraints, or objectives change.

## Output Format

Return an OR decision artifact with:

- `Decision Frame`: owner, horizon, cadence, choices, hard requirements, and preferences.
- `Variables And Parameters`: controllable variables, measured inputs, bounds, and units.
- `Objective`: primary metric, multi-objective policy, normalization or priority rule.
- `Constraints`: capacity, precedence, assignment, time, risk/policy, and flow conservation.
- `Model Family And Solve Approach`: exact model, simulation, robust scenario, or documented heuristic.
- `Policy Translation`: executable routing/allocation/scheduling rule, monitoring metrics, reoptimization triggers, and sensitivity notes.

## Failure, Recovery, And Idempotency

If no feasible solution exists, report the conflicting constraints and the smallest relaxations or added capacity that would restore feasibility. If inputs are uncertain, use ranges, scenarios, slack, or simulation rather than treating estimates as facts.

Repeated runs should preserve the same decision-variable meanings and only change bounds, parameters, objectives, or constraints with an explicit reason. Reoptimization should be triggered by observed changes such as backlog, quota, failure rate, budget burn, or objective-policy change.

## Hard Rules

- Feasibility comes before objective improvement.
- Do not mix incompatible units in one score without normalization or a stated weighting rule.
- Do not hide value judgments inside arbitrary weights; expose and test them.
- Do not return a solver-style answer without translating it into executable orchestration policy and monitoring triggers.

## Boundaries

Operations Research improves choice under explicit objectives and constraints. It does not discover user intent, invent authority, or replace safety policy. Ambiguous goals, permissions, and unacceptable risks must be clarified or encoded as hard gates before optimization.

This skill complements planning and decomposition work, but it does not require another skill at runtime. If the main unsolved issue is state-changing action semantics or decomposition, perform that modeling as a separate upstream pass; use this skill only to allocate scarce resources and choose the best feasible branch among alternatives.

Do not force mathematical programming when inputs are unmeasured, the stakes are low, or the result would be less explainable than a simple policy. In those cases, use a transparent heuristic and define the evidence that would justify a richer OR model later.

## Source Closure

This 11-operations-research skill is self-contained for runtime use; its source basis is Operations Research sources and local OR entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
