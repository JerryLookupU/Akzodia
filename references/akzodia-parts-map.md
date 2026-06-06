# Akzodia Parts Map

This map defines Akzodia as a book-derived skill organism. It keeps the project from becoming a flat list of summaries.

The metaphor is simple: a complete agent orchestration system needs different body parts. Each part is distilled from books and theories into executable skills. The parts do not merely store knowledge; they decide how knowledge is selected, represented, checked, and evolved.

## Knowledge Layers

| Layer | Meaning | Example |
|---|---|---|
| Knowledge | A usable method or theory. | Queueing theory estimates backlog and wait time. |
| Knowledge of knowledge | A routing rule for when a theory applies. | Queueing is for arrival/service/capacity problems, not for deliverable decomposition. |
| Meta-knowledge | A rule about representing, validating, translating, or evolving knowledge. | Sowa's logic-ontology-computation triad checks whether a representation is inferential, ontological, and computable. |

## Body Parts

### Head: Problem Framing And Planning

Skills: `01-11`

The Head turns ambiguous work into structured intent.

- `01-general-system-theory`: system boundary, environment, feedback, interacting subsystems.
- `02-artificial-systems-design-theory`: artifact, inner environment, outer environment, fit, satisficing.
- `03-systems-engineering`: requirements trace, function, interface, verification, validation.
- `04-work-breakdown-structure`: deliverable hierarchy, 100 percent scope, WBS dictionary.
- `05-design-structure-matrix`: dependency matrix, coupling, clustering, iteration loops.
- `06-信息组织-the-discipline-of-organizing`: collections, metadata, facets, access interactions.
- `07-ontological-engineering`: competency questions, classes, slots, facets, instances.
- `08-knowledge-representation-and-reasoning`: facts, rules, defaults, contexts, inference, explanation.
- `09-automated-planning`: state, goal, action, precondition, effect, replanning.
- `10-hierarchical-task-network-planning`: compound tasks, methods, primitive tasks, decomposition.
- `11-operations-research`: variables, objective, constraints, feasible policy, sensitivity.

Discovery question: what is the task really made of, and what structure must exist before action is safe?

### Left Arm: Flow Execution

Skills: `12-16`

The Left Arm manipulates workflow, state, and transaction semantics.

- `12-workflow-management`: case, token, split, join, race, cancellation.
- `13-business-process-management`: lifecycle, roles, handoffs, repeatable process improvement.
- `14-petri-nets`: places, transitions, tokens, markings, reachability.
- `15-statecharts-automata`: state, event, guard, action, hierarchy, parallel regions.
- `16-transaction-processing`: ACID, schedules, isolation, logs, commit and recovery.

Discovery question: what execution traces are legal, blocked, duplicated, or unsafe?

### Right Arm: Scheduling And Concurrent Resources

Skills: `17-21`

The Right Arm allocates capacity and handles concurrent work.

- `17-scheduling-theory`: jobs, machines, release dates, deadlines, precedence, objective.
- `18-queueing-theory`: arrivals, service, servers, utilization, wait time, Little's Law.
- `19-actor-model`: isolated state, mailbox, message, supervision, backpressure.
- `20-communicating-sequential-processes`: channels, rendezvous, choice, refusal, deadlock.
- `21-convex-optimization`: convex variables, feasible set, duality, sensitivity.

Discovery question: where do resource limits, waiting, communication, and optimization shape behavior?

### Left Leg: Trace, Replay, And Verification

Skills: `22-25`

The Left Leg gives the system historical footing.

- `22-event-sourcing`: commands, events, streams, projections, replay.
- `23-process-mining`: event log, case trace, variant, conformance, enhancement.
- `24-monitoring-observability`: logs, metrics, traces, evidence, unknown-failure investigation.
- `25-model-checking`: finite model, temporal property, exhaustive search, counterexample.

Discovery question: what actually happened, can it be replayed, and does it violate a property?

### Right Leg: Recovery And Reliability

Skills: `26-32`

The Right Leg keeps the system standing after partial failure.

