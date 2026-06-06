# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Metadata

- Entry id: 41
- Title: 信息论 / Information Theory
- Skill name: 41-information-theory
- Source completeness: incomplete. Two local source snapshots contain substantive source text; the Cambridge URL snapshot is a Cloudflare service error page.
- Supplemented metadata: the MacKay source identifies the book as David J. C. MacKay, *Information Theory, Inference, and Learning Algorithms*, Cambridge University Press, 2003, version 7.2 fourth printing dated March 28, 2005.

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Distilled Concepts For Orchestrator Design

1. Communication-system decomposition
   - Shannon models communication as information source, transmitter, channel, receiver, destination, and noise source.
   - Orchestrator mapping: world/user/tool state is the source; prompts, serializers, summarizers, retrievers, schemas, and monitors are transmitters; context windows, queues, tool calls, logs, and agent handoffs are channels; workers, verifiers, planners, policy engines, users, and downstream tools are receivers/destinations; truncation, ambiguity, stale data, sampling variance, parse failure, and hallucination are noise.

2. Information is selection among possibilities
   - Shannon frames the engineering problem as reproducing one selected message from a set of possible messages; semantic aspects are not enough for engineering reliability.
   - Orchestrator mapping: define which runtime states or downstream actions must be distinguished. Do not optimize context until the decision alphabet is explicit.

3. Entropy as uncertainty
   - Shannon derives entropy as a logarithmic measure of choice and uncertainty; MacKay defines entropy as the average Shannon information content of an outcome.
   - Orchestrator mapping: prioritize fields that reduce uncertainty about action-changing state. Rare, decision-changing signals often deserve more preservation than routine progress text.

4. Channel capacity
   - Shannon defines channel capacity as the maximum information rate a channel can transmit, subject to symbol durations and allowed sequences.
   - Orchestrator mapping: token windows, latency, storage, human attention, and API cost are channel capacities. If the necessary distinctions exceed capacity, reduce the alphabet, stage the exchange, retrieve on demand, or use a different channel.

5. Compression and source coding
   - MacKay's source-coding discussion ties entropy to the lower bound on compressed descriptions for typical data.
   - Orchestrator mapping: use structured summaries, stable IDs, deltas, hashes, sufficient statistics, and ranked evidence to preserve decision information with fewer tokens. Keep replay handles or raw logs when lossy compression would undermine audit or recovery.

6. Noisy channels and redundancy
   - Shannon's noisy-channel theory separates source uncertainty from noise and introduces conditional entropy and equivocation as ambiguity left after receiving a signal.
   - Orchestrator mapping: tool outputs and agent messages can be corrupted or ambiguous. Add targeted redundancy, independent confirmation, checksums, provenance, confidence, and invariant checks for high-risk decisions.

7. Equivocation
   - Shannon describes equivocation as the average ambiguity of the received signal about what was sent.
   - Orchestrator mapping: after a handoff or observation, explicitly model residual ambiguity. If ambiguity would change the next action, ask for more information or escalate instead of pretending the message was clear.

8. Information theory plus inference
   - MacKay connects information theory with Bayesian inference, model comparison, message passing, and learning algorithms.
   - Orchestrator mapping: a receiver should update beliefs from evidence, compare hypotheses, and propagate compact messages rather than treating every text field as equally reliable.

## Practical Heuristics

- Start with decisions, not data. The value of a message field is whether it changes the receiver's posterior belief or action.
- Use compression for ordinary repeated structure; use redundancy for high-risk corruption paths.
- Preserve provenance, timestamp, confidence, and invalidation rules because these are often the fields that let a receiver discount noisy evidence.
- Treat summaries as codes. Test whether the decoder can recover the needed distinction from the code under realistic noise.
- If the receiver cannot distinguish "safe to act" from "unsafe to act," the channel design has failed even if the message is fluent.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Information Theory sources including MacKay notes and local information-theory entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Source, channel, code, entropy, mutual information, noise, capacity, and decision value of information.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use information theory as a metaphor for any message; quantify or at least rank uncertainty and channel constraints.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Information is reduction of uncertainty under a channel constraint. More data is not better unless it changes distinguishable decisions.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Define the decision alphabet, uncertainty before/after signal, channel noise, coding scheme, compression/loss, and whether the receiver can act differently.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
