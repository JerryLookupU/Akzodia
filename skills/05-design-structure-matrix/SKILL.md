---
name: 05-design-structure-matrix
description: Use when designing or repairing an auto-orchestrator workflow whose tasks, agents, tools, modules, or decisions have hidden dependencies, feedback loops, unclear sequencing, rework risk, or excessive coordination cost; applies Design Structure Matrix analysis to map elements, cluster tightly coupled work, sequence acyclic work, and isolate iteration loops.
---

# Design Structure Matrix

## When To Use

Use this skill when the orchestration problem is not mainly about picking the best single next action, but about making dependencies visible and reshaping the work graph.

Strong triggers:
- A plan has many tasks, agents, tools, files, decisions, or subsystems and the order is disputed.
- Work keeps bouncing between steps because downstream outputs change upstream assumptions.
- A user asks to decompose, sequence, modularize, cluster, parallelize, or reduce coordination in a complex workflow.
- The orchestrator needs to decide which tasks can run in parallel, which must be serial, and which require an explicit iteration loop.
- Architecture, product, process, organization, or agent handoff design has coupling that is not obvious from a linear checklist.

Prefer a simpler checklist when there are fewer than five elements and dependencies are obvious.

## Workflow

1. Define the DSM boundary.
   - Name the system being orchestrated and the decision the matrix must support: sequencing, clustering, interface control, parallelization, or loop isolation.
   - List concrete elements as rows and columns. Use one element type per matrix when possible: tasks, agents, components, files, decisions, APIs, or milestones.
   - Keep element names actionably small. Split any element whose dependencies differ across its subparts.

2. Populate dependencies.
   - For each row element, mark the column elements it depends on before it can be completed reliably.
   - Use direction consistently: row needs column is the default.
   - Mark dependency strength when useful: `1` weak/informational, `2` needed for correctness, `3` blocking or high rework risk.
   - Add a short reason for every strong dependency; do not accept vague links such as "related".

3. Diagnose structure.
   - Empty or near-empty rows are early candidates.
   - Dense rows are integration-heavy tasks that need stable inputs, narrower scope, or explicit coordination.
   - Dense columns are shared constraints, bottlenecks, or platform interfaces.
   - Marks below the diagonal after a proposed order indicate feedback dependencies that may cause rework.
   - Blocks of dense mutual dependencies indicate a coupled module or an iteration loop.

4. Transform the plan.
   - Sequence: reorder elements so most dependencies sit above the diagonal under the chosen convention.
   - Parallelize: group elements with no direct or indirect dependency between them.
   - Cluster: put mutually dependent elements into one module, one agent remit, one sprint, or one explicit loop.
   - Decouple: replace a dependency with an interface contract, stable artifact, stub, schema, fixture, or decision record.
   - Isolate loops: when feedback cannot be removed, create a bounded iteration protocol with entry criteria, exit criteria, owner, and maximum cycle count.

5. Produce orchestration output.
   - Return the ordered task list plus parallel batches.
   - Call out clusters that should be owned together.
   - List critical dependencies and interface contracts.
   - Name feedback loops and the stopping rule for each.
   - Include unresolved dependency assumptions that need validation before execution.

6. Recheck after changes.
   - If a task is split, merged, delegated, or moved, update the matrix mentally or explicitly.
   - Before finalizing, ask: "Which dependency, if wrong, causes the most rework?" Put that validation early.

## Failure Modes

- Treating DSM as a pretty table instead of a design intervention. The matrix must change sequence, ownership, interfaces, or loop policy.
- Mixing incompatible element types in one matrix, such as tasks and teams, then reading the result as if all cells meant the same thing.
- Ignoring dependency direction. Reversing row/column meaning leads to the wrong order.
- Over-clustering everything. Dense coupling may justify one loop, but the goal is to expose where decoupling is cheaper than coordination.
- Forcing all feedback out of the plan. Some complex work is legitimately iterative; make it bounded rather than pretending it is linear.
- Recording every weak relation. Too many low-value marks hide the few dependencies that govern execution risk.
- Freezing the matrix after first analysis. DSM is useful because it can be updated as evidence arrives.

## Boundaries

DSM is a structural dependency method, not a prioritization formula, value model, staffing model, or optimization solver. Pair it with cost, impact, risk, or capability scoring when deciding what is worth doing first.

DSM works best when elements and dependency meanings can be made explicit. It is weaker for ambiguous discovery work where the main unknown is what the elements are. In that case, first run a short exploration pass, then build the matrix.

Do not use DSM to justify unnecessary process. For small, obvious workflows, a direct topological order or simple checklist is faster and clearer.

When data is incomplete, label the matrix as provisional and front-load the highest-risk dependency checks. The output should make uncertainty visible, not hide it behind a precise-looking grid.
