# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Local Sources

## Metadata

The entry is marked locally as a book entry:

- Chinese title: `业务过程管理`
- English title: `Business Process Management`
- Representative book: Marlon Dumas, Marcello La Rosa, Jan Mendling, and Hajo A. Reijers, *Fundamentals of Business Process Management*.
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

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Business Process Management lifecycle sources and local BPM entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Process discovery -> modeling -> execution -> monitoring -> improvement with roles, handoffs, and performance measures.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use BPM for a one-time project plan or static taxonomy with no recurring instances.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: BPM treats a process as a repeatable operational asset, not an isolated plan. Ownership, handoff, exception handling, and measurement are part of the process itself.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Follow a case instance through actors, activities, decisions, artifacts, exceptions, metrics, and improvement loops; then compare designed flow with actual work.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

ze bottlenecks or exceptions, and redesign the process from evidence.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
