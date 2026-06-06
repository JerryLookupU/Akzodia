# Source Notes

## Manifest Item

- Entry id: 23
- Skill name: `23-process-mining`
- Title: 过程挖掘 / Process Mining
- Primary source file: `auto_orchestrator_theory_txt_pack_v2/原文目录/04_左脚_跟踪记录回放/23_过程挖掘__Process_Mining/supplement_processmining_org.txt`

## Source Basis

The manifest source is a processmining.org book page for Wil van der Aalst's *Process Mining: Data Science in Action* and the earlier *Process Mining: Discovery, Conformance and Enhancement of Business Processes*. It states that process mining covers the spectrum from process discovery to predictive analytics, highlights conformance checking, organizational and time perspectives, and positions the field between business process modeling, business intelligence, data science, and event logs.

The local metadata for this entry identifies the auto-orchestrator use as discovering real processes, deviations, and bottlenecks from execution logs, then using task event logs to summarize common workflow templates, failure points, and duration distributions.

Because the primary source file is a short supplemental page rather than the full book text, the skill also uses local source-adjacent notes:
- `auto_orchestrator_theory_txt_pack_v2/04_左脚_跟踪记录回放/02_过程挖掘___Process_Mining.txt`
- `auto_orchestrator_theory_txt_pack_v2/10_核心内容补充/04_左脚_跟踪记录回放核心内容.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/04_左脚_跟踪记录回放/23_过程挖掘__Process_Mining/metadata.json`

## Distilled Operating Model

For auto-orchestrator design, process mining becomes a feedback loop:

1. Treat every workflow run as a case.
2. Convert raw events into a process-mining event log with case id, activity, timestamp, lifecycle/outcome, actor/tool, and evidence references.
3. Discover actual variants from traces instead of assuming the declared workflow is what happened.
4. Check conformance between observed traces and expected plans, policies, or templates.
5. Mine bottlenecks, waiting, rework, failure concentration, and hidden handoffs.
6. Feed findings back into orchestrator templates, guards, scheduling, retries, compensations, monitoring, and instrumentation.

## Key Concepts For The Skill

- Event log: structured records of what happened during process instances.
- Case or trace: the sequence of events for one process instance.
- Activity: a normalized step such as plan, retrieve, call tool, validate, wait, escalate, compensate, or complete.
- Discovery: deriving the actual process model from traces.
- Conformance: comparing observed traces with an intended model or policy.
- Enhancement: improving the process model or runtime behavior using evidence from logs.
- Variant: a recurring trace pattern that may represent a happy path, exception path, workaround, or defect.
- Bottleneck: an activity, queue, handoff, or state that contributes disproportionate waiting, failure, or cost.
- Alignment: a way to reason about where observed behavior matches or deviates from expected behavior.

## Adaptation Notes

The source literature is broader than auto-orchestrators and includes business-process analysis, ProM, inductive mining, alignments, organizational perspectives, time perspectives, and predictive analytics. This local skill narrows that theory into executable design work for agent orchestration:

- It emphasizes trace ids, task ids, tool calls, retry counts, state snapshots, decision reasons, and artifact references.
- It treats logs as design evidence for improving orchestrator templates and runtime controls.
- It avoids generic process-mining tutorial content and focuses on actions an agent can take during architecture, debugging, instrumentation, and improvement work.
