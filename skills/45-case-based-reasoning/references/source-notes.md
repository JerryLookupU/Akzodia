# Source Notes

## Manifest Entry

- id: 45
- title: Case-Based Reasoning
- skillName: 45-case-based-reasoning
- skillDir: distilled_skills/auto_orchestrator_theory_skills_v1/skills/45-case-based-reasoning

## Source Files

- `auto_orchestrator_theory_txt_pack_v2/原文目录/08_记忆_知识经验复用/45_案例推理__Case_Based_Reasoning/01_www_iiia_csic_es.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/08_记忆_知识经验复用/45_案例推理__Case_Based_Reasoning/02_journals_sagepub_com.txt`

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
