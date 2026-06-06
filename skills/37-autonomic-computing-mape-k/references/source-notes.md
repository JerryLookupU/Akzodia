# Source Notes

## Manifest Entry

- Entry id: 37
- Skill name: `37-autonomic-computing-mape-k`
- Title: `自主计算 / Autonomic Computing / MAPE-K`
- Assigned source file: `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/37_自主计算__Autonomic_Computing_MAPE_K/01_jmvidal_cse_sc_edu.txt`

## Assigned Source

The assigned file is a bibliographic snapshot from Jose M. Vidal's library page for Jeffrey O. Kephart and David M. Chess, "The Vision of Autonomic Computing," IEEE Computer, volume 36, number 1, pages 41-50, January 2003, DOI `10.1041/R1052s-2003`, with abstract and BibTeX metadata.

The source gives enough metadata to identify the representative paper and core vision: self-managing systems operate according to administrator goals, and new components integrate with minimal manual intervention. It does not include the full paper body or a complete MAPE-K architectural recipe, so the distillation was supplemented.

## Supplemented Theory Metadata

- Theory: Autonomic Computing / MAPE-K feedback loop.
- Representative source: Jeffrey O. Kephart and David M. Chess, "The Vision of Autonomic Computing," IEEE Computer, 2003.
- Additional IBM architectural lineage: IBM autonomic computing architecture and self-managing systems work describe autonomic managers using Monitor, Analyze, Plan, and Execute functions over shared Knowledge, with sensors and effectors connecting managers to managed resources.
- Main design promise: reduce operator burden in complex systems by making resources self-configuring, self-healing, self-optimizing, and self-protecting under high-level human objectives.

## Auto-Orchestrator Mapping

For agent runtimes, MAPE-K becomes a design pattern for bounded self-management:

- Managed resources map to agents, tools, prompts, memory, queues, sandboxes, budgets, model routes, and task state.
- Sensors map to traces, metrics, evaluator outputs, tool responses, user feedback, policy events, cost counters, and queue telemetry.
- Effectors map to retry, reroute, cancel, pause, escalate, checkpoint, roll back, change model, change retrieval depth, quarantine a dependency, or ask for clarification.
- Knowledge maps to shared state: goals, constraints, policies, topology, run history, tool contracts, action playbooks, and learned incident patterns.
- Monitor normalizes observations into decision-ready state.
- Analyze diagnoses state against goals and predicts risk or degradation.
- Plan selects bounded, policy-compliant actions with preconditions and rollback.
- Execute applies effectors with auditability and post-action verification.

## Distillation Choices

The skill emphasizes executable design steps rather than historical exposition. It adds orchestration-specific controls that are necessary for modern agent systems: idempotency, action leases, permission checks, stale-knowledge handling, dampening against oscillation, and human approval boundaries for high-impact actions.

## Sources Consulted

- Local assigned source file listed above.
- Vidal library page recorded in the local source: `https://jmvidal.cse.sc.edu/lib/kephart03a.html`
- IBM Research publication page, "Autonomic computing: The next era of computing": `https://research.ibm.com/publications/autonomic-computing-the-next-era-of-computing`
- IBM Research publication page, "Self-managing systems: A control theory foundation": `https://research.ibm.com/publications/self-managing-systems-a-control-theory-foundation--1`
- IBM Research publication page, "Autonomic computing: Architectural approach and prototype": `https://research.ibm.com/publications/autonomic-computing-architectural-approach-and-prototype`
