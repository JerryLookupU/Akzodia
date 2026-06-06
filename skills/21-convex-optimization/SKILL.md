---
name: 21-convex-optimization
description: Use when designing or auditing an auto-orchestrator that must choose resource allocations, worker/tool assignments, rate limits, SLA tradeoffs, budgets, retry quotas, batching levels, or scheduling policy weights under constraints that may be formulated as a convex optimization problem or convex relaxation.
source_files:
  - references/source-notes.md
---
# 21 Convex Optimization

## Book-Derived Essence

- Core framework: Convex objective + convex feasible set + duality + KKT/sensitivity. Convexity makes local evidence globally meaningful.
- Deep idea: The distinctive insight is certificates: a convex problem can often prove not just a good answer, but why no better feasible answer exists under the model.
- Discovery method: Define variables, objective, constraints, convexity assumptions, feasible region, dual variables, and sensitivity to weights or bounds.
- Boundary: Do not label a problem convex until variables, constraints, and objective preserve convexity.
- Source capsule: `references/source-notes.md#BDE-core-framework`

zation sources and local convex-optimization entry. Do not point users to original source files or source directories during normal use.

zation

## When To Use

Use this skill when orchestration design requires the best feasible allocation under explicit constraints, and the decision can plausibly be expressed with convex objectives, convex inequalities, and affine equalities.

Strong triggers:
- The orchestrator must allocate scarce workers, API quotas, browser sessions, GPUs, test environments, token budgets, money, or review capacity across competing tasks.
- The user asks for an optimal or near-optimal policy subject to SLA, budget, concurrency, fairness, risk, quality, deadline, or capacity constraints.
- A heuristic priority score is not enough; the design needs a clear objective, feasible set, solver-ready formulation, and tradeoff analysis.
- Multiple objectives compete, such as latency versus cost, throughput versus quality, urgency versus fairness, or exploration versus exploitation.
- A nonconvex scheduling, assignment, routing, or batching problem needs a convex relaxation to produce bounds, shadow prices, policy weights, or a tractable approximation.
- The user needs to interpret which constraint is binding, what extra quota is worth, or how objective value changes when a budget or SLA limit moves.

Prefer Scheduling Theory when all jobs are known and the main issue is ordering. Prefer Queueing Theory when dynamic arrivals and waiting dominate. Use Convex Optimization when the central work is constrained numerical allocation or tradeoff selection.

## Activation Gate

Activate only when the task needs constrained numerical allocation, policy weights, resource tradeoffs, a solver-ready formulation, convexity review, dual/tradeoff interpretation, or a convex relaxation for an orchestrator decision. Do not activate for pure job ordering, queueing-only waiting analysis, dashboard design, biographies, or exact discrete assignment unless the user asks for a relaxation or a nonconvexity diagnosis.

Before executing, identify the decision variables, objective direction, hard constraints, units/planning horizon, and whether the user wants formulation, audit, solution interpretation, or implementation policy. If convexity cannot be assessed from the prompt, state the missing functions/constraints and avoid claiming the model is convex.

## Standalone Contract

This skill must be usable from this `SKILL.md` alone. `references/source-notes.md` is provenance/source trace only; do not load it or any external source file for runtime execution. Mark all assumptions about convexity, solver class, data, and operational rounding explicitly.

## Output Format

Return a solver-oriented optimization brief with:
- Activation decision: why Convex Optimization is active and which nearby skills were ruled out.
- Formulation: decision vector, units, objective, constraints, domains, parameters, and solver class.
- Convexity audit: objective, inequalities, equalities, domain restrictions, nonconvex parts, and chosen relaxation or alternative.
- Operational policy: primal decision, rounding/feasibility handling, re-solve triggers, guardrails, and fallback heuristic.
- Validation plan: feasibility checks, residual/tolerance checks, baseline comparison, sensitivity/tradeoff analysis, and drift monitoring.

## Failure, Recovery, and Idempotency

If the problem is nonconvex, return a nonconvexity finding plus relaxation, decomposition, simulation, or mixed-integer alternative instead of forcing convex notation. If input data is missing, produce a parameterized formulation and list required measurements. On re-run, keep variable names, units, constraint names, and objective components stable unless the model boundary changes.

## Hard Rules

- Do not call a model convex unless minimization objectives and inequality functions are convex and equalities are affine, or a valid transformation is stated.
- Do not hide binary assignment, ordering, routing, or all-or-nothing decisions inside continuous variables without a relaxation and rounding plan.
- Do not present solver output without feasibility status, residual/tolerance expectations, and active-constraint interpretation.
- Do not treat arbitrary scalarization weights as objective truth; expose tradeoffs or justify weights.

## Workflow

1. Define the decision vector.
   - Name the variables the orchestrator can choose: worker fractions, tool permits, queue admission rates, retry budgets, batch sizes, per-class latency budgets, token allocations, model mix, or policy weights.
   - Separate continuous decisions from discrete decisions. Convex optimization is strongest for continuous variables; integer worker assignment or exact job ordering may require a relaxation, rounding step, or a different method.
   - Specify the planning horizon and units so variables share consistent dimensions: requests per minute, tokens per task, dollars per run, worker-minutes, probability mass, or milliseconds.

