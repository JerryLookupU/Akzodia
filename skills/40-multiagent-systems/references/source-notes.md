# Source Notes

## Source

- Michael Wooldridge, `An Introduction to MultiAgent Systems`, Second Edition, Wiley, 2009.
- Yoav Shoham and Kevin Leyton-Brown, `Multiagent Systems: Algorithmic, Game-Theoretic, and Logical Foundations`, Cambridge University Press, 2009/2010, Revision 1.1 manuscript.
- Local source files:
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/40_多智能体系统__Multiagent_Systems/01_www_cs_ox_ac_uk.txt`
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/40_多智能体系统__Multiagent_Systems/03_masfoundations_org.txt`
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/40_多智能体系统__Multiagent_Systems/04_www_masfoundations_org.txt`

## Distillation

The sources frame multiagent systems as systems containing multiple autonomous entities with diverging information, diverging interests, or both. For auto-orchestrator design, the useful transfer is not "many services" but "many decision makers": components choose local actions under local observations, and group behavior depends on interaction protocols.

Shoham and Leyton-Brown organize the field around coordination, competition, algorithms, game theory, and logic. That structure maps to orchestrator design choices:

- Cooperative distributed problem solving when agents share a global goal but no central controller or complete global view is feasible.
- Distributed constraint satisfaction when each agent owns a local variable and must communicate with neighbors to satisfy global constraints.
- Distributed optimization when the system needs not just feasibility but a best feasible assignment under shared or local objectives.
- Game-theoretic reasoning when agents have distinct preferences, private information, or strategic incentives.
- Communication, social choice, mechanism design, auctions, and coalitions when group protocols must elicit information, allocate resources, or aggregate preferences.

## Key Transfer Patterns

Distributed CSP is the clearest engineering pattern for cooperative orchestration with local ownership. Each agent owns a variable or assignment, communicates with constrained neighbors, tracks a local view, and sends conflict evidence when an assignment cannot work. The asynchronous backtracking pattern adds a priority order, `ok` messages carrying assignments, and `nogood` messages carrying inconsistent partial assignments. For orchestrators, this becomes a design for specialist agents negotiating task ownership, resource allocation, or compatibility constraints without a full central search.

Distributed optimization extends this from "find a feasible assignment" to "optimize a global objective." The source examples include distributed dynamic programming, distributed MDP action selection, auction-like optimization, and social laws. For orchestrators, the practical choice is whether to solve centrally then delegate, let local agents improve assignments through messages, or use market-like bidding to allocate scarce capabilities.

Game theory enters when agents are not perfectly aligned. The source emphasizes self-interested agents, rationalizability, equilibria, correlated signals, congestion games, social choice, mechanism design, auctions, and coalitions. The engineering lesson is that a multiagent protocol must state what agents know, what they prefer, what they can misreport, and why following the protocol is stable enough for the task.

## Auto-Orchestrator Implications

Use multiagent systems theory to design the interaction layer between planners, executors, verifiers, reviewers, retrievers, and tool specialists. The central design questions are:

- What does each agent decide locally?
- What information is private, stale, expensive, or unreliable?
- Are incentives cooperative, competitive, mixed, or unknown?
- Which protocol coordinates local decisions into a global outcome?
- What prevents cycling, deadlock, manipulation, duplicate work, or unbounded communication?
- What evidence explains the final group decision or failure?

The skill deliberately keeps mathematical solution concepts lightweight. In implementation work, protocol contracts, convergence rules, incentives, and failure evidence are usually more valuable than proving a full equilibrium unless the user explicitly asks for formal analysis.
