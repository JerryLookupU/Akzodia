# Source Notes

## Entry Metadata

- Entry: `02 设计科学 / Artificial Systems / Design Theory`
- Representative work: Herbert A. Simon, `The Sciences of the Artificial`
- Local metadata identifies the entry as a book/theory source for treating an auto-orchestrator as a goal-directed artificial artifact.
- MIT Press metadata used for supplementation: `The Sciences of the Artificial`, reissue of the third edition, Herbert A. Simon, introduction by John E. Laird, MIT Press, published August 13, 2019. The MIT Press page describes it as the expanded and updated third edition from 1996 and as a work arguing for a science of designed systems.

## Local Source Assessment

The assigned source file, `supplement_designresearchsociety_org.txt`, contains mostly Design Research Society navigation, login, footer, news, events, and organizational contact material. It does not provide usable book content for Simon's theory. It was therefore not sufficient by itself for distillation.

Supplementation came from:

- Local `metadata.json` in the same entry directory.
- MIT Press book page: `https://mitpress.mit.edu/9780262354752/the-sciences-of-the-artificial/`
- Stable, widely attributed Simon design-science concepts from `The Sciences of the Artificial`.

## Distilled Theory

Simon reframes design as a science of purposeful artifacts. Natural sciences mainly explain how things are; design sciences reason about how things can be arranged to satisfy goals. This matters for auto-orchestrators because they are not neutral natural objects. They are artificial systems built to transform user intents, environmental constraints, and available tools into preferred outcomes.

Core ideas used in the skill:

- **Artifact as interface:** analyze the orchestrator as an interface between an inner environment and an outer environment.
- **Inner environment:** the artifact's organization, mechanisms, control policies, prompts, memory, code, models, and evaluators.
- **Outer environment:** user goals, task distribution, tool affordances, APIs, files, budgets, latency, permission rules, organizational constraints, and failure costs.
- **Fit:** success depends on whether the inner mechanism is adapted to the outer environment and intended purpose.
- **Design as change:** design work devises actions that move from current conditions to preferred ones.
- **Bounded rationality:** real designers and agents cannot optimize with perfect information, so they need thresholds, heuristics, stopping rules, and feedback.
- **Means-ends decomposition:** complex goals should be converted into subgoals, operators, preconditions, resources, and verification points.
- **Near-decomposability:** complex systems become manageable when split into parts with stable interfaces and limited coupling.

## Auto-Orchestrator Translation

For auto-orchestrator work, the theory becomes a practical diagnostic:

1. If the orchestrator fails, do not only inspect the model or code. Inspect the fit among goals, environment, interface, and mechanism.
2. If goals are vague, do not optimize. Define the preferred situation and measurable thresholds first.
3. If the environment is unstable, build feedback and adaptation rather than hard-coding a static plan.
4. If the system is too complex to reason about, decompose around observable interfaces and independent failure domains.
5. If exhaustive planning is impossible, choose satisficing rules with clear escalation and revision triggers.

## Short Attribution

This skill is a paraphrased operationalization of Simon's artificial-systems and design-science framing for agent/orchestrator architecture. It avoids long quotation and uses only compact theory labels in the executable workflow.
