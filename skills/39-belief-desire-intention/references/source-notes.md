# Source Notes

## Source

- Anand S. Rao and Michael P. Georgeff, "BDI Agents: From Theory to Practice", Proceedings of the First International Conference on Multiagent Systems, AAAI, 1995.
- Local source file: `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/39_BDI_Agent_理论__Belief_Desire_Intention/01_cdn_aaai_org.txt`

## Distillation

The paper argues that Belief-Desire-Intention agents are useful for complex, dynamic, resource-bounded control domains such as air traffic management, telecommunications, spacecraft, medical services, and business processes. The useful design point is not a generic psychological metaphor. It is a runtime architecture for choosing actions when the environment is nondeterministic, the system has multiple options, objectives can conflict, sensing is partial, and the environment can change while deliberation or execution is underway.

For auto-orchestrator design, the three attitudes map cleanly:

- Beliefs are the mutable information component: current observations, inferred state, tool outputs, constraints, and assumptions.
- Desires are the motivational component: objectives, priorities, payoffs, and requested outcomes, which may conflict.
- Intentions are the deliberative component: the chosen course of action or plan stack retained from the last deliberation cycle.

The important engineering move is the explicit intention state. Recomputing the best action at every step can be too expensive and unstable, while executing a chosen plan to completion can ignore important changes. Intentions let the agent balance reactive behavior and goal-directed persistence.

## Interpreter Pattern

The source gives an abstract BDI interpreter:

1. Initialize state.
2. Generate options from the event queue.
3. Deliberate over options.
4. Update intentions.
5. Execute.
6. Get new external events.
7. Drop successful attitudes.
8. Drop impossible attitudes.
9. Repeat.

The practical version uses dynamic data structures for beliefs, desires, intentions, and an event queue. It recognizes both external and internal events. Plans are selected by invocation conditions and preconditions, then represented as intention stacks that may run, suspend, resume, or terminate.

## Commitment Strategies

The source distinguishes commitment condition from termination condition. It gives three useful behavior families:

- Blindly committed: resist belief or desire changes that conflict with current commitments.
- Single-minded: accept belief changes and drop commitments when they become impossible.
- Open-minded: accept belief and desire changes and drop commitments when the motivating desire no longer applies.

The paper does not prescribe one universal strategy. The strategy must be selected for the application and verified against the required behavior.

## Practical Constraints

The paper explicitly warns that ideal BDI logic is not directly practical as a runtime. Logical closure and theorem-proving procedures can be unbounded and destroy responsiveness. Practical BDI systems constrain representation: current beliefs rather than all temporal belief states, plans rather than arbitrary future-world descriptions, and runtime intention stacks rather than fully enumerated intention-accessible worlds.

For auto-orchestrators, this means BDI should become a fast event-driven execution architecture, not a heavyweight philosophical proof layer.

## Auto-Orchestrator Transfer

Use BDI when an execution center must:

- Track partial and changing runtime observations.
- Maintain several competing objectives.
- Convert events into applicable plan options.
- Commit to selected plan stacks long enough to make progress.
- Reconsider plans at bounded checkpoints when beliefs or desires change.
- Explain to humans why it is continuing, revising, or abandoning a plan.

The paper's OASIS example is especially relevant: the scheduler commits single-mindedly to a landing sequence until aircraft have landed or it no longer believes the next aircraft can meet its assigned time. This is a direct pattern for orchestrators that should not restart a global plan for every small signal but must react when feasibility breaks.
