---
name: 39-belief-desire-intention
description: Use when designing an auto-orchestrator or execution agent around Belief-Desire-Intention state: runtime beliefs, competing objectives, adopted plan intentions, commitment strategy, option generation, deliberation, reconsideration, event queues, plan libraries, or reactive goal-directed control. Trigger when a task asks how an orchestrator should decide what to do next in a dynamic environment while balancing plan commitment with changing observations; do not trigger for generic agent philosophy, simple task lists, or planning problems without runtime state and commitment behavior.
source_files:
  - references/source-notes.md
---
# 39 Belief-Desire-Intention

## Book-Derived Essence

- Core framework: Beliefs describe world state; desires define possible objectives; intentions commit to selected plans under resource limits.
- Deep idea: BDI is useful when action selection must persist despite uncertainty, changing evidence, and competing goals.
- Discovery method: List beliefs, desires, intentions, plan library, commitment strategy, reconsideration triggers, sensing gaps, and conflict handling.
- Boundary: Do not use BDI for simple stateless tool routing or psychological metaphor without executable commitments.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when the orchestrator must repeatedly choose and execute plans under changing runtime conditions. Typical signals include:

- The agent needs explicit runtime state for what it currently believes, wants, and has committed to doing.
- The system has many possible procedures, objectives, or environmental outcomes at the same time.
- A static plan fails because observations, tool results, constraints, or user priorities change during execution.
- The design must decide when to keep working a chosen plan and when to reconsider it.
- Multiple plan stacks, suspended goals, subgoals, or event-triggered procedures must coexist.
- The user asks for BDI, belief-desire-intention, PRS-style agents, intention maintenance, option generation, deliberation, or commitment strategy.

## Non-Triggers

- Do not trigger for generic agent philosophy, psychology essays, or histories of intentionality.
- Do not trigger for static project plans, simple checklists, or one-shot tool execution with no runtime reconsideration.
- Do not trigger when the problem is mainly multiagent protocol design, MAPE-K self-management, or deterministic workflow scheduling.
- Do not trigger for ordinary bug fixes unless the fix depends on beliefs, desires, intentions, event queues, or commitment strategy.

## Standalone Runtime Contract

This SKILL.md contains the full runtime procedure. Do not read external webpages, original papers, source reports, external source snapshots, distilled source material, or files outside this skill directory to execute the skill. Any local reference material is provenance-only and must not be treated as required runtime context.

## Activation And Execution Gate

Before applying this skill, state the activation decision in one sentence. Proceed only if all gate conditions are true:

- The target agent has changing observations or events during execution.
- The task requires separating beliefs, desires, candidate options, and adopted intentions.
- A commitment or reconsideration decision matters to correctness, cost, latency, or safety.

If a gate condition is missing, ask up to three targeted questions or use a simpler planning/workflow frame instead of imposing BDI machinery.

## Workflow

1. Define the BDI state contract.
   - Beliefs: mutable facts the orchestrator treats as currently likely, such as task status, tool results, user constraints, resource limits, observed failures, and environment state. Do not call them knowledge unless they are verified and stable.
   - Desires: active objectives, preferences, payoffs, or priorities. Allow them to be many and mutually incompatible until deliberation selects among them.
   - Intentions: adopted plans or plan stacks the orchestrator has committed to execute, monitor, suspend, resume, or abandon.
   - Events: external observations and internal state changes that can trigger option generation.

2. Separate possible actions from adopted intentions.
   - Build an option generator that maps events plus current beliefs to candidate plans.
   - Give every plan an invocation condition, precondition, expected effect, action body or subgoals, and success/impossibility tests.
   - Keep plan selection separate from plan execution. Candidate options are not commitments.
   - Encode context-sensitive plans so new specialized plans can be added without rewriting unrelated plans.

3. Deliberate against resource bounds.
   - Rank or filter options using current desires, belief confidence, plan cost, reversibility, deadlines, and risk.
   - Prefer fast, good-enough deliberation when the environment changes at a rate comparable to planning time.
   - If probabilities and payoffs are measurable, use decision-theoretic scoring. If not, use symbolic criteria and explicit priority rules.
   - Record the chosen option as an intention, not just as a transient next action.

