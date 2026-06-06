# Source Notes

## Local Sources

- `auto_orchestrator_theory_txt_pack_v2/原文目录/02_左手_流程执行/13_业务过程管理__Business_Process_Management/metadata.json`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/02_左手_流程执行/13_业务过程管理__Business_Process_Management/supplement_www_bpmn_org.txt`

## Metadata

The entry is marked locally as a book entry:

- Chinese title: `业务过程管理`
- English title: `Business Process Management`
- Representative book: Marlon Dumas, Marcello La Rosa, Jan Mendling, and Hajo A. Reijers, *Fundamentals of Business Process Management*.
- Springer link recorded locally: `https://link.springer.com/book/10.1007/978-3-662-56509-4`
- Local rationale: the entry covers the lifecycle of process identification, modeling, analysis, redesign, automation, and monitoring.
- Local usage note: convert a task executor into a process lifecycle of modeling, running, monitoring, and optimization.

The only local content file for this entry is a short BPMN.org supplement. It identifies BPMN.org as an official Object Management Group resource for Business Process Model and Notation 2.0, but it does not include substantive specification text.

## Supplemented Metadata And Context

Because the local source text was sparse, the distillation supplemented only minimal public metadata and conceptual context:

- The representative source is treated as the BPM textbook named in `metadata.json`, not as the BPMN.org website itself.
- BPMN.org/OMG is treated as the notation source for BPMN 2.0 concepts such as events, tasks, gateways, sequence flow, message flow, pools, lanes, subprocesses, and exceptions.
- The skill focuses on the BPM lifecycle widely associated with the named textbook and with the local metadata note: process identification, discovery/modeling, analysis, redesign, implementation/automation, monitoring, and continuous improvement.

## Distilled Claims

- A business process is best managed as a repeatable lifecycle, not as a one-off task list.
- Effective process design starts by identifying boundaries, process instances, triggering events, outcomes, participants, and performance goals.
- Process discovery should include actual runtime evidence: logs, tickets, traces, interviews, runbooks, and observed variants.
- BPMN-like modeling is useful for auto-orchestrators when notation elements map to execution contracts: events detect state changes, tasks execute work, gateways route by data, timers create waiting behavior, and boundary events handle exceptions.
- Roles and handoffs are core design objects. A process model should say who or what owns each task and what evidence proves completion.
- Instrumentation is required before optimization. Without correlated events, cycle time, waiting time, rework, queue depth, and failure causes remain guesswork.
- Redesign should be evidence-driven and explicit about tradeoffs among speed, cost, quality, compliance, risk, and user effort.
- Automation should not preserve a broken process unchanged; it should be introduced after process waste, handoffs, and failure modes are understood.

## Distillation Choices

- Converted textbook-level BPM concepts into an auto-orchestrator workflow that can guide implementation: process framing, as-is discovery, executable model, runtime contracts, instrumentation, redesign, and lifecycle review.
- Used BPMN as a practical modeling vocabulary, not as a full notation tutorial.
- Emphasized event correlation, human-task waiting states, exception handling, and compensation because these are frequent failure points in agent orchestration.
- Avoided long quotations; source content is paraphrased.

## Auto-Orchestrator Translation

- Process instance: one run of a repeatable workflow, keyed by a durable id.
- Event: a detectable trigger or state change from a user, tool, timer, log, webhook, queue, or external system.
- Task: an automated, human, or mixed unit of work with inputs, outputs, owner, preconditions, side effects, and evidence.
- Gateway: a routing decision based on explicit data conditions.
- Pool/lane: participant or responsibility boundary across agents, users, services, or organizations.
- Subprocess: reusable or complex process fragment with its own internal control flow.
- Boundary event: exception, timeout, cancellation, escalation, or compensation attached to a task or subprocess.
- Monitoring: correlated runtime events used to measure process health and support redesign.
