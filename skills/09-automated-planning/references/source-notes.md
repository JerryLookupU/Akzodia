# Source Notes

## Assigned Source

- `auto_orchestrator_theory_txt_pack_v2/原文目录/01_头_任务拆解与分类/09_自动规划理论__Automated_Planning/supplement_projects_laas_fr.txt`
- Supplement source URL: `https://projects.laas.fr/planning/`

The assigned file is an official project/book page snapshot, not a chapter-length theory excerpt. It identifies the book, authors, publisher, official links, and central framing around integrating planning, acting, and learning for autonomous intelligent systems.

## Supplemented Metadata

- Title: *Acting, Planning, and Learning*
- Authors: Malik Ghallab, Dana Nau, Paolo Traverso
- Publisher: Cambridge University Press
- Year: 2025
- DOI page listed by source: `https://doi.org/10.1017/9781009579346`
- Official BibTeX confirms: `@book{ghallab2025acting, title={Acting, Planning, and Learning}, author={Ghallab, Malik and Nau, Dana and Traverso, Paolo}, year={2025}, publisher={Cambridge University Press}}`

## Distilled Operating Ideas

Automated planning becomes useful for an auto-orchestrator when work cannot be represented safely as a static task list. The orchestrator needs a state model, goal conditions, actions with preconditions and effects, observation paths, and a loop that compares expected effects with actual outcomes.

The official source frames the book around combining planning, acting, and learning. For orchestration design, that maps to three runtime duties:

- Planning: choose actions or policies that can reach explicit goal conditions from the current state.
- Acting: execute through guarded actions whose preconditions, effects, and risks are known.
- Learning: update action models, method choices, and cost estimates from execution evidence without violating hard constraints.

The generated skill uses common automated-planning distinctions as execution choices:

- Forward state-space planning for reliable current-state reasoning.
- Backward reasoning for crisp goal-to-action derivation.
- Partial-order planning to preserve independent work and concurrency.
- Hierarchical task network planning for reusable expert procedures.
- Temporal/resource planning when time, capacity, or cost constraints dominate.
- Contingent or policy planning when observations determine the next action branch.

## Auto-Orchestrator Translation

For an AI orchestration system, a planner should not output only a numbered plan. It should output a plan trace:

- current-state assumptions,
- goal conditions,
- action operators,
- causal links from effects to later preconditions,
- threats and resource conflicts,
- sensing steps for unknown facts,
- replanning triggers,
- approval gates for risky actions.

This is the practical difference between task decomposition and automated planning: task decomposition describes work; planning reasons about which action is valid next in a changing state.
