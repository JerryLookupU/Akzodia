---
name: 34-requisite-variety
description: Use when designing or diagnosing an auto-orchestrator that must keep outcomes within acceptable bounds despite many task types, failures, user intents, tool states, latency regimes, or environment disturbances; especially when deciding whether to add sensing, routing branches, fallback policies, specialist agents, approval gates, retries, or task constraints.
---

## When To Use

Use this skill when an orchestrator is failing because the world presents more distinct situations than the orchestrator can observe, classify, or counteract.

Typical triggers:
- A router, planner, supervisor, or recovery loop handles simple cases but collapses under mixed task classes, tool failures, partial observability, or concurrent constraints.
- You need to decide whether to add more policy branches, tools, specialist agents, state tracking, approval gates, retries, or narrower task contracts.
- A team asks for "more control" over outputs without specifying which disturbances must be sensed and which responses are actually available.
- An agent appears overcomplicated, and you need to check whether the extra complexity is necessary response variety or avoidable noise.

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
