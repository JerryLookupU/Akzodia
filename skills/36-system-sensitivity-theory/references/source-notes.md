# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Metadata

- Entry id: 36
- Title: 系统灵敏度理论 / System Sensitivity Theory
- Skill name: `36-system-sensitivity-theory`

## Source Basis

The assigned source is a Wikipedia supplement for **Sensitivity analysis**. It defines sensitivity analysis as the study of how uncertainty in a model or system output can be divided among uncertain input sources. It also distinguishes sensitivity analysis from uncertainty analysis: uncertainty analysis describes overall output uncertainty, while sensitivity analysis identifies which input sources weigh most on the conclusion.

Core ideas distilled:

- Treat the system or mathematical model as a function from input vector to output.
- Quantify uncertainty in inputs before interpreting output robustness.
- Use sensitivity indices or practical approximations to rank which inputs influence output variability.
- Run uncertainty analysis and sensitivity analysis together when possible.
- Choose methods according to constraints such as computational expense, high dimensionality, correlated inputs, nonlinear response, stochastic code, limited data, and multiple outputs.
- One-at-a-time methods are simple and useful for local debugging, but they miss interactions and poorly explore high-dimensional spaces.
- Variance-based and global methods can account for nonlinear response and interactions when enough runs or a metamodel are feasible.
- Sensitivity auditing extends the analysis beyond numeric parameters to framing assumptions and institutional or decision context.

## Supplemented Theory Metadata

The source file is a web article supplement, not a complete monograph or textbook excerpt. It contains enough conceptual material to distill an executable auto-orchestrator skill, but not enough source metadata for a book-level distillation. Minimal supplemental framing was therefore added:

- Primary theory label: system sensitivity analysis for uncertain input-output systems.
- Representative source cited by the supplement: Saltelli et al., *Global Sensitivity Analysis: The Primer* (2008).
- Related practical reference cited by the supplement: Saltelli et al., *Sensitivity Analysis in Practice* (2004).
- Core auto-orchestrator translation: model an orchestrator as a parameterized input-output system, deliberately perturb credible input assumptions, rank which factors most affect user-visible and operational outcomes, then harden or simplify the design accordingly.

## Auto-Orchestrator Translation

For auto-orchestrator design, system sensitivity theory is most useful when a runtime has many knobs and uncertain inputs:

- Inputs map to prompts, model selection, routing policy, tool reliability, context quality, timeout, retry count, budget, evaluator threshold, user ambiguity, and dependency latency.
- Outputs map to completion, correctness, evidence quality, cost, latency, safety, rework, escalation, and user satisfaction.
- Local sensitivity reveals which knob causes a nearby failure or improvement.
- Global sensitivity reveals which combinations of conditions produce brittle, costly, unsafe, or slow behavior.
- Sensitivity auditing reveals when a design conclusion depends on hidden framing assumptions such as "tools are mostly reliable" or "users prefer autonomy over interruption."

The skill therefore emphasizes credible uncertainty ranges, interaction tests, output deltas, sensitivity ranking, and design changes. It avoids turning the agent into a statistics package unless the user's task explicitly requires formal numerical indices.

## Distillation Heuristic

If a design decision changes when a parameter is perturbed within a credible range, the orchestrator is sensitive to that parameter. Require at least:

- a named output that matters to orchestration quality;
- a list of uncertain or tunable inputs;
- credible ranges or scenario values;
- a perturbation plan that includes interactions when plausible;
- a ranking of first-order, interaction-sensitive, low-impact, and unknown factors;
- a concrete design response for high-sensitivity factors.

Without these, the work is ordinary tuning or anecdotal debugging rather than sensitivity-aware orchestration design.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: System sensitivity theory sources and local sensitivity entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Output response to parameter/input perturbation; rank leverage, robustness, and uncertainty impact.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not infer causality from sensitivity alone; it is a model-and-range-dependent diagnostic.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: Sensitivity analysis finds where the system is fragile or controllable by measuring how small changes propagate.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Pick outputs, uncertain inputs, ranges, perturbation design, local/global sensitivity measures, interaction effects, and retest after design changes.
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
