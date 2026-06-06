# Source Notes: Knowledge Representation and Reasoning

## Source Files

- `auto_orchestrator_theory_txt_pack_v2/原文目录/01_头_任务拆解与分类/08_知识表示与推理__Knowledge_Representation_and_Reasoning/supplement_plato_stanford_edu.txt`

## Metadata

- Source title: `Logic-Based Artificial Intelligence`.
- Source venue: Stanford Encyclopedia of Philosophy.
- Source URL recorded in file: `https://plato.stanford.edu/entries/logic-ai/`.
- First published: August 27, 2003.
- Substantive revision: February 27, 2024.
- Entry role for this skill: supplemental theory source for knowledge representation, logic-based AI, commonsense reasoning, nonmonotonic logic, and action/change reasoning.

## Distilled Concepts

The source frames knowledge representation as a distinct AI concern: declarative representations, retrieval, maintenance, and reasoning systems should be separable from the programs they serve. This distinction is central for auto-orchestrators because decisions, memory, policy, and explanations become difficult to maintain when knowledge is buried in procedural code or prompts.

Logic-based AI is treated as a way to make reasoning problems explicit, even when final implementations are incomplete, hybrid, or not purely theorem-proving based. For orchestration, this maps to using formal or semi-formal representations as design specifications and audit surfaces.

The strongest operational pattern is nonmonotonic reasoning. Practical agents often reason with defaults that can be defeated by later evidence. The source connects this to belief revision, closed-world reasoning, planning, default logic, circumscription, truth maintenance, and multiple possible extensions. The skill adapts these into explicit default rules, blockers, support dependencies, retraction, and conflict surfacing.

Reasoning about action and change is another core pattern. Planning requires actions with preconditions and effects, plus rules for persistence. The frame problem becomes an orchestrator design issue: after a tool call or subagent handoff, which facts changed, which remained stable, and which hidden qualifications or secondary effects matter?

The source also covers taxonomic representation, nonmonotonic inheritance, contextual reasoning, causal reasoning, spatial reasoning, multiagent knowledge, and practical reasoning. The skill converts these into representation choices for classification, policy inheritance, context-scoped assertions, source integration, and explanation.

Commonsense formalization is presented as difficult but methodologically useful. Benchmark problems and evaluation criteria such as reusability, usability, and elaboration tolerance were adapted into tests for whether an orchestrator knowledge design can absorb new exceptions, changed facts, and scenario variants without wholesale redesign.

## Adaptation Rationale

The skill is not a summary of logic-based AI. It translates the source into a runtime design method for auto-orchestrators:

- Declarative KR becomes a separate knowledge layer for facts, rules, defaults, contexts, provenance, and explanations.
- Nonmonotonic logic becomes a practical default/exception and belief-revision loop.
- Closed-world reasoning becomes a bounded assumption that must be declared rather than applied globally.
- Situation calculus and action/change reasoning become state transition modeling for plans and tool execution.
- Context logic becomes source, user, workspace, time, environment, and policy scoping.
- Taxonomic reasoning becomes task/tool/policy classification and inheritance.
- Commonsense methodology becomes elaboration-tolerance testing for orchestration scenarios.

## Supplementation

The provided source content and metadata were sufficient for this entry. No external web supplementation was needed. The requested `cangjie` skill was not available in this runtime, so distillation used local `book2skill` and `skill-creator` guidance.
