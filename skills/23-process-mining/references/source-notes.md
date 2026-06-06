# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
Runtime note: this file is provenance/source trace only. The executable skill contract and required operating knowledge are contained in `../SKILL.md`; do not require external source files, webpages, source reports, or original texts at runtime.

## Manifest Item

- Entry id: 23
- Skill name: `23-process-mining`
- Title: 过程挖掘 / Process Mining

## Source Basis

The manifest source is a processmining.org book page for Wil van der Aalst's *Process Mining: Data Science in Action* and the earlier *Process Mining: Discovery, Conformance and Enhancement of Business Processes*. It states that process mining covers the spectrum from process discovery to predictive analytics, highlights conformance checking, organizational and time perspectives, and positions the field between business process modeling, business intelligence, data science, and event logs.

The local metadata for this entry identifies the auto-orchestrator use as discovering real processes, deviations, and bottlenecks from execution logs, then using task event logs to summarize common workflow templates, failure points, and duration distributions.

Because the primary source file is a short supplemental page rather than the full book text, the skill also uses local source-adjacent notes:

## Distilled Operating Model

For auto-orchestrator design, process mining becomes a feedback loop:

1. Treat every workflow run as a case.
2. Convert raw events into a process-mining event log with case id, activity, timestamp, lifecycle/outcome, actor/tool, and evidence references.
3. Discover actual variants from traces instead of assuming the declared workflow is what happened.
4. Check conformance between observed traces and expected plans, policies, or templates.
5. Mine bottlenecks, waiting, rework, failure concentration, and hidden handoffs.
6. Feed findings back into orchestrator templates, guards, scheduling, retries, compensations, monitoring, and instrumentation.

## Key Concepts For The Skill

- Event log: structured records of what happened during process instances.
- Case or trace: the sequence of events for one process instance.
- Activity: a normalized step such as plan, retrieve, call tool, validate, wait, escalate, compensate, or complete.
- Discovery: deriving the actual process model from traces.
- Conformance: comparing observed traces with an intended model or policy.
- Enhancement: improving the process model or runtime behavior using evidence from logs.
- Variant: a recurring trace pattern that may represent a happy path, exception path, workaround, or defect.
- Bottleneck: an activity, queue, handoff, or state that contributes disproportionate waiting, failure, or cost.
- Alignment: a way to reason about where observed behavior matches or deviates from expected behavior.

## Adaptation Notes

The source literature is broader than auto-orchestrators and includes business-process analysis, ProM, inductive mining, alignments, organizational perspectives, time perspectives, and predictive analytics. This local skill narrows that theory into executable design work for agent orchestration:

- It emphasizes trace ids, task ids, tool calls, retry counts, state snapshots, decision reasons, and artifact references.
- It treats logs as design evidence for improving orchestrator templates and runtime controls.
- It avoids generic process-mining tutorial content and focuses on actions an agent can take during architecture, debugging, instrumentation, and improvement work.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Process Mining sources and local process-mining entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Event log -> discovery -> conformance -> enhancement. The real process is reconstructed from traces.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not mine logs that lack stable case identity or trustworthy timestamps without first repairing instrumentation.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Process mining prevents process theater: it compares designed flow with observed behavior and exposes variants, bottlenecks, and deviations.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Validate case id, activity, timestamp, actor, and lifecycle fields; discover variants, align them to the model, then mine performance and resource perspectives.
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
