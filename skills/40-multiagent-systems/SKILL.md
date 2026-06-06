---
name: 40-multiagent-systems
description: Use when designing, reviewing, or debugging an auto-orchestrator made of multiple autonomous agents, workers, tools, planners, evaluators, or services that have local state, partial information, separate objectives, strategic behavior, resource contention, negotiation, voting, auctions, coalitions, distributed constraint solving, or coordination protocols. Trigger when the design question is how agents interact and converge on group behavior; do not trigger for a single-agent planner, generic microservices, or distributed reliability issues without autonomous decision makers.
---

# Multiagent Systems For Auto-Orchestrators

## When To Use

Use this skill when orchestration behavior emerges from interactions among multiple decision-making components:

- A task is split across agents that each own local state, capabilities, tools, budgets, or permissions.
- No participant has a complete global view, but the system still needs a coherent global outcome.
- Agents may be cooperative, self-interested, adversarial, or only partially aligned.
- The design needs a protocol for assignment, negotiation, voting, auctions, coalition formation, conflict resolution, or shared-resource use.
- Local choices can conflict through constraints, congestion, duplicate work, stale beliefs, or incompatible incentives.
- The user asks for multiagent systems, MAS, distributed constraint satisfaction, distributed optimization, social choice, mechanism design, auctions, coalition behavior, agent communication, or coordination conventions.

## Workflow

1. Identify the agents and their autonomy.
   - List every participant that can choose actions independently: planner, executor, verifier, specialist agent, scheduler, tool gateway, evaluator, retriever, human proxy, or external service.
   - For each agent, record its observations, private state, action space, utility or objective, authority, resource limits, and communication channels.
   - Decide whether autonomy is real or only an implementation detail. If all choices are centrally controlled, use a workflow, distributed-systems, or scheduling pattern instead.

2. Classify the interaction regime.
   - Cooperative: agents share one global objective but have local information or local resources.
   - Competitive: agents optimize different objectives and can benefit from withholding information, gaming the protocol, or shifting cost.
   - Mixed-motive: agents share some goals but compete over priority, budget, reputation, latency, scarce tools, or final credit.
   - Unknown or changing: assume incentives can drift and add observation, audit, and override paths.

3. Model local decision variables and global constraints.
   - Define which variable, task, tool, route, budget slice, or artifact each agent owns.
   - Write the constraints that couple agents: mutual exclusion, dependency order, consistency, quality threshold, budget cap, privacy boundary, deadline, or resource capacity.
   - If the target is feasibility, use a distributed constraint-satisfaction framing: local assignments, neighbor communication, conflict detection, and explicit nogood messages or rejection reasons.
   - If the target is best feasible outcome, add objective functions and choose distributed optimization, auction-like allocation, local search, or centralized optimization with delegated execution.

4. Choose the coordination protocol.
   - Direct coordination: message local assignments, status, constraints, and conflict explanations between affected agents.
   - Market-style coordination: use bids, prices, budgets, auctions, or contract-net style task allocation when agents compete for scarce work or resources.
   - Voting or preference aggregation: use when agents provide rankings, recommendations, or judgments and the system must select a group outcome.
   - Convention or social law: use stable default rules for repeated coordination problems, such as tie-breaking, priority lanes, lock ordering, escalation order, or retry etiquette.
   - Coalition or team formation: use when a subset of agents can jointly satisfy a task that no single agent can satisfy alone.

5. Make strategic assumptions explicit.
   - State whether agents are truthful, boundedly rational, utility maximizing, policy constrained, or adversarial.
   - If truthful reporting matters, design incentives or verification so lying, exaggerating confidence, hiding cost, or free riding is not rewarded.
   - If preferences are aggregated, check spoiler effects, agenda sensitivity, tie-breaking power, and whether the voting rule matches the decision risk.
   - If auctions or bids allocate work, define valuation units, reserve prices or caps, anti-collusion assumptions, budget exhaustion behavior, and winner obligations.

6. Define communication semantics.
   - Specify the message types: proposal, bid, vote, assignment, ok, conflict, nogood, counteroffer, acceptance, rejection, commitment, cancellation, and evidence.
   - Include sender, recipient, round, run id, local state version, deadline, confidence, cost, and required response in every protocol message.
   - Bound communication with rounds, fanout limits, quorum rules, or escalation paths; naive all-to-all communication usually fails under scale.
   - Separate communication for coordination from telemetry for observability.

7. Add convergence and stopping rules.
   - Define success: feasible global assignment, selected winner, stable coalition, equilibrium-like no-improvement state, quorum decision, or bounded best effort.
   - Define failure: empty domain, no acceptable bid, cyclic preferences, no quorum, budget exhaustion, inconsistent constraints, or protocol timeout.
   - Use priority order, deterministic tie-breaking, potential functions, monotone progress metrics, leases, or bounded rounds to prevent endless cycling.
   - Preserve conflict evidence so a central overseer or human can diagnose why convergence failed.

8. Validate under interaction pressure.
   - Simulate delayed messages, partial information, conflicting local choices, strategic misreports, overloaded shared resources, duplicate claims, and changing objectives.
   - Test both cooperative cases and mixed-motive cases; a design that only works when all agents are honest and synchronized is not a multiagent protocol.
   - Check that local improvements do not degrade global objectives beyond accepted bounds.
   - Confirm that every final decision can be explained from agent inputs, protocol rules, and tie-breakers.

## Failure Modes

- Calling ordinary service decomposition a multiagent system even though no component makes autonomous decisions.
- Centralizing all hidden decisions while pretending the agents negotiate, which prevents testing incentive and information assumptions.
- Assuming local optimization creates global optimality without modeling constraints, externalities, or congestion.
- Using naive asynchronous local updates that can cycle forever or terminate in a locally stuck but globally solvable state.
- Omitting priorities, tie-breakers, deadlines, or no-solution messages, causing coordination protocols to hang.
- Letting agents vote, bid, or rank outputs without considering strategic manipulation, agenda sensitivity, spoiler effects, or collusion.
- Treating communication as free and reliable; multiagent protocols can become dominated by message fanout, stale views, or missing responses.
- Aggregating preferences before normalizing confidence, cost, eligibility, and authority, causing weak agents to overrule accountable owners.
- Rewarding agents only for local success, which encourages duplicate work, hidden failures, or bad handoffs.

## Boundaries

- This skill designs interaction protocols for autonomous agents in auto-orchestrators; it is not a generic summary of multiagent theory.
- Use a distributed-systems skill when the main issue is replication, consistency, queues, retries, or partial failure without autonomous decision makers.
- Use BDI or planning skills when the main issue is a single agent's runtime beliefs, goals, intentions, or plan selection.
- Use operations research or scheduling skills when a central optimizer has full information and agents only execute assigned work.
- Do not introduce auctions, voting, or game-theoretic machinery unless incentives, private information, or independent authority make simple assignment inadequate.
- For source provenance and distilled rationale, read `references/source-notes.md`.
