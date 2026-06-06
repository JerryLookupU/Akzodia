---
name: 34-requisite-variety
description: Use when designing or diagnosing an auto-orchestrator that must keep outcomes within acceptable bounds despite many task types, failures, user intents, tool states, latency regimes, or environment disturbances; especially when deciding whether to add sensing, routing branches, fallback policies, specialist agents, approval gates, retries, or task constraints.
source_files:
  - references/source-notes.md
---
# 34 Requisite Variety

## Book-Derived Essence

- Core framework: Disturbance variety D, response variety R, acceptable outcomes E, and attenuation/amplification through channels.
- Deep idea: Only variety absorbs variety: a controller must have enough distinguishable responses for the distinguishable disturbances that matter.
- Discovery method: Enumerate disturbance classes, acceptable outcome bands, sensor distinctions, actuator options, policy states, and where variety is reduced or amplified.
- Boundary: Do not add response variety when simpler boundary changes or disturbance attenuation solve the problem.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestrator is failing because the world presents more distinct situations than the orchestrator can observe, classify, or counteract.

Typical triggers:
- A router, planner, supervisor, or recovery loop handles simple cases but collapses under mixed task classes, tool failures, partial observability, or concurrent constraints.
- You need to decide whether to add more policy branches, tools, specialist agents, state tracking, approval gates, retries, or narrower task contracts.
- A team asks for "more control" over outputs without specifying which disturbances must be sensed and which responses are actually available.
- An agent appears overcomplicated, and you need to check whether the extra complexity is necessary response variety or avoidable noise.

## Do Not Trigger

- Do not use this skill for historical exposition of Ashby or generic systems-thinking commentary.
- Do not use it for simple formatting, implementation, or summarization tasks where disturbance/response variety is irrelevant.
- Do not use it when the question is primarily feedback-loop timing or stability; use cybernetics or engineering cybernetics instead.
- Do not use it to justify adding agents, branches, or approvals without named disturbances and regulated outcomes.

## Standalone Contract

This skill is self-contained. Do not browse, open, or depend on external source files, source reports, original books, websites, or cross-skill distilled text during normal execution. `references/source-notes.md` is optional provenance only, not required runtime knowledge. A compliant answer must define regulated outcomes `E`, acceptable bands `h`, disturbance classes `D`, available responses `R`, environment transformation `T`, sensory/motor channel limits, variety gaps, and the smallest boundary/reduction/response change that closes the gap.

## Activation and Execution Gate

Proceed only if all of these are true:

1. The request involves outcomes that must stay within bounds despite varying tasks, states, failures, users, tools, or constraints.
2. The answer can distinguish at least two disturbance classes that require different sensing or response.
3. The design decision is whether to reduce disturbance variety, add sensing, add response capacity, or narrow the task boundary.

If any condition is false, state why this skill is not applicable and route to the more direct implementation, observability, or control-loop guidance.

## Workflow

1. Define the regulation target before proposing mechanisms.
   - `E`: the outcome variables the orchestrator must regulate, such as correctness, safety, latency, cost, user trust, data integrity, or completion.
   - `h`: the acceptable band for each outcome variable. Write concrete pass/fail or tolerance criteria.
   - Do not start with agent roles or tools; start with what must stay inside bounds.

2. Map the disturbance system.
   - `D`: distinguishable disturbances that can push `E` outside `h`: task categories, ambiguous prompts, malformed inputs, tool outages, stale data, long context, adversarial content, budget pressure, human interruptions, hidden dependencies.
   - Treat compound disturbances as vectors. For example, "legal question + stale source + low budget" is a different disturbance from "legal question + fresh source + normal budget".
   - Include initial state when it matters: existing repo dirtiness, prior conversation state, cached plan state, browser tab state, or partially completed work.

3. Map the regulator and environment.
   - `R`: what the orchestrator can vary in response: route, specialist selection, prompt, tool choice, approval policy, decomposition depth, retry strategy, escalation, refusal, or scope reduction.
   - `T`: the environment and fixed transformation from disturbance plus response to outcome: model limits, tool APIs, runtime permissions, service contracts, latency, user-provided constraints, and downstream systems.
   - Identify sensory channels from `D` or `T` into `R`, and motor channels from `R` into `T`.

