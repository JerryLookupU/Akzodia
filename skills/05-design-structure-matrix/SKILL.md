---
name: 05-design-structure-matrix
description: Use when designing or repairing an auto-orchestrator workflow whose tasks, agents, tools, modules, or decisions have hidden dependencies, feedback loops, unclear sequencing, rework risk, or excessive coordination cost; applies Design Structure Matrix analysis to map elements, cluster tightly coupled work, sequence acyclic work, and isolate iteration loops.
source_files:
  - references/source-notes.md
---
# 05 Design Structure Matrix

## Book-Derived Essence

- Core framework: Components on both axes; dependencies in cells; reorder to expose modules, cycles, bottlenecks, and iteration loops.
- Deep idea: DSM makes hidden coupling visible. The method is not decomposition but dependency diagnosis: find what forces rework and what can be decoupled.
- Discovery method: Build the square matrix, mark information/material/decision dependencies, cluster dense blocks, identify feedback above the diagonal, and propose interface cuts or sequencing changes.
- Boundary: Do not use DSM when dependencies are obvious and acyclic; a simple dependency list is enough.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestration problem is not mainly about picking the best single next action, but about making dependencies visible and reshaping the work graph.

Strong triggers:
- A plan has many tasks, agents, tools, files, decisions, or subsystems and the order is disputed.
- Work keeps bouncing between steps because downstream outputs change upstream assumptions.
- A user asks to decompose, sequence, modularize, cluster, parallelize, or reduce coordination in a complex workflow.
- The orchestrator needs to decide which tasks can run in parallel, which must be serial, and which require an explicit iteration loop.
- Architecture, product, process, organization, or agent handoff design has coupling that is not obvious from a linear checklist.

Prefer a simpler checklist when there are fewer than five elements and dependencies are obvious.

## Standalone Contract

This skill is self-contained. Use the workflow below to analyze dependencies and reshape an orchestration plan without reading original source files.

The skill should produce a dependency model that supports sequencing, clustering, parallelization, interface control, and bounded iteration loops.

## Activation and Execution Gate

Activate only when there are enough elements or hidden dependencies that a linear checklist may cause rework, wrong sequencing, or coordination waste. Do not activate for simple priority scoring, value ranking, or glossary explanations.

Before running the workflow, identify the matrix boundary, element type, dependency direction, and decision the DSM must support. If there are fewer than five obvious elements, first decide whether a simpler loop contract is sufficient.

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

## Output Format

Return a DSM analysis with:

- `Boundary`: system, element type, decision objective, dependency convention.
- `Elements`: rows/columns with stable labels and split/merge notes.
- `Dependency map`: dependency strength, direction, and reasons for strong dependencies.
- `Diagnosis`: bottlenecks, dense rows/columns, feedback marks, clusters, and uncertainty.
- `Transformation`: sequence, parallel batches, clusters, decoupling moves, interface contracts.
- `Iteration policy`: loop entry criteria, exit criteria, owner, maximum cycles, stop rule.
- `Validation priorities`: dependencies to verify early because they create the most rework if wrong.

## Failure Modes

- Treating DSM as a pretty table instead of a design intervention. The matrix must change sequence, ownership, interfaces, or loop policy.
- Mixing incompatible element types in one matrix, such as tasks and teams, then reading the result as if all cells meant the same thing.
- Ignoring dependency direction. Reversing row/column meaning leads to the wrong order.
- Over-clustering everything. Dense coupling may justify one loop, but the goal is to expose where decoupling is cheaper than coordination.
- Forcing all feedback out of the plan. Some complex work is legitimately iterative; make it bounded rather than pretending it is linear.
- Recording every weak relation. Too many low-value marks hide the few dependencies that govern execution risk.
- Freezing the matrix after first analysis. DSM is useful because it can be updated as evidence arrives.

## Failure, Recovery, and Idempotency

If dependencies are unknown, label the matrix provisional and front-load discovery for the highest-rework assumptions. If dependency direction is disputed, resolve the convention before interpreting sequence or parallelism.

On re-run, preserve element labels where possible, document split/merge/move changes, and update the dependency map before changing recommended sequence. Repeated execution should refine the same matrix and transformation choices rather than inventing a new convention.

## Hard Rules

- Do not mix incompatible element types in one matrix unless each cell meaning is explicitly defined.
- Do not ignore dependency direction or change row/column convention mid-analysis.
- Do not present DSM output as a priority, staffing, or value model.
- Do not eliminate legitimate feedback loops by pretending iterative work is linear; bound the loop instead.

## Boundaries

DSM is a structural dependency method, not a prioritization formula, value model, staffing model, or optimization solver. Pair it with cost, impact, risk, or capability scoring when deciding what is worth doing first.

DSM works best when elements and dependency meanings can be made explicit. It is weaker for ambiguous discovery work where the main unknown is what the elements are. In that case, first run a short exploration pass, then build the matrix.

Do not use DSM to justify unnecessary process. For small, obvious workflows, a direct topological order or simple checklist is faster and clearer.

When data is incomplete, label the matrix as provisional and front-load the highest-risk dependency checks. The output should make uncertainty visible, not hide it behind a precise-looking grid.

## Source Closure

This 05-design-structure-matrix skill is self-contained for runtime use; its source basis is Design Structure Matrix sources and local theory-pack entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
