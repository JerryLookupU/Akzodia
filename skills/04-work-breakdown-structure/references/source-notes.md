# Source Notes: Work Breakdown Structure

## Sources Used

- `auto_orchestrator_theory_txt_pack_v2/原文目录/01_头_任务拆解与分类/04_WBS_工作分解结构__Work_Breakdown_Structure/01_ntrs_nasa_gov.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/01_头_任务拆解与分类/04_WBS_工作分解结构__Work_Breakdown_Structure/02_soma_larc_nasa_gov.txt`
- `auto_orchestrator_theory_txt_pack_v2/原文目录/01_头_任务拆解与分类/04_WBS_工作分解结构__Work_Breakdown_Structure/03_www_pmi_org.txt`

## Metadata

- NASA source: `NASA Work Breakdown Structure (WBS) Handbook`, NASA/SP-20210023927, November 2021. The NTRS record also points to a 2019 NASA/SP-3404 record acquired January 15, 2020; the full source text provided is the November 2021 revision.
- PMI source: Shelly A. Brotherton, Robert T. Fried, and Eric S. Norman, `Applying the work breakdown structure to the project management lifecycle`, PMI Global Congress 2008, published October 19, 2008.

## Distilled Principles

- WBS is a product or deliverable-oriented hierarchy for the total approved scope. It describes the "what" of the project, not the execution sequence.
- The top element represents the entire project. Descending levels provide increasingly detailed elements until work can be assigned, estimated, verified, and controlled.
- The 100% rule applies at every parent-child relationship: child scope must equal all parent scope and must not include unauthorized work.
- A WBS dictionary is a separate control artifact that defines each element, removes ambiguity, records interfaces, and links the element to requirements/specifications and reporting tags.
- A single WBS can support technical, schedule, cost, performance, risk, and communication management when those systems share WBS element codes.
- Schedules should be derived from the WBS by decomposing lowest-level work packages into activities, milestones, dependency networks, and schedule baselines.
- Ownership should be mapped to WBS elements through a responsibility matrix. Organizational structure should not determine the WBS hierarchy.
- Contractor, partner, or subagent work should extend and trace back to the project WBS rather than becoming a disconnected plan.
- WBS depth is contextual. High-risk, high-cost, complex, or management-critical branches may need more decomposition than simple branches.
- After scope baseline, WBS changes require change control and dictionary updates.

## Auto-Orchestrator Translation

- Treat the WBS as the orchestration spine. Every agent assignment, artifact, status update, risk, and acceptance check should reference a WBS code.
- Use nouns for agent work packages: `evaluation harness`, `data ingestion adapter`, `policy test corpus`, `deployment runbook`. Derive verbs later as tasks.
- Keep top-level branches focused on deliverables or enabling controls, not on subagent names, tools, repos, or calendar phases.
- Use a WBS dictionary to make each agent handoff inspectable: included scope, excluded scope, inputs, outputs, acceptance criteria, dependencies, owner, and review point.
- For multi-agent plans, use the 100% rule to detect missing deliverables and duplicated work before dispatching agents.
- Use scope relationship diagrams or parent-child plus dependency maps when a flat outline hides inclusion and sequence differences.

## Failure Signals From Sources

- Prior WBS templates can import old mistakes.
- Phase-oriented or function-oriented elements such as `Phase C`, `Engineering`, `Manufacturing`, or `Testing` obscure product scope.
- Breaking out centers, vendors, or teams too high in the hierarchy fragments deliverable rollups.
- Incorrect hierarchy occurs when parent-child structure does not reflect real inclusion; sequencing or shared ownership is not enough to make something a child.
- A WBS without a dictionary leaves content boundaries unclear and weakens scheduling, cost, risk, and performance controls.

## Short Source Anchors

- NASA describes WBS as a product-oriented family tree for hardware, software, services, data, and other deliverables.
- PMI emphasizes deliverable-oriented hierarchical decomposition and the 100% rule.
- PMI distinguishes WBS scope from processes, schedule, and timing.
- NASA emphasizes the WBS dictionary, coding, control accounts, change control, and integration with cost/schedule/risk systems.
