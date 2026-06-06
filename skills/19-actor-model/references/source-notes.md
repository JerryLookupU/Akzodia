# Source Notes

## Assigned Source

- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/19_Actor_模型__Actor_Model/supplement_dspace_mit_edu.txt`

The assigned file is an MIT DSpace publication record and abstract for Gul Agha's *ACTORS: A Model of Concurrent Computation in Distributed Systems*. It is not a full thesis text extraction.

## Supplemental Local Context

Additional local files used to fill missing metadata and orchestration mapping:

- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/19_Actor_模型__Actor_Model/metadata.json`
- `auto_orchestrator_theory_txt_pack_v2/03_右手_调度并发资源/03_Actor_模型___Actor_Model.txt`
- `auto_orchestrator_theory_txt_pack_v2/10_核心内容补充/03_右手_调度并发资源核心内容.txt`

Relevant metadata:

- Title: *ACTORS: A Model of Concurrent Computation in Distributed Systems*
- Author: Gul Abdulnabi Agha
- Date issued: June 1, 1985
- Series/report number: AITR-844
- Persistent link: `http://hdl.handle.net/1721.1/6952`

## Distilled Concepts

The source abstract frames Actor Model as a concurrency model for distributed systems. The extracted operating ideas for auto-orchestrator design are:

- Concurrency is limited by hardware resources and logical dependencies rather than by a single global control flow.
- Actors communicate through asynchronous message passing.
- Actors can encapsulate changing local state.
- Actors can create other actors dynamically.
- Pipelining and message passing can expose large-scale parallelism.
- Deadlock and divergence are first-class distributed-computing risks.

The local theory pack maps these ideas to orchestrator roles:

- `SchedulerActor`: decides what work is ready and where it should go.
- `WorkerActor`: executes a unit of work or wraps a tool.
- `MonitorActor`: observes health, queue depth, progress, and timing.
- `RecoveryActor`: retries, restarts, compensates, or escalates failed work.
- `MemoryActor`: serializes writes to shared memory or experience stores.

## Auto-Orchestrator Interpretation

For agent orchestration, Actor Model is most useful as a state-ownership and communication discipline:

- Put mutable state behind one actor or one transactional boundary.
- Use explicit message schemas instead of hidden shared variables.
- Make mailboxes observable and bounded.
- Treat supervision as part of the design, not an implementation afterthought.
- Record delivery assumptions and idempotency rules anywhere messages cross process, queue, or storage boundaries.

The resulting skill therefore turns Actor Model into a design checklist for actor boundaries, mailbox contracts, local state ownership, supervision trees, backpressure, dynamic actor creation, and message-failure testing.