4. Compare disturbance variety with regulator variety.
   - Use a rough table when possible: rows are `D` cases, columns are `R` responses, cells are outcomes.
   - If one response column maps many different disturbance rows to bad outcomes, the regulator needs more response variety or the task boundary must shrink.
   - If the orchestrator cannot distinguish rows that require different responses, add sensing/state, not just more actions.
   - If it can distinguish rows but cannot act differently, add response capacity, tool access, specialist routes, or escalation paths.

5. Reduce required variety before adding machinery.
   - Block disturbances passively: narrow supported task classes, validate inputs, enforce schemas, cap context windows, pin tool versions, require source freshness, or reject unsupported states.
   - Exploit constraints: collapse equivalent cases, standardize interfaces, canonicalize inputs, reuse deterministic plans, and remove distinctions that do not affect `E`.
   - Move noisy external variation into explicit `D` variables when it affects outcomes.

6. Add regulator variety only where it matches real disturbance variety.
   - Add a route, policy branch, subagent, retry, guardrail, or tool only if it handles a named disturbance class that threatens `h`.
   - For each added response, state the signal that selects it and the outcome risk it reduces.
   - Preserve controller bandwidth: if a human, supervisor model, or policy file must control many independent disturbances, estimate whether its review capacity is enough.

7. Close the loop with evidence.
   - Test should-trigger, should-not-trigger, and edge-case prompts against the designed orchestrator.
   - Check whether failures are sensory restrictions, motor restrictions, wrong boundaries, insufficient response variety, or unrealistic `h`.
   - Iterate by changing one of `D`, `R`, `T`, `E`, or `h`; avoid vague fixes such as "make the agent smarter".

## Output Format / Deliverables

Return a requisite-variety audit with:

- `regulated_outcomes`: `E` variables and concrete `h` bounds.
- `disturbance_map`: `D` classes, compound disturbance vectors, and initial-state factors.
- `regulator_map`: `R` responses, sensing channels, motor channels, owners, and capacity limits.
- `variety_gap`: cases where the regulator cannot distinguish or cannot counteract required disturbance classes.
- `design_moves`: passive variety reduction, added sensing, added response capacity, escalation, or narrowed task contract.
- `evidence_plan`: prompts, logs, simulations, or matrix cases that verify the chosen change.

## Failure, Recovery, and Idempotency

- Re-running this skill should update the same `E/h/D/R/T` map; preserve labels so later audits can compare gaps.
- If outcomes or acceptable bands are undefined, stop and define them before proposing agents, routes, or approvals.
- If the regulator lacks sensing, do not add branches until the selecting signal is defined.
- If the regulator lacks action capacity, report that better diagnosis alone will not regulate the outcome.

## Failure Modes

- Confusing activity with regulation: a busy orchestrator may still let the outcome vary outside `h`.
- Adding actions without sensing: more branches do not help if the orchestrator cannot tell which branch applies.
- Adding sensing without actions: better diagnosis does not help if no distinct response can change `T`.
- Treating all failures as one disturbance: "tool failure" may hide auth failure, timeout, schema drift, stale data, and unsafe output, each needing different responses.
- Ignoring channel limits: a supervisor, approval queue, context window, or logging channel may not carry enough information to regulate all disturbances.
- Overfitting regulator variety: branches for distinctions that do not affect `E` add cost and failure surface without improving regulation.
- Setting undefined targets: without explicit `E` and `h`, the design cannot say what counts as successful control.

## Boundaries

This skill does not produce a complete agent architecture by itself. Use it to size and place sensing, routing, response, and constraint mechanisms.

Do not use it for ordinary summarization of cybernetics, historical exposition of Ashby, or generic "systems thinking" commentary.

Do not assume maximum variety is always best. The first design move is often to reduce disturbance variety through boundaries, schemas, standardization, and passive blocks.

Do not use the law as a precise numeric claim unless the relevant varieties, channels, and acceptable outcomes can actually be measured. In most orchestrator design work, use it as a disciplined comparative audit.

Optional provenance trace is recorded in `references/source-notes.md`; do not load it during normal runtime execution.

## Hard Rules

- Define `E` and `h` before recommending mechanisms.
- Add a response only when it handles a named disturbance that threatens a regulated outcome.
- Add sensing when indistinguishable disturbance classes require different responses.
- Reduce unnecessary disturbance variety before adding regulator complexity.
- Treat human review, context, logging, and approval queues as limited channels with capacity constraints.

## Source Closure

This 34-requisite-variety skill is self-contained for runtime use; its source basis is W. Ross Ashby requisite variety sources and local Ashby entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
