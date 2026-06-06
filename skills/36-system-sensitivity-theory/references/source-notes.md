# Source Notes

## Manifest Metadata

- Entry id: 36
- Title: 系统灵敏度理论 / System Sensitivity Theory
- Skill name: `36-system-sensitivity-theory`
- Source file: `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/36_系统灵敏度理论__System_Sensitivity_Theory/supplement_en_wikipedia_org.txt`

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
