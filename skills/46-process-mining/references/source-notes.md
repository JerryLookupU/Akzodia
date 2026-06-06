# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Entry

- id: `46`
- skillName: `46-process-mining`
- title: `过程挖掘 / Process Mining`
- sourceFiles:

## Source Coverage

The source is a processmining.org book page for Wil van der Aalst's process mining books:

- `Process Mining: Data Science in Action`, second edition, Springer, 2016.
- `Process Mining: Discovery, Conformance and Enhancement of Business Processes`, Springer, 2011.

The page describes process mining as a discipline that uses event logs from information systems to bridge business process modeling and business intelligence/data science. It emphasizes practical analysis from recorded execution data rather than fictional or assumed process descriptions.

## Distilled Concepts

- Event logs are the primary evidence object. A useful log must reconstruct cases, activities, and ordering over time.
- Process discovery learns process models from raw event data.
- Conformance checking compares observed behavior with an expected model or policy.
- Enhancement extends beyond control-flow discovery into bottlenecks, organizational/resource views, time perspectives, and operational support.
- Operational support includes detecting problems, predicting execution issues, and guiding interventions from event data.
- Tooling and practice matter: the source highlights ProM, commercial tools, real-life data sets, and practical application.

## Auto-Orchestrator Translation

For auto-orchestrator design, process mining becomes a workflow for turning historical runs into design evidence:

- Treat each user request, task, job, incident, or agent run as a case.
- Treat orchestrator steps, tool calls, retries, approvals, failures, handoffs, and completions as activities.
- Use timestamps and attributes to expose variants, bottlenecks, loops, conformance deviations, and predictive intervention points.
- Convert mining findings into routing, retry, validation, escalation, instrumentation, and operational-support changes.

## Metadata Completeness

The manifest provides skill name, directory, title, and one source file. The source provides theory identity, author, books, publication years, scope, target audience, and core method families. No additional external supplementation was required.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Process Mining sources and local process-mining entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Event log quality, process discovery, conformance checking, performance/resource mining, and improvement loop.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not infer process truth from logs that omit manual work, queue waits, or failed attempts.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The essence is evidence-based process repair: actual traces reveal the process model people really execute.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Validate event schema, discover variants, compare to intended model, locate bottlenecks and deviations, then translate findings into model or instrumentation changes.
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
