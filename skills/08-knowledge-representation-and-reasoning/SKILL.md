---
name: 08-knowledge-representation-and-reasoning
description: Use when designing or repairing an auto-orchestrator that needs explicit knowledge representation, auditable inference, defaults with exceptions, context-scoped facts, action/change reasoning, taxonomies, belief state, or conflict-aware reasoning across agents and tools.
source_files:
  - references/source-notes.md
---
# 08 Knowledge Representation and Reasoning

## Book-Derived Essence

- Core framework: Facts + rules + defaults + contexts + change + explanation. Representation is chosen by the reasoning task.
- Deep idea: The essence is elaboration tolerance: a knowledge design is good if new exceptions, contexts, and facts can be added without rewriting the whole system.
- Discovery method: Identify the questions the system must answer, what counts as unknown, where defaults can be defeated, what context scopes a claim, and what explanation must be returned.
- Boundary: Do not formali

ze everything; use symbolic KR when inference, explanation, retraction, or context boundaries matter.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when orchestration quality depends on what the system knows, how that knowledge is structured, and which conclusions are licensed from it. Typical triggers:

- The orchestrator must maintain declarative facts, rules, assumptions, tool results, user constraints, and explanations separately from procedural control flow.
- Decisions depend on defaults, exceptions, absent evidence, closed-world assumptions, or "normally true unless contradicted" rules.
- Multi-step plans require reasoning about actions, preconditions, effects, persistence, and what should remain unchanged after each step.
- Subagents, tools, memories, or external sources produce conflicting, partial, stale, or context-specific claims.
- The design needs auditable answers: why a task was routed, why a constraint blocked action, why a fact was believed, or why a default was withdrawn.
- You need a taxonomy or ontology for decomposing domains, classifying work, inheriting policies, or querying stored knowledge.

## Standalone Contract

This skill is self-contained for designing a knowledge and inference layer for auto-orchestrators. `references/source-notes.md` is provenance and rationale, not required runtime context.

Runtime dependency rule: do not open or depend on external files, webpages, original books, source reports, source snapshots, external source folders, or files outside this skill directory. Use `SKILL.md` as the executable contract; local `references/`, `assets/`, or `examples/` may be used only when present and only as optional in-skill support.

Activation gate: use this skill only when the request involves explicit facts, rules, defaults, exceptions, scoped contexts, belief revision, action/change reasoning, auditable inference, or conflict-aware knowledge across agents/tools. Do not activate for generic logic summaries, ordinary UI/code tasks, or simple command selection with no reusable knowledge layer.

Execution gate: before proposing a representation, identify the orchestration decisions to explain, fact/rule sources, context boundaries, default/exception behavior, and whether missing evidence means `false` or `unknown`. If any item is unknowable, state a bounded assumption or ask a targeted question.

## Workflow

1. Separate the knowledge base from the control procedure.
   - Identify the declarative layer: facts, rules, defaults, context labels, provenance, confidence, timestamps, permissions, and source ownership.
   - Identify the procedural layer: planners, subagents, tools, retrieval, execution loops, and UI/reporting.
   - Require every important orchestration decision to name the knowledge inputs and inference rule type it used.

2. Choose the representation by reasoning need.
   - Use a taxonomy or ontology when classification, inheritance, policy lookup, or schema alignment is central.
   - Use rules and constraints when the system must explain why conclusions follow or why actions are disallowed.
   - Use action/state representations when tasks involve plans, preconditions, effects, rollback, or changing world state.
   - Use context-scoped assertions when claims are valid only for a user, workspace, time period, source, environment, jurisdiction, or subtask.
   - Use probabilistic or statistical methods when uncertainty is quantitative and calibrated likelihood matters more than symbolic explanation.

3. Model defaults and exceptions explicitly.
   - Mark which rules are monotonic, meaning added facts should not invalidate prior conclusions.
   - Mark which rules are defeasible, meaning new facts can retract or revise a conclusion.
   - For each default, record its prerequisites, blockers, conclusion, priority, and provenance.
   - Decide whether absence of evidence is meaningful. Closed-world assumptions are acceptable only in bounded inventories, schemas, and verified datasets; otherwise preserve "unknown."

4. Build a conflict and belief-revision loop.
   - Track support dependencies for conclusions: which facts, defaults, source claims, and context assumptions produced them.
   - When new evidence arrives, update affected conclusions instead of globally recomputing or silently accumulating contradictions.
   - When multiple coherent extensions are possible, surface the alternatives, common conclusions, disputed claims, and what evidence would choose between them.
   - Preserve retraction history for decisions that affect safety, cost, policy, user trust, or irreversible actions.

