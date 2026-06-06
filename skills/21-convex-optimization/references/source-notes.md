# Source Notes

Primary assigned sources:
- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/21_凸优化__Convex_Optimization/01_stanford_edu.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/21_凸优化__Convex_Optimization/02_web_stanford_edu.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/21_凸优化__Convex_Optimization/03_www_cambridge_org.txt`

Local metadata consulted:
- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/21_凸优化__Convex_Optimization/metadata.json`
- `auto_orchestrator_theory_txt_pack_v2/90_书单总索引.txt`
- `auto_orchestrator_theory_txt_pack_v2/10_核心内容补充/03_右手_调度并发资源核心内容.txt`

## Source-Derived Points

- The representative resource is Stephen Boyd and Lieven Vandenberghe, *Convex Optimization*, published by Cambridge University Press in 2004.
- The Stanford page records that Cambridge University Press allowed the book to remain available on the web and links the open PDF, lecture slides, exercises, and code resources.
- The Cambridge page describes the book as a comprehensive introduction that teaches recognition of convex optimization problems, numerical solution methods, duality, approximation, statistical estimation, and applications.
- The book defines an optimization problem around variables, an objective function, constraint functions, and bounds. A solution is the feasible point with the smallest objective value.
- Convex optimization generalizes least squares and linear programming. The standard convex form minimizes a convex objective subject to convex inequality constraints and affine equality constraints.
- The source emphasizes that recognizing or reformulating a practical problem as convex is the central skill; after that, solving is comparatively reliable and efficient.
- Interior-point and special-purpose methods can solve many convex problems reliably, especially when problem structure such as sparsity is exploited.
- General nonlinear optimization lacks comparable guarantees; local methods may depend heavily on initial guesses and can return only local optima.
- Lagrangian duality augments the objective with weighted constraints. Dual functions give lower bounds, dual problems are convex, and dual variables can support interpretation of constraints.
- For convex problems satisfying suitable conditions, KKT conditions provide necessary and sufficient optimality conditions.
- Multi-objective problems can be scalarized with nonnegative weights, and varying weights can explore an optimal tradeoff curve or surface.

## Auto-Orchestrator Distillation

For auto-orchestrator design, convex optimization becomes a formulation discipline:

- Decision variables represent controllable orchestration choices: allocation shares, quotas, permits, retry budgets, model mix, batching levels, admission rates, or policy weights.
- Objectives represent measurable cost or utility: latency penalty, dollar cost, quota use, risk, fairness deviation, quality loss, or deadline miss penalty.
- Constraints represent hard runtime contracts: SLA ceilings, token budgets, API quotas, worker capacity, queue fairness, memory, deadline feasibility, and conservation of allocation.
- Convexity checks protect the design from pretending a heuristic or nonconvex assignment is solver-ready.
- Dual variables and active constraints can be interpreted as resource pressure signals when the formulation and solver conditions support that.
- Relaxations are useful when exact scheduling or assignment is discrete: solve the convex version for bounds, weights, resource prices, or a continuous policy, then round and validate.

## Metadata Completeness

Metadata and source coverage are complete enough for this skill: the manifest supplies the skill name, target directory, and source files; the local metadata identifies the representative book, authors, status, links, and auto-orchestrator usage; and the full open PDF text is available locally.

No long source quotations were copied into the skill.
