---
name: 04-work-breakdown-structure
description: Use when designing or auditing an auto-orchestrator plan that needs a deliverable-oriented work breakdown, 100% scope coverage, WBS dictionary, ownership mapping, and traceable handoff into schedule, cost, risk, or execution control. Trigger on requests to decompose a project, convert scope into work packages, build a WBS/CWBS-like hierarchy, prevent scope gaps/overlap, or assign agent work from deliverables rather than tasks.
---

# Work Breakdown Structure

## When To Use

Use this skill when the orchestration problem is bigger than a task list and needs a stable scope spine:

- A user asks to decompose a project, program, product, migration, research effort, or multi-agent build into manageable work units.
- You need a common reference for agents, schedules, costs, risks, acceptance checks, and status rollups.
- The plan has multiple performers, vendors, subagents, teams, repositories, workstreams, or ownership boundaries.
- Scope creep, duplicated work, missing deliverables, unclear assignments, or untraceable progress are likely.
- A task-oriented plan is already causing confusion and should be rebuilt around outcomes.

Prefer WBS before detailed scheduling. A WBS defines what must be delivered; schedules and task networks define how and when work happens.

## Workflow

1. Anchor the scope.
   - Collect the charter-equivalent inputs: objective, success criteria, explicit exclusions, constraints, required outputs, stakeholder promises, contracts or specs, and lifecycle phases if relevant.
   - Name the Level 1 element as the whole project outcome. Treat it as 100% of authorized scope.
   - If source scope is unstable, create a preliminary WBS and mark the assumptions that must be revisited before baselining.

2. Build a deliverable-oriented hierarchy.
   - Decompose by products, services, data, decisions, capabilities, documents, or verifiable results.
   - Use nouns or noun phrases for elements. Avoid verbs such as "design", "build", "test", "review" unless the deliverable is itself a service or controlled support function.
   - Include enabling deliverables needed for management and control, such as project management, systems integration, assurance, documentation, risk management, evaluation, and operations support.
   - Stop decomposing a branch when its child elements are small enough to assign, estimate, verify, risk-rate, and track. Different branches may stop at different depths.

3. Enforce the 100% rule.
   - For each parent, verify that its children sum to all of the parent scope and no more.
   - Scan from requirements to WBS to find uncovered requirements.
   - Scan from WBS to requirements to find unauthorized work.
   - Ensure each deliverable appears in exactly one branch unless it is a shared enabling function with an explicit interface.

4. Create a WBS dictionary.
   - For every element, record: code, title, parent, description, included work, excluded work, acceptance/completion criteria, interfaces, owner, source requirement/spec reference, risk notes, and reporting or charge tag if relevant.
   - Lower-level elements need more detail than upper-level summaries.
   - Use the dictionary to remove ambiguity, overlap, and hidden assumptions before assigning agents.

5. Map performers without letting performers shape the tree.
   - Assign owners after the product hierarchy is coherent.
   - Use a responsibility matrix that maps WBS elements to agents/teams/tools.
   - If a contractor/subagent owns only part of a branch, make its contract/subplan an extension traceable to the parent WBS element.
   - Put organizational, vendor, repository, geography, or phase breakouts at the lowest useful level, not as top-level categories unless they are true deliverables.

6. Derive execution controls from the WBS.
   - Turn lowest-level WBS elements into work packages or planning packages.
   - Derive activities, milestones, dependencies, and schedule networks from those packages.
   - Attach budgets, effort estimates, resource needs, quality gates, risks, and status reports to WBS codes.
   - Roll status up through the hierarchy so progress, variance, blockers, and risks remain traceable to deliverables.

7. Baseline and change-control the structure.
   - Label drafts as preliminary until scope is stable enough for execution control.
   - Once baselined, change WBS elements only with a recorded rationale, affected requirements, schedule/cost/risk impacts, and approval owner.
   - Update the WBS dictionary whenever a WBS element changes.

## Failure Modes

- Task WBS: the hierarchy is made of activities or phases, so no one can verify what has actually been delivered.
- Org-chart WBS: teams, centers, vendors, or subagents become top-level branches and fragment integrated deliverables.
- Tool-shaped WBS: the scheduler, issue tracker, repo layout, or budget account structure dictates the scope model.
- Copy-paste WBS: an old template is reused without removing inherited mistakes, gaps, or irrelevant branches.
- Missing dictionary: titles look clear but acceptance criteria, interfaces, and exclusions are ambiguous.
- Broken 100% rule: child elements omit scope, include extra scope, or duplicate work under multiple parents.
- Wrong hierarchy: a peer deliverable is nested under another deliverable only because it is sequenced later or owned by the same performer.
- Premature baseline: volatile concept work is locked into accounting/reporting codes before content stabilizes.
- No transition path: WBS exists as a diagram but schedule, cost, risk, status, and agent assignments are not keyed to WBS elements.

## Boundaries

- WBS is not a schedule. Do not use it to encode task order, dates, critical path, or sprint sequencing; derive those after scope is decomposed.
- WBS is not an organizational breakdown. Use ownership mapping separately.
- WBS is not a requirements document. It must trace to requirements, but it does not replace them.
- WBS is not enough for small one-person tasks where a short checklist would be clearer.
- WBS should not force every branch to the same depth. Decompose to the level needed for management, risk, estimation, and verification.
- WBS can include enabling work, but only when that work is necessary to deliver or control the project and has clear boundaries.
