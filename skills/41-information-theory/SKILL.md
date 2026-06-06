---
name: 41-information-theory
description: Use when designing an auto-orchestrator as an information system: observations, messages, evidence handoffs, uncertainty reduction, entropy budgets, compression, redundancy, noisy tool channels, ambiguity, confidence, error correction, or signal-to-noise tradeoffs. Trigger when a task asks how much context to transmit, what evidence to preserve, how to reduce ambiguity across agent/tool boundaries, how to design robust monitoring signals, or how to allocate tokens and retries based on information value; do not trigger for generic information theory summaries or communication history.
source_files:
  - references/source-notes.md
---
# 41 Information Theory

## Book-Derived Essence

- Core framework: Source, channel, code, entropy, mutual information, noise, capacity, and decision value of information.
- Deep idea: Information is reduction of uncertainty under a channel constraint. More data is not better unless it changes distinguishable decisions.
- Discovery method: Define the decision alphabet, uncertainty before/after signal, channel noise, coding scheme, compression/loss, and whether the receiver can act differently.
- Boundary: Do not use information theory as a metaphor for any message; quantify or at least rank uncertainty and channel constraints.
- Source capsule: `references/source-notes.md#BDE-core-framework`

## When To Use

Use this skill when an orchestration design problem is really about information flow, uncertainty, or loss across boundaries. Typical signals include:

- The orchestrator receives noisy observations from tools, logs, agents, sensors, users, or retrieval systems.
- Context windows, traces, summaries, or handoffs must preserve the most decision-relevant information under size limits.
- The design must decide what redundancy, confirmation, retry, or error-correction policy is worth its cost.
- Multiple agents exchange messages and the receiving side may misunderstand, ignore, truncate, or mis-rank evidence.
- Monitoring signals need enough capacity and resolution to distinguish states that require different actions.
- The user asks about entropy, mutual information, channel capacity, source coding, noisy-channel coding, equivocation, redundancy, compression, information bottlenecks, signal-to-noise, or uncertainty reduction in an agent or workflow system.

## Non-Triggers

- Do not trigger for generic Shannon-history summaries, coding-theory homework, or telecommunications tutorials without orchestrator application.
- Do not trigger for ordinary copyediting, prompt shortening, or UI fixes unless a decision-relevant information budget is at stake.
- Do not trigger when observations are exact, channels are lossless enough, and no uncertainty or context-capacity tradeoff affects action.
- Do not trigger for detector thresholds or posterior decision rules when detection-and-estimation theory is the more direct frame.

## Standalone Runtime Contract

This SKILL.md contains the full runtime procedure. Do not read external webpages, original books, source reports, external source snapshots, distilled source material, or files outside this skill directory to execute the skill. `references/source-notes.md` is provenance-only: use it only when the user explicitly asks to audit source lineage, not as an execution dependency.

## Activation And Execution Gate

Before applying this skill, state the activation decision in one sentence. Proceed only if all gate conditions are true:

- A source, channel, receiver, and decision or action alphabet can be named.
- The task involves uncertainty, compression, redundancy, ambiguity, noisy observations, or capacity limits.
- The requested improvement depends on preserving or transmitting decision-relevant information, not merely making text shorter.

If a gate condition is missing, ask up to three targeted questions or recommend a simpler design, copyediting, observability, or detection-theory approach.

## Workflow

1. Model the orchestrator as a communication system.
   - Source: the changing world state, user intent, task graph, tool output, memory, or upstream agent state.
   - Encoder/transmitter: prompt, serializer, summarizer, retriever, schema, trace reducer, monitor, or planner that turns source state into a message.
   - Channel: context window, API call, queue, database row, log stream, tool result, agent handoff, UI field, or human approval path.
   - Noise: truncation, stale data, lossy summarization, ambiguous wording, hallucination, race conditions, latency, sampling variance, parse errors, partial observability, or adversarial input.
   - Decoder/destination: worker, verifier, planner, policy engine, user, or downstream tool that acts on the received message.

2. Define the decision alphabet before optimizing messages.
   - List the downstream actions or states the receiver must distinguish.
   - Treat two source details as equivalent if they always lead to the same downstream decision.
   - Split any overloaded state whose cases require different actions, escalation, rollback, or risk handling.
   - Avoid preserving verbose raw context when a compact sufficient statistic or structured field preserves the same decision power.

3. Estimate uncertainty and information value.
   - Identify the prior uncertainty: what can vary before the receiver observes the message?
   - Estimate which observation fields reduce uncertainty about the next decision, failure mode, or hidden state.
   - Preserve high-value rare signals; rare but action-changing evidence usually carries more information than routine confirmations.
   - Use confidence, source, timestamp, and invalidation rules so the receiver can distinguish evidence from assertion.
   - When a field does not change posterior belief or action choice, compress it, aggregate it, or drop it.