4. Choose the commitment strategy deliberately.
   - Blind commitment: keep the intention even when beliefs or desires change. Use only for short, reversible, or safety-required procedures.
   - Single-minded commitment: keep the intention until it is achieved or believed impossible. Use for most execution plans where stability matters.
   - Open-minded commitment: drop or revise the intention when its motivating desire is no longer active. Use when user priorities or business goals can change mid-run.
   - Define both the commitment condition and the termination condition before implementation.

5. Implement the interpreter loop.
   - Initialize beliefs, desires, intentions, and the event queue.
   - Generate options from queued events.
   - Deliberate and update intentions.
   - Execute the next atomic action or subgoal from active intention stacks.
   - Collect new external events and post internal events.
   - Drop successful desires and satisfied intentions.
   - Drop impossible desires and unrealizable intentions.
   - Post intention-status events at controlled checkpoints so the option generator sees commitment changes at predictable times.

6. Validate behavior under change.
   - Test that stale beliefs are updated before they drive irreversible actions.
   - Inject events during execution and verify whether each active intention is kept, suspended, revised, or dropped according to its strategy.
   - Check that incompatible desires are resolved by deliberation rather than hidden in execution code.
   - Confirm that plan stacks can complete, fail, and clean up without leaving orphaned intentions.
   - Verify that reconsideration frequency is bounded: not every minor event should cause replanning, and no critical event should be ignored.

## Failure Modes

- Treating BDI as labels on ordinary variables while still mixing state update, plan selection, and execution in one procedure.
- Assuming beliefs are true instead of maintaining confidence, source, recency, and invalidation rules.
- Letting every new observation trigger full replanning, causing thrashing and missed deadlines.
- Never reconsidering intentions, causing the orchestrator to pursue obsolete or impossible plans.
- Encoding desires as a single goal string, which hides conflicts, priority changes, and tradeoffs.
- Adding plans without invocation conditions and preconditions, making the option generator noisy and expensive.
- Choosing blind, single-minded, or open-minded commitment implicitly instead of matching it to domain risk.
- Using theorem-prover-level BDI formalisms as the runtime implementation when real-time responsiveness is required.

## Output Format And Deliverables

Return the design or diagnosis in this order unless the user requests another format:

1. Activation decision and runtime scope.
2. BDI state contract: beliefs, desires, intentions, events, confidence, recency, and invalidation rules.
3. Option-generation and plan-library rules with invocation conditions, preconditions, effects, and failure tests.
4. Deliberation and commitment strategy, including reconsideration triggers and termination conditions.
5. Interpreter-loop sketch, validation scenarios, and remaining risks.

## Failure, Recovery, And Idempotency

- Treat BDI outputs as architecture or runtime-policy designs until the user explicitly asks for implementation.
- Re-running the skill should preserve stable intention IDs and annotate why intentions are kept, suspended, revised, or dropped.
- If beliefs are stale, unobservable, or missing confidence/source/recency, require instrumentation before using them for irreversible actions.
- On partial execution failure, post an internal event, update beliefs, and reconsider only affected intentions instead of clearing all plan stacks.
- Bound reconsideration frequency with checkpoints, urgency levels, or event classes so recovery does not become constant replanning.

## Boundaries

- This skill designs runtime deliberation and intention maintenance for auto-orchestrators; it is not a generic project planner.
- Do not use BDI machinery for a one-shot task where a simple checklist or direct tool call is enough.
- Do not claim rationality or optimality without naming the beliefs, desires, intentions, constraints, and deliberation rule.
- Keep formal modal logic lightweight unless the user asks for verification or the system already has a formal model.
- For safety-critical, legal, medical, financial, or irreversible actions, add independent verification and human approval where required.
- If the current runtime state is not observable, instrument event capture and belief updates before designing the deliberator.

## Hard Rules

- Do not call a fact a belief without source, confidence or trust basis, recency, and invalidation conditions.
- Candidate options are not intentions until deliberation adopts them.
- Every intention must have commitment, suspension, success, impossibility, and cleanup conditions.
- Do not let every event trigger full replanning; critical events must be classified and bounded.
- Provenance or source-note files are not runtime inputs and must not be required to execute this skill.

## Source Closure

This 39-belief-desire-intention skill is self-contained for runtime use; its source basis is BDI agent sources and local BDI entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
