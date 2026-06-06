# Source Notes

## Manifest Metadata

- Entry id: 31
- Title: 幂等理论 / Idempotency / Idempotent Receiver
- Skill name: `31-idempotency-idempotent-receiver`
- Source file: `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/31_幂等理论__Idempotency_Idempotent_Receiver/01_www_enterpriseintegrationpatterns_com.txt`

## Source Basis

The provided source is the Enterprise Integration Patterns page for **Idempotent Receiver**, whose core problem is that a receiver may observe the same message more than once even when the sender intended to send it once.

Core claims distilled:

- A receiver should be designed so receiving the same message multiple times is safe.
- In messaging, idempotency means the message has the same effect whether processed once or many times.
- The source identifies two primary approaches:
  - explicit de-duplication by removing duplicate messages;
  - message semantics that are naturally idempotent.
- Related pattern context includes Command Message, Guaranteed Delivery, Messaging, and Resequencer.

## Supplemented Theory Metadata

The source file contains enough pattern text to identify the theory and executable design implications, but it is a short web excerpt rather than the full book chapter. Supplemented metadata used for distillation:

- Primary domain: enterprise integration, message endpoints, distributed workflow recovery.
- Auto-orchestrator mapping: queue redelivery, retry loops, webhooks, tool timeouts, checkpoint restore, external side effects, and finalization.
- Key design translation: duplicate safety must live at the receiver/effect boundary, not only in the sender or broker.

## Distillation Notes

For auto-orchestrators, the practical unit is not only a message endpoint. The receiver can be a worker step, tool adapter, webhook handler, sink writer, run finalizer, or recovery worker. The skill therefore turns the EIP pattern into a concrete design workflow:

1. identify the duplicate boundary and business identity;
2. classify operations as naturally idempotent or unsafe;
3. persist a stable idempotency key and result state;
4. define behavior for completed, pending, retryable, terminal, and mismatched states;
5. test crash, redelivery, timeout, and concurrent duplicate cases.

## Auto-Orchestrator Heuristic

If a step can be retried automatically and has any external side effect, require one of:

- semantic idempotency through a stable target state;
- durable deduplication with a stable idempotency key;
- downstream idempotency support using the same key;
- a transaction, outbox, reconciliation, or compensation design.

Without one of these, retries and recovery must be gated by human review or an explicit risk acceptance.
