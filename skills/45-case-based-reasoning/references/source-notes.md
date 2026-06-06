# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Entry

- id: 45
- title: Case-Based Reasoning
- skillName: 45-case-based-reasoning

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Bibliographic Basis

The main source is Agnar Aamodt and Enric Plaza, "Case-Based Reasoning: Foundational Issues, Methodological Variations, and System Approaches," AI Communications, 7(1), pages 39-59, May 1994. The second source is the Sage metadata page and abstract for the same paper.

## Distilled Theory

The paper defines case-based reasoning as solving a new problem by remembering a similar prior problem situation and reusing knowledge from that situation. It frames CBR as both problem solving and sustained learning: new solved experiences are retained so future problems can reuse them.

The central operational model is the four-step cycle:

1. Retrieve the most similar prior case or cases.
2. Reuse the information and knowledge in those cases.
3. Revise the proposed solution through evaluation and repair.
4. Retain the useful parts of the new experience.

For orchestrator design, the important design problem is not just "find a similar transcript." The case memory must store enough information to support reuse: problem descriptors, solution, reasoning path, explanations, outcome evidence, failure information, and indexes.

The source distinguishes shallow syntactic retrieval from knowledge-intensive retrieval. Syntactic retrieval can work when domain knowledge is unavailable and there are enough cases. Knowledge-intensive retrieval uses semantic descriptors, causal explanations, feature importance, expectations, and domain models to justify matches.

Retrieval should be shaped by the intended reuse. A case that is superficially similar may be less useful than a case whose solution can be adapted. Selection should rank cases by match strength, explanation quality, expected consequences, feature importance, and compatibility with the new problem.

Reuse can be direct copying, transformational reuse, or derivational reuse. Copying is suitable for simple classification or routing. Transformational reuse adapts the old solution according to differences between old and new cases. Derivational reuse replays the old method or plan, using the prior reasoning path, subgoals, alternatives, and failed paths.

Revision creates the learning signal. The proposed solution should be evaluated in the real environment, by a teacher/user, by tests, or by a simulator. Failures should be explained and repaired; failure explanations can become memory that helps predict and avoid similar failures.

Retention involves deciding what to keep, how to index it, and how to integrate it into the case base. Useful retained material can include descriptors, solution, explanation, reasoning method, failure notes, and index adjustments. Successful indexes should be strengthened; misleading indexes should be weakened.

The paper also emphasizes integrated architectures. CBR often works alongside rules, causal models, planners, induction, or other learning methods. For auto-orchestrators, this means case memory should accelerate and guide orchestration, while other methods handle novel tasks, hard constraints, and missing-case situations.

## Auto-Orchestrator Translation

- A "case" becomes a stored agent episode: task framing, context, constraints, tool sequence, intermediate decisions, final output, evaluator results, and feedback.
- "Retrieve" becomes memory search over prior runs, incidents, prompts, plans, or workflow templates.
- "Reuse" becomes route selection, prompt/plan adaptation, tool selection, or replay of a proven reasoning path.
- "Revise" becomes validation with tests, policies, user feedback, simulations, evaluator models, or execution results.
- "Retain" becomes selective update of the orchestrator's case memory, index weights, failure memory, and adaptation rules.

## Source Completeness

The manifest metadata and source files were sufficient. No external supplementation was needed.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Aamodt and Plaza case-based reasoning sources; local CBR entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Retrieve, reuse, revise, retain with similarity, adaptation, validation, and memory maintenance.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not trust case retrieval when the new case differs on causal features that the similarity metric ignores.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: CBR treats past solved cases as operational knowledge, but relevance depends on adaptation and post-use learning, not nearest match alone.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Define case descriptors, similarity weights, adaptation rules, validation checks, outcome feedback, and retention/deletion policy.
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
