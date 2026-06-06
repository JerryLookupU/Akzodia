# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Source Basis
- Distilled source: Sowa Computer Standards And Systems History.
- Source pages and local mirrors were used during generation, but no machine-local path is required or preserved as a runtime dependency.
- This note carries the portable source summary. Runtime execution uses `SKILL.md`.
## Key Concepts Internalized
- Law of Standards
- de facto standard
- proactive official standard
- clarification of proven interfaces
- evolutionary system design
- future-system failure
- primary architecture
- secondary architecture
- smooth migration path
- upward compatibility
- hardware/software tradeoff
- make it run before you make it faster
- slogans versus principles
- late system integration risk
- committee overreach
- task-force symptom
- performance feedback
- interim products
- legacy system constraints
- simple rival adoption
## Portable Overview
# Book Overview: Computer Systems and History

## Bibliographic Frame

- Title: Computer Systems and History
- Author: John F. Sowa
- Source entry: `local source snapshot used during distillation`
- Local book wrapper: `local source snapshot used during distillation`
- Chapters: 5
- Nature of text: linked historical notes, standards essay, IBM Future Systems material, Memo 125, and a short Task-Force Tim page.
- Publication dates visible in source: Memo 125 is dated November 27, 1974; "The Law of Standards" is based on a 1991 email and has copyright notes for 2000 and 2004; the index page includes notes added in 2006 and 2016.

## Structural Understanding

The book is not a linear textbook. It is a curated historical case file around one recurring question: why do ambitious future systems and official standards often fail, while simpler evolutionary systems become the real standards?

Reading order:

1. `Computer Systems`: frames IBM FS, HLS, AFS, lost opportunities, and the law of standards.
2. `Advanced Future Systems`: reconstructs the early AFS/HLS context and the more compatible path that might have worked.
3. `Memo 125`: gives the deepest engineering method: primary architecture, slogans versus principles, hardware/software tradeoffs, integration, and migration.
4. `The Law of Standards`: generalizes the historical pattern into a prediction framework for official versus de facto standards.
5. `Task-Force Tim`: supplies organizational symptoms of a failing large system program.

## Interpretive Thesis

Sowa's central claim is that durable systems and standards emerge from working interfaces, evolutionary migration, and simple primary architecture. They do not emerge reliably from large organizations declaring a complex, untested replacement as the future.

The "future" fails when it lacks a path from the past. IBM FS tried to replace System/370 with a revolutionary architecture while customers still needed compatible growth, while competitors could supply better near-term alternatives, and while internal teams lacked a precise primary architecture.

The "standard" fails when it arrives too late or too complex. The official effort raises awareness of a need, but urgent users adopt the simpler alternative that is available soon enough.

## Key Terms

- Law of Standards: official proactive standardization of a new system often causes adoption of a simpler de facto standard.
- De facto standard: the interface or system users actually adopt because it solves practical problems.
- Primary architecture: the closed, fundamental interface base on which all other system components depend.
- Secondary architecture: open-ended user-facing or application-level facilities that can evolve after the primary base exists.
- Smooth migration path: compatibility and interim products that let users move from old to new with minimal disruption.
- Slogan: a catchy term that is not yet a design principle.
- Principle: a precise architectural requirement or constraint that can be implemented and checked.
- Evolutionary integration: build a small working framework and add components one at a time.
- Future-system fantasy: a large replacement project whose architectural, migration, and adoption assumptions are not proved.

## Critical Reading

The source is strongest as an engineering diagnostic, not as a statistically formal law. Sowa's standards examples are persuasive historical cases, but the law should be used as a risk heuristic. It predicts failure mechanisms, not destiny.

The IBM FS material is insider testimony and should be read with that standpoint in mind. Its value is that it names specific design mechanics: data descriptors, linker checks, primary architecture, hardware/software partitioning, virtual-machine migration, and integration structure.

The skill distilled from the book should therefore avoid two overextensions:

- It should not claim that all standards fail.
- It should not claim that all clean-sheet designs are bad.

The executable method is narrower: do not declare a complex new system as standard before implementation, use, migration, and simpler alternatives have been confronted.

## Application Focus

The distilled skill is designed for modern standard and architecture work:

- AI agent protocols and tool contracts.
- API and platform governance.
- Enterprise runtime migrations.
- Cloud, data, and operating-system compatibility plans.
- Hardware/software boundary decisions.
- Language, command syntax, schema, and data model standardization.
- Large program reviews where reorganization and task forces mask missing architecture.

## Book2Skill Decision

The source could have produced several smaller skills, but the user's requested focus is coherent as one executable skill: "Sowa Computer Standards And Systems History." The final skill combines the Law of Standards, IBM FS historical constraints, compatibility design, anti-pattern detection, and future-system judgment into one review workflow.
## Runtime Coverage
- `SKILL.md` contains the executable method, triggers, gates, output formats, failure handling, and boundaries.
- `test-prompts.json` contains portability and compliance expectations.
- `audit.json` points to this local source note rather than external paths.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: John F. Sowa computer history and standards essays. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Standards law, migration path, primary architecture, component discipline, and organizational warning signs.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use this as nostalgia; use it to diagnose architecture and standards decisions today.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Sowa’s practical lesson is that official standards fail when they ignore working interfaces, migration, and simpler de facto alternatives.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Look for monolithic design, absent primary architecture, no migration path, management insulation, repeated task forces, and standards that arrive before practice stabilizes.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

zation, legacy constraints, hardware/software tradeoffs, interface stability, or de facto adoption risk could decide success.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
