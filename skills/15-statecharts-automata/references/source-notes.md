# Source Notes

## Bibliographic Grounding

- Entry: `15 状态机 / Statecharts / Automata`.
- Main representative source: David Harel, "Statecharts: a visual formalism for complex systems", *Science of Computer Programming*, 8(3), 231-274, June 1987. DOI: `10.1016/0167-6423(87)90035-9`.
- The entry metadata also names Michael Sipser, *Introduction to the Theory of Computation*, as representative automata background, but the assigned local source files only provide Harel statecharts material and publication metadata.

## Extracted Ideas For Auto-Orchestrator Design

Harel frames reactive systems as event-driven systems whose behavior is best understood as allowed sequences of events, conditions, actions, and timing constraints. Auto-orchestrators fit this class: they react to tool results, user approval, budget changes, dependencies becoming ready, retries, and cancellation.

Conventional flat state diagrams are useful but break down for complex systems because they become large, repetitive, and hard to review. Statecharts add three practical mechanisms:

- Hierarchy: cluster substates into superstates and attach shared transitions to the superstate.
- Orthogonality/concurrency: split a state into parallel regions so independent dimensions do not create a Cartesian explosion of flat states.
- Communication: transitions can emit actions/events that trigger behavior elsewhere, including across concurrent regions.

Important statechart concepts mapped to orchestration:

- State transition: "when event occurs in state, if guard holds, perform action and enter target state."
- Superstate: a lifecycle group such as `active` containing `ready`, `running`, `blocked`, and `retrying`.
- Default entry: the substate chosen when entering a compound state without a more specific target.
- History entry: re-enter the last active substate when restoration is intentional.
- Orthogonal product: simultaneous state across regions, such as execution state plus budget state plus approval state.
- Action: instantaneous effect such as persisting a transition, emitting an event, or enqueueing work.
- Activity: durable work such as a tool call, timer, or worker process; it needs explicit start and stop.
- Formal next-step semantics: from a current configuration plus current events and conditions, compute the next valid configuration, including internally generated events, until stable.

## Design Implications

Use statecharts to keep orchestration behavior inspectable:

- Put global events like cancellation, budget exhaustion, or fatal error at the highest superstate where they apply.
- Use guards for policy checks rather than duplicating policy states.
- Use parallel regions for independent dimensions and explicit events for synchronization.
- Treat nondeterminism as a bug unless the runtime explicitly resolves it.
- Review the statechart as an executable contract: states, events, guards, actions, activities, invariants, and transition tests.

## Source Completeness Notes

The assigned text file `01_www_weizmann_ac_il.txt` contains only page markers and no extracted article body. The local PDF at the same source path was image-only for embedded text extraction, so selected pages were OCRed locally with Tesseract to recover the paper's core concepts. The second assigned source file provides complete publication metadata and abstract text.
