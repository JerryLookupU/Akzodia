# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Entry

- Entry: `06 分类学 / 信息组织 / The Discipline of Organizing`
- Skill: `06-信息组织-the-discipline-of-organizing`
- Primary source files:

## Metadata Extracted

- Title: `The Discipline of Organizing: 4th Professional Edition`
- Author: Robert J. Glushko
- First publication: 2013
- Fourth edition noted by iSchools: 2016
- Publisher in Open Textbook Library record: University of California, Berkeley
- ISBN 13: `9780999797013`
- License: Attribution-NonCommercial / CC BY-NC
- Book positioning: a transdisciplinary foundation for organizing systems across information organization, knowledge management, digital collections, information architecture, information systems design, data science, and related fields.

## Distilled Concepts Used

- Organizing is a general design problem: organizing things, information, information about things, and information about information.
- The central abstraction is an `Organizing System`: an intentionally arranged collection of resources and the interactions the arrangement supports.
- Every organizing system involves:
  - a collection of resources,
  - principles or properties used to describe and arrange those resources,
  - interactions supported with the resources.
- The book emphasizes cross-domain comparison: libraries, informatics, computer science, cognitive science, linguistics, philosophy, business, law, archives, museums, and data science use different vocabularies but face recurring organizing patterns.
- The fourth edition adds stronger data-science relevance: resource selection, organization, maintenance, personalization, classification, and descriptive statistics can all be read as organizing techniques.
- The table of contents implies the design sequence used in the skill: foundations, design decisions, activities, resources, metadata, relationships, categorization, classification, description forms, interactions, roadmap, and case studies.

## Auto-Orchestrator Translation

The skill treats an auto-orchestrator as an organizing system whose resources include tasks, agents, prompts, tools, files, memories, datasets, outputs, assumptions, schemas, decisions, and evaluation artifacts. The workflow therefore asks the agent to:

- define the collection boundary,
- inventory resources and resource types,
- choose organizing principles,
- design metadata and relationship models,
- map supported interactions,
- assign governance,
- validate through retrieval and handoff scenarios.

This is intentionally more operational than a summary of the book. The output expected from the skill is an executable organization design that improves agent routing, resource discovery, provenance, reuse, auditability, and lifecycle control.

## Source Limitations

The provided local source files are web/book-record extracts, not the full book text. They include enough metadata and core framing to distill a focused auto-orchestrator skill, but not enough for detailed chapter-by-chapter extraction. I supplemented only with the official online edition availability/path implied by the Open Textbook Library record and the table-of-contents structure already present in the source file. No long quotations were used.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: The Discipline of Organizing; local information-organization entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Resource collection + organizing principles + metadata + interactions. Organizing is designing how resources will be found, compared, combined, and governed.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not build a beautiful taxonomy before knowing access paths, users, and maintenance rules.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: The book’s most useful thought is that categories are interaction commitments. A taxonomy is wrong if it cannot support the retrieval and maintenance actions users actually perform.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Start from supported interactions: what question is asked, what resource is needed, what attribute discriminates it, and what lifecycle state changes it. Let those interactions determine facets and metadata.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

zing is the right skill for a request.
- Key fragment: Use when designing or repairing an auto-orchestrator's information organization: resource collections, task/agent taxonomies, metadata schemas, category systems, retrieval paths, supported interactions, versioned knowledge stores, or handoff structures. Trigger when resources are hard to find, categories overlap, metadata is inconsistent, agents use different naming schemes, or orchestration needs an explicit organizing system rather than an ad hoc folder/list.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
