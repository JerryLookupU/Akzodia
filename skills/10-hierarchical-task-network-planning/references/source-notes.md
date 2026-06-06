# Source Notes

## Local Sources

- `auto_orchestrator_theory_txt_pack_v2/原文目录/01_头_任务拆解与分类/10_HTN_层次任务网络__Hierarchical_Task_Network_Planning/01_www_cs_umd_edu.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/01_头_任务拆解与分类/10_HTN_层次任务网络__Hierarchical_Task_Network_Planning/02_www_jair_org.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/01_头_任务拆解与分类/10_HTN_层次任务网络__Hierarchical_Task_Network_Planning/03_arxiv_org.txt`

## Metadata

This entry is a theory/system entry rather than a single book.

Primary paper represented by the JAIR/arXiv source:
- Dana Nau, Tsz-Chiu Au, Okhtay Ilghami, Ugur Kuter, J. William Murdock, Dan Wu, and Fusun Yaman.
- "SHOP2: An HTN Planning System."
- Journal of Artificial Intelligence Research, volume 20, pages 379-404, published December 2003.
- DOI: `10.1613/jair.1141`.

Supplementary project source:
- University of Maryland SHOP project page describing SHOP, SHOP2, and JSHOP2 as domain-independent automated planning systems based on ordered task decomposition, a form of HTN planning.

## Distilled Claims

- HTN planning starts from an initial world state and a task network, then recursively decomposes compound tasks into subtasks until primitive tasks can be performed by operators.
- Methods are schemas for decomposing compound tasks. A method has a task head, preconditions, and subtasks; multiple applicable methods create search branches.
- Operators perform primitive tasks and define preconditions and effects. The planner updates state as primitive actions are added to the plan.
- SHOP2 plans forward in the same order actions will execute, which lets method and operator preconditions be evaluated against the current state rather than an abstract future state.
- SHOP2 supports partially ordered subtasks, so subtasks from different compound tasks may interleave when constraints allow.
- Domain knowledge is central: HTN methods often represent standard operating procedures and can make planning practical for complex domains.
- Search control matters. SHOP2 can sort alternative variable bindings by a criterion and can use branch-and-bound to improve plan quality within a time limit.
- Axioms, numeric computations, and external function calls can keep the HTN model expressive without encoding every calculation as a decomposition method.
- Temporal and concurrent domains can be handled by maintaining bookkeeping state, such as read/write timing for dynamic properties.

## Distillation Choices

- Converted formal HTN/SHOP2 concepts into an auto-orchestrator design workflow: state facts, compound tasks, primitive operators, methods, preconditions, effects, branch ranking, and traceable decomposition.
- Emphasized ordered task decomposition because it maps directly to agent orchestration where tool actions mutate shared state.
- Kept optimization pragmatic: rank branches first, reserve branch-and-bound for cases where quality gains justify extra planning time.
- Treated temporal multi-timeline preprocessing as a reusable design pattern: track per-resource read/write conflicts or use explicit locks/versions.
- Avoided long quotations; all source content is paraphrased.

## Auto-Orchestrator Translation

- Compound task: a high-level agent objective that cannot be directly executed.
- Primitive task/operator: a command, API call, edit, message, test, review, deployment, or other executable action.
- Method: a reusable playbook selected when its preconditions match the current state.
- World state: facts about files, tools, user approvals, budget, resource locks, completed evidence, and failed branches.
- Preconditions: facts that must be true before selecting a method or executing an action.
- Effects: facts added, removed, or changed after an action.
- Partial order: constraints that allow safe interleaving or parallel work.
- Backtracking: abandon a failed method/binding and try the next ranked alternative while preserving failure evidence.