4. Check channel capacity and coding policy.
   - Set the budget: tokens, latency, bandwidth, memory, UI space, human attention, retry allowance, or cost.
   - Compare the budget with the number and complexity of distinctions the receiver must make.
   - If required distinctions exceed capacity, reduce the alphabet, stage the exchange, retrieve on demand, or change the channel.
   - Use source coding for normal operation: schemas, summaries, deltas, stable IDs, hashes, ranked evidence, and structured traces.
   - Keep raw source access or replay handles when compression could erase evidence needed for audit or recovery.

5. Add redundancy where the channel is noisy.
   - Repeat or cross-check only fields whose corruption would cause a wrong or irreversible action.
   - Use independent confirmation channels for high-risk decisions: verifier output, replayed tool call, checksum, citation, audit log, or human approval.
   - Prefer targeted redundancy over full duplication: include confidence, provenance, invariant checks, and small witness examples.
   - Design the decoder to detect impossible, stale, contradictory, or low-confidence messages before acting.
   - Bound retries and confirmations so robustness does not become infinite deliberation.

6. Manage equivocation explicitly.
   - After receiving a message, ask what uncertainty remains about what was actually meant or observed.
   - If residual ambiguity changes the next action, request a clarifying observation instead of guessing.
   - Represent ambiguity as a first-class state: unknown, conflicting, underdetermined, insufficient capacity, or suspected noise.
   - Escalate when the channel cannot reduce ambiguity enough for the action's risk level.

7. Validate the information design.
   - Inject lossy summaries, missing fields, stale observations, conflicting tool outputs, and truncated context.
   - Confirm that the receiver still chooses the correct action or pauses for more information.
   - Measure whether added fields change decisions; remove fields that do not.
   - Check that compressed traces can be expanded or audited when failures occur.
   - Test rare but critical states separately from common paths because average throughput can hide catastrophic ambiguity.

## Failure Modes

- Treating information theory as a metaphor and never naming the source, channel, noise, receiver, and action alphabet.
- Maximizing message detail instead of maximizing decision-relevant uncertainty reduction per unit of budget.
- Compressing away provenance, timestamps, negative evidence, or uncertainty because they look like incidental metadata.
- Assuming semantic meaning is transmitted just because text was transmitted; the receiver only gets what the channel and decoder preserve.
- Adding broad redundancy everywhere, exhausting context and attention without improving high-risk decisions.
- Trusting a single noisy channel for irreversible actions without confirmation or ambiguity detection.
- Calculating confidence from model style or verbosity rather than from evidence quality, independence, recency, and channel reliability.
- Ignoring distribution shift: a coding policy that works for common cases may hide rare failures.

## Output Format And Deliverables

Return the design or analysis in this order unless the user requests another format:

1. Activation decision and communication-system map.
2. Decision alphabet and information needed to distinguish downstream actions.
3. Uncertainty, noise, capacity, compression, and redundancy analysis.
4. Proposed message/channel design with required fields, omitted fields, replay handles, and ambiguity handling.
5. Validation plan, metrics, rare-state tests, and remaining risks.

## Failure, Recovery, And Idempotency

- Treat message formats and coding policies as design recommendations until the user explicitly asks for implementation.
- Re-running the skill should preserve stable field names and decision alphabets unless evidence shows they do not support downstream actions.
- If probabilities, distributions, or measurements are unavailable, use qualitative estimates and label them as provisional.
- On receiver misunderstanding or corrupted handoff, preserve raw replay handles, confidence, provenance, and invalidation rules before compressing further.
- If capacity is insufficient, stage the exchange, retrieve on demand, or change the channel rather than silently dropping action-changing information.

## Boundaries

- This skill designs information flow for auto-orchestrators; it is not a general tutorial on Shannon theory, coding theory, or telecommunications.
- Do not use it when the task is a simple implementation change with no meaningful uncertainty, channel, or context-budget decision.
- Do not claim exact entropy, capacity, or mutual information unless probabilities and measurements are actually available.
- For most software design work, use qualitative entropy and capacity estimates, then validate with tests or traces.
- Keep privacy and security constraints upstream of compression: do not preserve sensitive details merely because they are informative.
- For safety-critical, legal, medical, financial, or irreversible actions, pair information-theoretic robustness with domain-specific review and approval.

## Hard Rules

- Always name source, encoder, channel, noise, decoder/receiver, and action alphabet before optimizing messages.
- Do not claim exact entropy, capacity, mutual information, or error-correction guarantees without measured probabilities or defensible assumptions.
- Do not compress away provenance, timestamp, confidence, negative evidence, or replay handles when they affect audit, recovery, or irreversible decisions.
- Redundancy must target action-changing corruption; broad duplication is not a substitute for channel design.
- Provenance files are not runtime inputs. `references/source-notes.md` may only be cited as source trace when provenance is requested.

## Source Closure

This 41-information-theory skill is self-contained for runtime use; its source basis is Information Theory sources including MacKay notes and local information-theory entry. For provenance, cite `references/source-notes.md#BDE-core-framework`, `#BDE-deep-idea`, or `#BDE-discovery-method` instead of requiring original source files, websites, crawl folders, machine-local paths, parent directories, or cross-skill files.
