# Source Notes

## Local Source

- `auto_orchestrator_theory_txt_pack_v2/原文目录/02_左手_流程执行/12_工作流理论__Workflow_Management/supplement_workflow_patterns_tue.txt`

## Metadata

This entry is a theory/paper entry rather than a single book.

Primary source represented by the local text:
- W.M.P. van der Aalst, A.H.M. ter Hofstede, B. Kiepuszewski, and A.P. Barros.
- "Workflow Patterns."
- Distributed and Parallel Databases, volume 14, issue 1, pages 5-51, published 2003.
- DOI: `10.1023/A:1022883727209`.
- The source text is a publisher PDF extraction from Eindhoven University of Technology, with document status "Published" and document version "Publisher's PDF."

## Distilled Claims

- Workflow process definitions specify activities and their execution order for case-driven business processes.
- The paper focuses on the control-flow perspective: sequence, branching, synchronization, loops, multiple instances, state-based routing, and cancellation.
- Workflow patterns express recurring business routing requirements independently of a specific workflow language.
- Basic constructs such as sequence, parallel split, synchronization, exclusive choice, and simple merge are widely supported, but their semantics can diverge when assumptions are violated.
- Advanced branching and merge patterns include multi-choice, synchronizing merge, multi-merge, and discriminator or n-out-of-m joins.
- Structural patterns distinguish arbitrary cycles from restricted structured loops, and implicit termination from explicit final-node termination.
- Multiple-instance patterns depend on whether instance count is known at design time, known at runtime before launch, unknown while running, or irrelevant because no synchronization is needed.
- State-based patterns such as deferred choice, interleaved parallel routing, and milestone require explicit state or equivalent cancellation/locking semantics.
- Cancellation patterns distinguish withdrawing one enabled activity from withdrawing an entire case and all descendant work.
- The paper's product comparison shows that direct support for advanced patterns was uneven; resorting to scripts, external triggers, or database manipulation obscures workflow semantics.

## Pattern Catalog For Orchestrators

- `Sequence`: run B after A completes.
- `Parallel split`: create multiple active branches from one point.
- `Synchronization`: wait for all expected parallel branches, assuming one signal per branch.
- `Exclusive choice`: choose exactly one branch from control data or a decision.
- `Simple merge`: reconverge alternatives that are never parallel.
- `Multi-choice`: select any number of branches from a set.
- `Synchronizing merge`: run downstream once after all actually selected branches complete.
- `Multi-merge`: run downstream once per incoming activation.
- `Discriminator`: release downstream on the first completion, ignore or drain the rest, then reset.
- `Arbitrary cycles`: allow repeat paths that may not be block structured.
- `Implicit termination`: finish when no work remains, rather than when a final node is reached.
- `Multiple instances without synchronization`: spawn independent child work.
- `Multiple instances with design-time knowledge`: fixed number of copies, then synchronize.
- `Multiple instances with runtime knowledge`: count known before launch, then synchronize.
- `Multiple instances without runtime knowledge`: count can grow while instances are running, then synchronize when closed and complete.
- `Deferred choice`: enable alternatives and let the first external event or started activity win.
- `Interleaved parallel routing`: all activities execute in arbitrary order, but not concurrently.
- `Milestone`: enable an activity only while the case is in a specific phase.
- `Cancel activity`: withdraw one enabled activity instance.
- `Cancel case`: withdraw the whole workflow instance and descendants.

## Auto-Orchestrator Translation

- Case: one orchestration run, such as a request, project, issue, incident, release, document, or conversation.
- Activity: an executable unit, such as a tool call, agent task, approval, test, edit, callback, timer, or deployment step.
- Token/thread: an active control-flow obligation, including queued, running, waiting, or enabled work.
- Branch predicate: structured condition that decides whether a branch is selected.
- Join contract: precise rule for how many signals are expected, which signals are ignored, and when downstream work fires.
- Spawned instance: repeated child activity sharing a definition but scoped to one case.
- Milestone/state place: a phase marker that enables and later withdraws work.
- Cancellation API: runtime mechanism for removing queued/running work and marking late results invalid.

## Distillation Choices

- Recast the paper's workflow-management-system evaluation into a modern auto-orchestrator design checklist.
- Emphasized semantic questions an orchestrator designer must answer: token count, duplicate signals, optional branches, runtime fan-out, state visibility, and cancellation behavior.
- Treated indirect implementations through code, event queues, triggers, or APIs as useful but risky because they hide semantics outside the workflow model.
- Omitted product-by-product historical details except for the general lesson that advanced routing support varies by runtime.
- Avoided long quotations; source content is paraphrased.
