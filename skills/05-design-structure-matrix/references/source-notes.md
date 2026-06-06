# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Local Source

- The local source is a DSMweb supplement. It defines DSM, also called Design Structure Matrix, as a dependency and structure modeling technique for managing complexity by focusing on elements of a complex system and their relationships.
- It says DSM-based techniques are used for understanding, designing, and optimizing complex products, organizations, and processes, and are often combined with MBSE and digital visualization tools.

## Supplemented Metadata

The provided source did not contain complete book-style metadata. For audit completeness, the skill treats this entry as a theory/method entry rather than one specific book.

Supplemented stable context:
- Foundational origin commonly attributed to Donald V. Steward, "The Design Structure System: A Method for Managing the Design of Complex Systems", IEEE Transactions on Engineering Management, 1981.
- Major modern methods text: Steven D. Eppinger and Tyson R. Browning, *Design Structure Matrix Methods and Applications*, MIT Press, 2012.
- DSM families commonly include component/product DSM, process/task DSM, organization/team DSM, and multi-domain variants; this skill focuses on auto-orchestrator task, agent, module, and decision dependencies.

## Distillation Choices

- Converted DSM from a general complexity-management technique into an executable orchestration workflow.
- Emphasized dependency direction, clustering, sequencing, feedback-loop isolation, and interface contracts because these are the levers an auto-orchestrator can act on.
- Avoided long quotations; the skill paraphrases the source and uses no extended source excerpts.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Design Structure Matrix sources and local theory-pack entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Components on both axes; dependencies in cells; reorder to expose modules, cycles, bottlenecks, and iteration loops.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use DSM when dependencies are obvious and acyclic; a simple dependency list is enough.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: DSM makes hidden coupling visible. The method is not decomposition but dependency diagnosis: find what forces rework and what can be decoupled.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Build the square matrix, mark information/material/decision dependencies, cluster dense blocks, identify feedback above the diagonal, and propose interface cuts or sequencing changes.
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
