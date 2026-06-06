# Source Notes

## Manifest Item

- id: 32
- title: Saga / 补偿事务 / Compensating Transaction
- skillName: 32-补偿事务-compensating-transaction
- assigned source files:
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/32_Saga__补偿事务_Compensating_Transaction/01_learn_microsoft_com.txt`
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/32_Saga__补偿事务_Compensating_Transaction/02_learn_microsoft_com.txt`
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/32_Saga__补偿事务_Compensating_Transaction/03_microservices_io.txt`

## Source Status

The assigned sources are complete enough for this local skill. They include current Microsoft Learn pages for the Saga and Compensating Transaction patterns, a microservices.io Saga pattern page, and local metadata that maps the pattern to auto-orchestrator recovery: long transactions across multiple tools or services should register both forward actions and compensation actions.

No external source supplementation was required. The source set covers:

- Saga as a sequence of local transactions across services.
- Compensating transactions as domain-specific undo or repair actions.
- Choreography and orchestration as coordination styles.
- Compensable, pivot, retryable, and irreversible transaction categories.
- Eventual consistency, lack of distributed ACID isolation, and common saga anomalies.
- The need for idempotent compensation, durable progress records, monitoring, retries, dead-letter/manual recovery, and human review for ambiguous cases.

## Distilled Principles

A saga is not a rollback mechanism in the ACID sense. It is a design contract for a long-running operation that commits local work step by step and still needs to reach a valid final state when later work fails.

The central auto-orchestrator translation is: every meaningful forward action that can escape the process should have a recorded recovery strategy before the orchestrator treats the step as complete. That strategy might be compensation, retry, substitution, manual review, or acceptance that the step is the pivot point.

Compensation is application-specific. It often means "make the business situation valid again," not "restore every record to the exact previous value." This matters when concurrent workflows, customers, providers, or operators have changed the same resource after the original step.

Saga design therefore starts with step classification:

- Compensable steps can be repaired or undone by an explicit command.
- Pivot steps define the point of no return or commitment boundary.
- Retryable steps after the pivot must eventually complete and should be idempotent.
- Irreversible steps need late placement, stronger validation, or human approval.

Retry and alternative forward progress should be considered before compensation. The Microsoft compensating transaction source emphasizes that a single step failure does not always require canceling the whole operation; a substitute path or human decision may be better.

The choice between choreography and orchestration is a control problem. Choreography can keep simple flows decentralized, but complex auto-orchestrator flows usually need explicit state, inspectability, recovery, and operator intervention. That pushes toward orchestration or at least a clearly modeled saga state machine.

Reliable sagas require durable coordination data. The orchestrator should record the forward step, compensation command, idempotency key, correlation id, external transaction id, timeout, result, and retry/dead-letter state. Logs alone are not enough.

Saga isolation is weaker than local ACID isolation. Designers must address dirty reads, lost updates, fuzzy reads, and concurrent saga conflicts using semantic locks, pending states, version checks, rereads, commutative updates, operation logs, or risk-based stronger coordination.

## Auto-Orchestrator Translation

Use the source material as a design checklist:

1. Name the saga boundary and valid terminal states.
2. Decompose the operation into durable local transactions.
3. Attach a recovery strategy to each forward step before implementation.
4. Identify compensable, pivot, retryable, and irreversible steps.
5. Select orchestration or choreography based on complexity, inspectability, and recovery needs.
6. Prefer retry or alternate forward path for transient and substitutable failures.
7. Trigger compensation only when forward progress is invalid, exhausted, canceled, or unsafe.
8. Persist compensation records, idempotency keys, external transaction ids, and audit state.
9. Make both forward and compensation commands duplicate-safe.
10. Test failure after every step, crash during compensation, duplicate messages, and manual review paths.

## Source Files

- `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/32_Saga__补偿事务_Compensating_Transaction/01_learn_microsoft_com.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/32_Saga__补偿事务_Compensating_Transaction/02_learn_microsoft_com.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/32_Saga__补偿事务_Compensating_Transaction/03_microservices_io.txt`

## Metadata Supplement

No metadata supplementation was required. The manifest provided the target name, skill directory, source files, source type, representatives, and usage note; the assigned source files supplied enough theory and implementation context to distill an executable auto-orchestrator design skill.
