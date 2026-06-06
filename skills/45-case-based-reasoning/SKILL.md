---
name: 45-case-based-reasoning
description: Use when designing or repairing an auto-orchestrator that should solve new tasks by retrieving similar prior workflow cases, adapting the prior solution or reasoning path, validating the adapted result, and retaining the new episode for future orchestration.
---

# Case-Based Reasoning For Auto-Orchestrators

## When To Use

Use this skill when an orchestrator needs experience reuse rather than a fresh plan from scratch:

- There is a growing history of solved tasks, incidents, plans, tool traces, evaluations, user corrections, or workflow outcomes.
- Similar past work should influence route selection, tool choice, decomposition, prompt construction, risk controls, or recovery strategy.
- The system needs sustained learning from successes and failures without forcing every lesson into global rules.
- Retrieval quality, case indexing, adaptation, validation, or retention policy is the design problem.

Good auto-orchestrator fits include support-ticket routing, task-plan reuse, agent runbook selection, failed-run repair, evaluation-driven prompt selection, and domain workflows where experts naturally ask "what similar case have we already handled?"

## Workflow

1. Define the case shape before designing retrieval.
   Capture each episode as `problem`, `context`, `constraints`, `solution`, `reasoning_path`, `tool_trace`, `outcome`, `failure_notes`, `human_feedback`, and `retention_decision`. Keep enough explanation to adapt the case, not just enough labels to classify it.

2. Identify retrieval descriptors.
   Separate surface descriptors from causal or semantic descriptors. Prefer descriptors that predict reusable action: goal type, domain, constraints, required tools, failure mode, data shape, user intent, risk class, and expected answer type. Drop noisy descriptors that create false similarity.

3. Choose the memory/index design.
   Use a flat nearest-neighbor index when cases are many, descriptors are stable, and adaptation is lightweight. Use hierarchical or category/exemplar memory when cases cluster into recurring workflow families. Use explanation-backed indexes when the orchestrator must justify why a prior case is relevant.

4. Retrieve for adaptation, not only similarity.
   Rank candidate cases by expected transfer value: shared goal, compatible constraints, similar failure costs, available adaptation path, and known outcome quality. Return several candidates when no single case dominates, then select with an explicit similarity rationale.

5. Reuse by copying, transforming, or replaying.
   Copy only when the new case is a classification or routing decision and differences are irrelevant. Transform the prior solution when known differences can be compensated by operators such as changing tools, thresholds, data sources, prompts, or ordering. Replay the prior reasoning path when the method matters more than the final answer, such as planning, debugging, or multi-agent orchestration.

6. Revise before committing.
   Evaluate the adapted result against the current task: constraints, expected output type, safety rules, tests, user feedback, simulator results, or evaluator scores. If it fails, record the failure explanation and repair the plan with domain knowledge or a fallback reasoning method.

7. Retain selectively.
   Store the new episode when it adds a new workflow family, a new adaptation rule, a corrected failure, a stronger index, or evidence that an existing case should be weakened. Merge or discard near-duplicates. Mark unevaluated cases so they do not become trusted precedents.

8. Tune the case base from outcomes.
   Strengthen indexes and cases that led to successful reuse. Weaken descriptors that retrieved misleading cases. Keep failure cases as first-class memory when they help the orchestrator predict and avoid repeat mistakes.

9. Integrate with other reasoning methods.
   Let rules, search, models, or planners solve cases when memory is insufficient. Retain those solved episodes afterward. Use CBR as one component in an architecture, not as a replacement for all reasoning.

## Failure Modes

- False similarity: the retrieved case shares visible terms but differs in constraints, goals, risk, or hidden causal structure.
- Over-copying: the orchestrator transfers a past answer when the correct reuse target is the reasoning path, repair strategy, or warning.
- Index bloat: every feature becomes an index, making retrieval noisy, expensive, and hard to maintain.
- Unverified retention: failed, partial, or unevaluated cases become precedents without status markers.
- Case-base drift: stale outcomes or changed tools keep influencing current orchestration because retention lacks decay, review, or outcome weighting.
- Missing failure memory: the system only stores successes, so it cannot recognize conditions that should trigger avoidance or repair.
- Over-isolation: CBR is forced to solve tasks that need rules, causal models, planning, search, or direct user clarification.

## Boundaries

Do not use this skill when there are no prior cases, no meaningful similarity relation, or no acceptable way to store task histories. Start with explicit rules, planning, or data collection instead.

Do not treat CBR as simple semantic search over transcripts. A useful case carries the problem, reusable solution knowledge, outcome evidence, and indexing rationale.

Do not retain sensitive or user-specific data without redaction and policy checks. Store abstractions, descriptors, and outcome lessons when raw traces are not appropriate.

Do not let high-confidence retrieval bypass validation. A retrieved case is a hypothesis for reuse; the revise step is still required before action.