2. Express the objective.
   - Minimize a convex cost such as expected latency penalty, risk penalty, quota overage, squared deviation from targets, variance, or weighted resource consumption.
   - For maximization, rewrite as minimizing the negative of a concave utility.
   - If there are several goals, scalarize with explicit nonnegative weights or build a tradeoff curve by solving multiple weighted problems.
   - Keep the objective tied to an orchestrator decision, not to a vague preference. Example: minimize `p95_latency_penalty + cost_weight * dollars + risk_weight * failure_risk`.

3. Encode constraints.
   - Use affine equalities for conservation and balance: total allocation sums to one, assigned load equals admitted load, or reserved quota equals the sum of per-class quotas.
   - Use convex inequalities for SLA, budget, risk, fairness, capacity, rate limit, and saturation bounds.
   - Make hard limits explicit: API quota, max concurrent browser sessions, token budget, worker capacity, approval gates, memory, and deadline requirements.
   - Represent soft limits with penalties only when violation is acceptable; otherwise keep them as constraints.

4. Verify convexity before solving.
   - Check that the objective is convex for minimization, inequality constraint functions are convex, and equality constraints are affine.
   - Use known convex forms first: linear programs, least squares, quadratic programs with positive semidefinite matrices, second-order cone constraints, norm bounds, entropy-like penalties, and log-convex transformations where justified.
   - Check domain restrictions: nonnegative allocations, probability simplex constraints, positive rates, and valid logarithm or reciprocal domains.
   - If a formulation is nonconvex, identify the nonconvex part explicitly and decide whether to relax, approximate, decompose, or hand the problem to a mixed-integer/global optimizer.

5. Solve at the right fidelity.
   - Start with the simplest solver class that fits: LP for linear cost and constraints, QP for convex quadratic objectives, SOCP for norm or robust bounds, SDP only when matrix inequality structure is essential.
   - Prefer existing solver-backed modeling tools over hand-rolled optimization code.
   - Scale variables and constraints so solver tolerances are meaningful; avoid mixing huge token counts and tiny probabilities without normalization.
   - Produce both the primal decision and diagnostics: feasibility status, objective value, constraint residuals, active constraints, and solver tolerance.

6. Interpret duals and tradeoffs.
   - Treat dual variables as shadow prices for constraints when strong duality and solver support make the interpretation valid.
   - Use high shadow prices to identify scarce resources: quota, worker capacity, latency budget, cost cap, or fairness lower bound.
   - Explore Pareto tradeoffs by varying weights and recording the resulting objective components.
   - Look for knees in the tradeoff curve where a small gain in one objective requires a large sacrifice in another.

7. Convert the solution into orchestration policy.
   - Map continuous allocations into implementable policy: queue weights, concurrency permits, admission thresholds, retry budgets, batch limits, model-selection ratios, or reservation rules.
   - If rounding is needed, preserve feasibility first; then measure objective degradation against the relaxed solution.
   - Add guardrails for drift: re-solve triggers, maximum policy change per interval, fallback heuristics, and manual override rules.
   - Log enough data to reconstruct each optimization instance: variables, parameters, constraints, weights, solver status, chosen policy, and observed outcome.

8. Validate against reality.
   - Backtest on historical traces or simulate burst cases before deploying a solver-generated policy.
   - Compare the optimized policy against the current heuristic and a simple baseline.
   - Monitor whether the assumptions remain true: convex cost shape, stable parameters, feasible domains, independent resource constraints, and continuous approximation quality.
   - Refit or reformulate when residuals, constraint violations, tail latency, or post-rounding behavior diverge from the model.

## Failure Modes

- Optimizing before formulating the real decision. A beautiful model with the wrong variables produces a precise but useless policy.
- Calling a problem convex because the feasible set "seems nice." Standard convex form requires convex objective and inequality functions plus affine equality constraints.
- Hiding nonconvex decisions such as exact assignment, ordering, binary tool choice, or all-or-nothing approvals inside continuous notation without a relaxation or rounding plan.
- Using solver output without checking feasibility status, residuals, scaling, active constraints, and tolerance.
- Treating dual variables as resource prices when strong duality, constraint qualification, or solver accuracy is not credible.
- Scalarizing objectives with arbitrary weights and presenting one solution as "the" optimum without showing the tradeoff curve or policy sensitivity.
- Ignoring operational friction: integer worker counts, quota granularity, cold starts, lock contention, retry feedback, human approvals, and deployment lag.
- Re-solving too frequently without change limits, causing policy thrash in live orchestration.
- Overfitting weights and parameters to a short trace window that does not include incidents, bursts, or dependency failures.

## Boundaries

Convex optimization helps formulate and solve constrained continuous allocation problems reliably when convexity holds or a useful convex relaxation exists. It does not by itself define task value, safety policy, business priority, or acceptable risk.

Exact scheduling, routing, matching, and assignment problems are often discrete or nonconvex. Convex optimization can still provide relaxations, bounds, shadow prices, and policy weights, but the final orchestrator may need rounding, mixed-integer optimization, simulation, or scheduling-specific algorithms.

This skill complements Operations Research, Scheduling Theory, Queueing Theory, and System Sensitivity Theory. Use Operations Research for broader modeling choices, Scheduling Theory for job ordering, Queueing Theory for dynamic arrivals and waiting, and System Sensitivity Theory when the main question is which parameter most affects outcomes.

## Source Closure

This 21-convex-optimization skill is self-contained for runtime use; its source basis is Convex optimization sources and local convex-optimization entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
