# Source Notes

## Manifest Metadata

- Entry id: 41
- Title: 信息论 / Information Theory
- Skill name: 41-information-theory
- Source completeness: incomplete. Two local source snapshots contain substantive source text; the Cambridge URL snapshot is a Cloudflare service error page.
- Supplemented metadata: the MacKay source identifies the book as David J. C. MacKay, *Information Theory, Inference, and Learning Algorithms*, Cambridge University Press, 2003, version 7.2 fourth printing dated March 28, 2005.

## Source Files

- `auto_orchestrator_theory_txt_pack_v2/原文目录/07_感官_观测信息/41_信息论__Information_Theory/02_people_math_harvard_edu.txt`
  - Local text of Claude E. Shannon, "A Mathematical Theory of Communication," reprinted with corrections from *The Bell System Technical Journal*, Vol. 27, pp. 379-423 and 623-656, July and October 1948.
  - Useful for the communication-system abstraction, logarithmic information measure, entropy, channel capacity, noisy channels, conditional entropy, and equivocation.
- `auto_orchestrator_theory_txt_pack_v2/原文目录/07_感官_观测信息/41_信息论__Information_Theory/04_www_inference_org_uk.txt`
  - Local text of David J. C. MacKay, *Information Theory, Inference, and Learning Algorithms*.
  - Useful for entropy as uncertainty, compression bounds, noisy-channel coding, inference, model comparison, message passing, and the link between information theory and machine learning.
- `auto_orchestrator_theory_txt_pack_v2/原文目录/07_感官_观测信息/41_信息论__Information_Theory/05_www_cambridge_org.txt`
  - Local snapshot contains only a temporary service-unavailable error and no substantive theory content.

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