- `26-distributed-systems`: nodes, messages, clocks, partitions, state ownership.
- `27-reliable-distributed-systems`: fault model, quorum, replication, consensus, recovery.
- `28-data-intensive-applications`: source of truth, derived views, storage, streams, schema evolution.
- `29-checkpointing-and-rollback-recovery`: consistent cut, checkpoint, rollback line, replay.
- `30-site-reliability-engineering`: SLI, SLO, error budget, toil, incident response.
- `31-idempotency-idempotent-receiver`: idempotency key, duplicate store, state-specific duplicate handling.
- `32-补偿事务-compensating-transaction`: saga, compensable step, pivot, retryable step, semantic repair.

Discovery question: what fails partially, what must remain true, and how does the system continue?

### Control Core: Feedback And Autonomy

Skills: `33-40`

The Control Core regulates behavior.

- `33-cybernetics`: sensor, comparator, controller, actuator, feedback, disturbance.
- `34-requisite-variety`: disturbance variety, response variety, acceptable outcomes.
- `35-engineering-cybernetics`: plant, controller, dynamics class, transfer path, delay, noise, stability.
- `36-system-sensitivity-theory`: perturbation, output response, leverage, robustness.
- `37-autonomic-computing-mape-k`: monitor, analyze, plan, execute, knowledge.
- `38-viable-system-model`: operations, coordination, control, intelligence, policy.
- `39-belief-desire-intention`: belief, desire, intention, commitment, reconsideration.
- `40-multiagent-systems`: local agents, protocols, incentives, coordination, emergence.

Discovery question: how does the system sense error, choose correction, remain stable, and adapt?

### Senses: Signals And Diagnosis

Skills: `41-43`

The Senses convert noise into actionable evidence.

- `41-information-theory`: entropy, channel, code, noise, capacity, information value.
- `42-detection-and-estimation-theory`: hypotheses, observations, estimator, threshold, false alarm, miss.
- `43-monitoring-and-observability`: symptoms, causes, alerts, traces, operational diagnosis.

Discovery question: which signals reduce uncertainty enough to justify action?

### Memory: Knowledge And Experience Reuse

Skills: `44-47`

Memory keeps experience from being lost.

- `44-knowledge-engineering`: CommonKADS organization, task, agent, knowledge, communication, design models.
- `45-case-based-reasoning`: retrieve, reuse, revise, retain.
- `46-process-mining`: process traces as reusable operational knowledge.
- `47-retrieval-augmented-generation`: corpus, chunk, retrieve, rerank, cite, evaluate.

Discovery question: what prior knowledge or experience can be reused, and how should it be adapted?

### Meta-Knowledge Crown: Knowledge About Knowledge

Skills: `48-52`

The Meta-Knowledge Crown checks representation, meaning, and proof.

- `48-sowa-conceptual-graphs`: concept, relation, referent, context, coreference, CGIF, Common Logic.
- `49-sowa-knowledge-representation`: logic, ontology, computation.
- `50-sowa-ontology-engineering`: top-level category, lexicon, role, process, sign, purpose.
- `51-sowa-computer-standards-history`: standard, de facto adoption, migration path, primary architecture.
- `52-sowa-mathematical-logic-background`: set, relation, graph, lattice, model truth, object language, metalanguage.

Discovery question: is the knowledge represented in a form that preserves meaning, supports inference, and can be translated without semantic loss?

## Neighbor Boundaries

- WBS is not scheduling: WBS owns deliverable scope; scheduling owns scarce resources over time.
- Planning is not HTN: automated planning owns state-action search; HTN owns reusable procedural decomposition.
- Workflow is not Petri net: workflow owns pattern semantics; Petri nets own token/resource concurrency.
- Event sourcing is not process mining: event sourcing records domain facts; process mining discovers actual process behavior from logs.
- Observability is not SRE: observability preserves diagnostic context; SRE turns reliability into SLO/error-budget decisions.
- Cybernetics is not MAPE-K: cybernetics models feedback regulation; MAPE-K defines an autonomic management architecture.
- Ontology engineering is not KR: ontology names what exists; KR also chooses inference and computational realization.
- Conceptual graphs are not ordinary diagrams: they must preserve type, referent, relation order, identity, context, and quantifier scope.

## Evolution Constraint

Any future update should identify which body part is being strengthened. If the update cannot name the part, the native framework, and the discovery method, it is probably generic documentation rather than Akzodia evolution.