5. Represent action and change before planning.
   - Define state variables, actions, preconditions, direct effects, indirect effects, and invariants.
   - Add persistence rules for facts that should normally remain true across actions.
   - Check frame, qualification, and ramification risks: what stays unchanged, what hidden preconditions may fail, and what secondary effects follow.
   - For every proposed plan, simulate or reason through the state transition sequence before delegating execution.

6. Scope reasoning by context.
   - Attach each fact and rule to the context where it is valid: user, repo, environment, runtime, organization policy, date, location, source, or task phase.
   - Define bridge rules for moving knowledge between contexts, such as "staging policy applies to production only after approval."
   - Prevent context leakage: do not let local assumptions, old memory, or one subagent's working context become global truth without promotion.

7. Design query and explanation paths.
   - Support the queries the orchestrator actually needs: classify this task, choose eligible tools, test whether a plan is allowed, explain a decision, find contradictions, and list missing preconditions.
   - Return explanations in terms of source facts, active context, applied rules/defaults, blocked alternatives, and open unknowns.
   - Keep explanations compact enough for runtime use but complete enough to audit failures.

8. Evaluate by elaboration tolerance.
   - Test the knowledge design on normal cases plus small perturbations: new exception, missing tool result, changed user policy, stale memory, contradictory source, impossible action, and cross-context query.
   - A good representation absorbs these elaborations by adding or revising localized facts/rules, not by rewriting the whole orchestrator.
   - Prefer designs that make scale, integration, maintenance, and automated testing easier.

## Failure Modes

- Encoding knowledge only in prompts or procedural branches, making it hard to query, update, test, or explain.
- Treating all reasoning as monotonic, so exceptions and new evidence fail to retract earlier conclusions.
- Using closed-world assumptions outside bounded datasets, causing "not found" to become false certainty.
- Letting defaults stack without priorities, blockers, or support tracking, producing arbitrary conclusions when rules conflict.
- Ignoring the frame problem in plans, so the orchestrator either assumes everything changes or forgets that most state should persist.
- Mixing contexts: applying a fact from one user, repo, environment, or time period as if it were global.
- Building a rich ontology that no runtime query, verification step, or user explanation actually needs.
- Replacing quantitative uncertainty with symbolic defaults when calibrated probability, statistics, or empirical testing is the right tool.

## Output Format

Return a compact KR design with:

- `Decision Queries`: what the orchestrator must classify, allow, block, explain, or revise.
- `Knowledge Layers`: facts, rules, defaults, contexts, provenance, confidence, and timestamps.
- `Inference Contract`: monotonic rules, defeasible rules, closed-world scopes, bridge rules, and retraction behavior.
- `Action/Change Model`: relevant state variables, preconditions, effects, invariants, and persistence rules.
- `Conflict And Explanation Path`: support dependencies, disputed claims, alternatives, and audit output.
- `Evaluation Cases`: normal case plus exception, stale fact, contradictory source, missing evidence, and context-leak test.

## Failure, Recovery, And Idempotency

When facts conflict, do not silently pick one. Surface source, context, support, priority, and evidence needed to resolve the conflict. When a default is defeated, retract dependent conclusions and preserve the retraction reason for audit-sensitive decisions.

Repeated runs should update the same fact/rule/default inventory by stable IDs or names. Do not promote one session's local assumption to global truth without an explicit bridge rule or owner approval.

## Hard Rules

- Keep knowledge representation separate from procedural control flow.
- Treat closed-world assumptions as valid only inside declared bounded inventories, schemas, or verified datasets.
- Do not use symbolic defaults where the requirement is calibrated probability or empirical ranking.
- Do not allow facts from one user, repo, environment, time period, or subtask to become global truth without promotion rules.

## Boundaries

- This skill is for orchestrator design and repair, not for writing a complete theorem prover, ontology engine, or formal logic textbook.
- It does not require formal logic notation unless the problem is safety-critical, highly regulated, or already uses formal methods.
- It complements retrieval and machine learning. Use KR to structure, constrain, explain, and revise knowledge; use ML where perception, ranking, language variation, or calibrated prediction dominates.
- Do not overformalize low-risk one-off tasks. Use the lightest representation that supports the needed inference, revision, and explanation.
- Domain-specific legal, medical, financial, security, or compliance rules still require domain review; KR helps expose and enforce those rules but does not validate their substance.

## Source Closure

This 08-knowledge-representation-and-reasoning skill is self-contained for runtime use; its source basis is Knowledge Representation and Reasoning sources; local KRR entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
