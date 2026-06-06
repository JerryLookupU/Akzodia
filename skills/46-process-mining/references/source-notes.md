# Source Notes

## Manifest Entry

- id: `46`
- skillName: `46-process-mining`
- title: `过程挖掘 / Process Mining`
- sourceFiles:
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/08_记忆_知识经验复用/46_过程挖掘__Process_Mining/supplement_processmining_org.txt`

## Source Coverage

The source is a processmining.org book page for Wil van der Aalst's process mining books:

- `Process Mining: Data Science in Action`, second edition, Springer, 2016.
- `Process Mining: Discovery, Conformance and Enhancement of Business Processes`, Springer, 2011.

The page describes process mining as a discipline that uses event logs from information systems to bridge business process modeling and business intelligence/data science. It emphasizes practical analysis from recorded execution data rather than fictional or assumed process descriptions.

## Distilled Concepts

- Event logs are the primary evidence object. A useful log must reconstruct cases, activities, and ordering over time.
- Process discovery learns process models from raw event data.
- Conformance checking compares observed behavior with an expected model or policy.
- Enhancement extends beyond control-flow discovery into bottlenecks, organizational/resource views, time perspectives, and operational support.
- Operational support includes detecting problems, predicting execution issues, and guiding interventions from event data.
- Tooling and practice matter: the source highlights ProM, commercial tools, real-life data sets, and practical application.

## Auto-Orchestrator Translation

For auto-orchestrator design, process mining becomes a workflow for turning historical runs into design evidence:

- Treat each user request, task, job, incident, or agent run as a case.
- Treat orchestrator steps, tool calls, retries, approvals, failures, handoffs, and completions as activities.
- Use timestamps and attributes to expose variants, bottlenecks, loops, conformance deviations, and predictive intervention points.
- Convert mining findings into routing, retry, validation, escalation, instrumentation, and operational-support changes.

## Metadata Completeness

The manifest provides skill name, directory, title, and one source file. The source provides theory identity, author, books, publication years, scope, target audience, and core method families. No additional external supplementation was required.
