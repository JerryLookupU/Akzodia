# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Entry

- Entry id: 37
- Skill name: `37-autonomic-computing-mape-k`
- Title: `自主计算 / Autonomic Computing / MAPE-K`

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

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Autonomic Computing and MAPE-K sources; local autonomic-computing entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Monitor, Analyze, Plan, Execute over shared Knowledge, bounded by goals and policies.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not call a system autonomic if it only alerts humans and cannot execute governed adaptation.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: MAPE-K is not a vague loop; it separates telemetry, diagnosis, decision, action, and knowledge so self-management can be audited.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Check whether each loop stage has inputs, outputs, ownership, policy, and evidence; missing knowledge or ungoverned execution breaks autonomy.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

zing symptoms and goals, planning changes, executing actions through tools/effectors, and maintaining shared knowledge. Trigger for self-healing, self-optimization, self-configuration, self-protection, adaptive policy control, or MAPE-K loop design in agent runtimes.

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
