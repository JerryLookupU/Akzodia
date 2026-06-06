# Source Notes

## Assigned Sources

- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/20_CSP_通信顺序进程__Communicating_Sequential_Processes/01_www_cs_ox_ac_uk.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/20_CSP_通信顺序进程__Communicating_Sequential_Processes/02_www_cs_cmu_edu.txt`

## Metadata

- Book title: *Communicating Sequential Processes*
- Author: C. A. R. Hoare
- Publisher: Prentice Hall International
- Publication year: 1985
- Related paper: "Communicating Sequential Processes," C. A. R. Hoare, *Communications of the ACM*, Volume 21, Number 8, August 1978.

The Oxford source supplies the book metadata and describes CSP as a language for patterns of interaction supported by mathematical theory, proof tools, and literature. It frames the book as an introduction to both the language and the theory for specification, design, and implementation of continuously interacting computer systems.

The CMU source is the 1978 CACM paper text. It gives the operational basis used for this skill: input and output as programming primitives, parallel composition of sequential processes, explicit source/destination naming, no communication through global-variable updates, synchronous communication without automatic buffering, input guards, arbitrary selection among ready guarded alternatives, termination behavior for repetitive commands, and deadlock risk when corresponding input/output commands cannot meet.

## Distillation For Auto-Orchestrators

CSP maps well onto auto-orchestrator design when agents and tools should be treated as independent state owners connected by explicit protocol events:

- A process becomes an agent, worker, service facade, resource manager, scheduler, or tool adapter.
- Local process state becomes owned state that other participants must access by message.
- CSP input/output commands become channel contracts: sender, receiver, payload type, reply, timeout, and termination behavior.
- Synchronous communication becomes rendezvous, backpressure, or request/accepted handoff.
- Input guards become accept conditions for commands, such as resource availability, buffer capacity, budget, approval, or valid state.
- Alternative guarded commands become orchestrator choice among ready events.
- Deadlock analysis becomes wait-cycle analysis across agents, tools, queues, buffers, and resource managers.
- CSP's caution about fairness becomes an explicit scheduling requirement: correctness must not depend on a runtime "probably" choosing a ready input eventually.

## Source Constraints And Interpretation

The skill paraphrases the sources rather than summarizing the full language. The 1978 paper states that the proposed notation is partial and omits proof method and efficient implementation. For auto-orchestrators, this means CSP should be used as a design and verification lens for communication contracts, not as a demand to implement every queue, lock, monitor, or scheduler from primitive synchronous sends.

No external supplement was needed. The assigned sources contained enough metadata and source content for the entry.
