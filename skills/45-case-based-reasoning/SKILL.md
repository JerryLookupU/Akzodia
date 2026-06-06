---
name: 45-case-based-reasoning
description: Use when designing or repairing an auto-orchestrator that should solve new tasks by retrieving similar prior workflow cases, adapting the prior solution or reasoning path, validating the adapted result, and retaining the new episode for future orchestration.
source_files:
  - references/source-notes.md
---
# 45 Case-Based Reasoning

## Book-Derived Essence

- Core framework: Retrieve, reuse, revise, retain with similarity, adaptation, validation, and memory maintenance.
- Deep idea: CBR treats past solved cases as operational knowledge, but relevance depends on adaptation and post-use learning, not nearest match alone.
- Discovery method: Define case descriptors, similarity weights, adaptation rules, validation checks, outcome feedback, and retention/deletion policy.
- Boundary: Do not trust case retrieval when the new case differs on causal features that the similarity metric ignores.
- Source capsule: `references/source-notes.md#BDE-core-framework`

za case-based reasoning sources; local CBR entry. Do not point users to original source files or source directories during normal use.

## When To Use

Use this skill when an orchestrator needs experience reuse rather than a fresh plan from scratch:

- There is a growing history of solved tasks, incidents, plans, tool traces, evaluations, user corrections, or workflow outcomes.
- Similar past work should influence route selection, tool choice, decomposition, prompt construction, risk controls, or recovery strategy.
- The system needs sustained learning from successes and failures without forcing every lesson into global rules.
- Retrieval quality, case indexing, adaptation, validation, or retention policy is the design problem.

Good auto-orchestrator fits include support-ticket routing, task-plan reuse, agent runbook selection, failed-run repair, evaluation-driven prompt selection, and domain workflows where experts naturally ask "what similar case have we already handled?"

## Standalone Contract

This `SKILL.md` contains the complete runtime procedure. Do not rely on external papers, webpages, source reports, source snapshots, original source paths, or parent-directory materials to execute it. `references/source-notes.md` is provenance-only and may be read only for source trace audits.

Required task inputs are the new problem type, available prior episodes or case sources, similarity signals, reusable solution or reasoning elements, validation method, retention policy constraints, and privacy requirements. If these are missing, ask for the smallest missing item that determines whether case-based reasoning is viable.

## Activation And Execution Gate

Trigger only when an orchestrator should solve or improve new tasks by retrieving similar prior episodes, adapting prior solutions or reasoning paths, validating the adaptation, and deciding what to retain.

Do not trigger when there are no prior cases, no meaningful similarity relation, no acceptable case storage path, or the request is only semantic search, case-table querying, literature summary, or rule-based routing without experiential reuse.

Before executing the workflow, verify all gate conditions:

- There is, or will be, a case base of prior tasks, runs, incidents, plans, traces, evaluations, or user corrections.
- The request depends on reuse and adaptation, not only lookup or classification.
- The design can validate adapted outputs before action or retention.
- Sensitive or user-specific case data can be redacted, abstracted, permissioned, or excluded.

If the gate fails, state the mismatch and recommend explicit rules, planning, data collection, retrieval-only search, or validation design before CBR.

## Workflow

Execute the steps in order. Treat retrieval as a hypothesis generator; adaptation, revision, and retention are mandatory before a case becomes trusted precedent.

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

## Output Format And Deliverables

Return a CBR design or audit with these sections:

- `case_contract`: fields, redaction rules, trust status, ownership, and versioning for stored episodes.
- `retrieval_design`: descriptors, indexes, similarity rationale, candidate count, ranking criteria, and false-similarity controls.
- `reuse_strategy`: copy, transform, replay, or hybrid adaptation method with adaptation operators.
- `revise_validation`: tests, policies, user feedback, simulators, evaluator checks, and repair behavior before action.
- `retention_policy`: store, merge, discard, weaken, strengthen, or quarantine rules with status markers.
- `integration_points`: where rules, planners, search, models, or clarification take over when memory is insufficient.
- `open_risks`: sparse cases, weak validation, stale tools, privacy constraints, index drift, or missing failure memory.

For audits, report each finding against retrieve, reuse, revise, retain, or integration behavior.

## Failure Modes

- False similarity: the retrieved case shares visible terms but differs in constraints, goals, risk, or hidden causal structure.
- Over-copying: the orchestrator transfers a past answer when the correct reuse target is the reasoning path, repair strategy, or warning.
- Index bloat: every feature becomes an index, making retrieval noisy, expensive, and hard to maintain.
- Unverified retention: failed, partial, or unevaluated cases become precedents without status markers.
- Case-base drift: stale outcomes or changed tools keep influencing current orchestration because retention lacks decay, review, or outcome weighting.
- Missing failure memory: the system only stores successes, so it cannot recognize conditions that should trigger avoidance or repair.
- Over-isolation: CBR is forced to solve tasks that need rules, causal models, planning, search, or direct user clarification.

## Failure, Recovery, And Idempotency

- If the case base is too small or unvalidated, design collection, labeling, and validation first; do not present retrieval as reliable.
- If retrieved cases conflict, return multiple candidates with transfer rationales and choose only after explicit validation.
- If a prior case used deprecated tools, policies, or assumptions, adapt or reject it and record the stale dependency as a retention signal.
- If validation fails, store the failure explanation only when it helps future avoidance or repair, and mark it untrusted until reviewed.
- Re-running this skill should preserve stable case IDs, descriptor names, trust labels, and retention decisions unless new evidence changes them.
- If retention is blocked by privacy or policy, retain abstractions, descriptors, and lessons rather than raw traces.

## Boundaries

Do not use this skill when there are no prior cases, no meaningful similarity relation, or no acceptable way to store task histories. Start with explicit rules, planning, or data collection instead.

Do not treat CBR as simple semantic search over transcripts. A useful case carries the problem, reusable solution knowledge, outcome evidence, and indexing rationale.

Do not retain sensitive or user-specific data without redaction and policy checks. Store abstractions, descriptors, and outcome lessons when raw traces are not appropriate.

Do not let high-confidence retrieval bypass validation. A retrieved case is a hypothesis for reuse; the revise step is still required before action.

## Hard Rules

- Do not treat CBR as simple transcript search; every useful case must carry reusable solution knowledge, outcome evidence, and indexing rationale.
- Do not act on a retrieved case without a revise/validation step.
- Do not retain raw sensitive data without redaction, permissions, and a policy basis.
- Do not allow unevaluated, partial, or failed cases to become trusted precedents without status markers.
- Keep runtime execution self-contained in this `SKILL.md`; provenance notes are not required to perform the workflow.

## Source Closure

This 45-case-based-reasoning skill is self-contained for runtime use; its source basis is Aamodt and Plaza case-based reasoning sources; local CBR entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
