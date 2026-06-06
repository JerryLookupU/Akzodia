# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Source

The local source file contains the Google SRE book table of contents rather than full chapter text. It identifies the domain scope: embracing risk, service level objectives, eliminating toil, monitoring, automation, release engineering, simplicity, alerting, on-call, troubleshooting, emergency response, incident management, postmortems, testing, overload, cascading failures, reliable launches, communication, and production best practices.

## Supplemental Metadata

- Book: `Site Reliability Engineering: How Google Runs Production Systems`
- Editors: Betsy Beyer, Chris Jones, Jennifer Petoff, and Niall Richard Murphy
- Publisher: O'Reilly Media
- Supplemented pages consulted from the same official source family:

## Distillation Rationale

The auto-orchestrator translation treats SRE as an operating discipline for agent and workflow platforms:

- SLOs convert user promises into measurable reliability policy.
- Error budgets give teams an explicit way to trade launch velocity against reliability work.
- Toil analysis prevents the orchestrator team from scaling production by adding manual intervention.
- Monitoring should page on user-impacting symptoms and keep cause signals available for triage.
- Incident response and postmortems turn failures into changes in system design, process, tests, and ownership.
- Overload handling and launch readiness make reliability a design-time concern rather than a post-incident patch.

The resulting skill is deliberately not a generic SRE summary. It is an executable checklist for designing reliability contracts, ownership, operational controls, and feedback loops around auto-orchestrators.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Site Reliability Engineering source notes and local SRE entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: SLI, SLO, error budget, toil reduction, incident response, overload handling, and launch readiness.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not turn SRE into generic ops hygiene; the method needs user-facing reliability measures and budget decisions.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: SRE’s sharpest idea is the error budget: reliability becomes an explicit product tradeoff, not an infinite aspiration.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Define user-visible SLIs, set SLOs, compute budget burn, identify toil, rehearse incidents, and gate launches against reliability evidence.
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
