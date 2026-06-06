# Source Notes

Primary assigned source:
- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/18_排队论__Queueing_Theory/supplement_web_mit_edu.txt`
- Snapshot source URL recorded in that file: `https://web.mit.edu/urban_or_book/www/book/chapter4/4.1.html`

Local metadata consulted:
- `auto_orchestrator_theory_txt_pack_v2/原文目录/03_右手_调度并发资源/18_排队论__Queueing_Theory/metadata.json`
- `auto_orchestrator_theory_txt_pack_v2/90_书单总索引.txt`
- `auto_orchestrator_theory_txt_pack_v2/10_核心内容补充/03_右手_调度并发资源核心内容.txt`

## Source-Derived Points

- Queueing analysis starts by choosing or building a mathematical model for a real service system.
- The modeling step necessarily simplifies, approximates, and often relies on assumptions about behavior that may not be directly evidenced.
- Queueing results should usually be treated as approximate indicators for real systems, useful for finding operating weaknesses, improvement directions, and rough values of controllable variables.
- Many exact queueing results assume equilibrium or steady-state behavior; transient and nonstationary behavior is harder.
- There is a tradeoff between realistic models that may be analytically intractable and simplified models whose validity may be limited.
- Queueing theory is strong at estimating expected waiting time, number of users/jobs in the system, server busy/idle fraction, and busy-period duration.
- It is less generally strong at producing full probability distributions, except in special cases or with transform and numerical methods.
- The source highlights Poisson arrivals and exponential interarrival/service assumptions as common foundations for many exact results.

## Auto-Orchestrator Distillation

For orchestrator design, the theory becomes a capacity-control workflow:

- Model tasks, tool calls, review requests, test runs, or subagent jobs as arrivals.
- Model workers, API permits, browser sessions, review lanes, test environments, and database connections as servers.
- Use `lambda`, `mu`, `c`, and `rho = lambda / (c * mu)` as first-pass congestion variables.
- Treat high utilization as a warning sign because wait time can rise sharply near full capacity.
- Separate queues by task class or urgency when mixed work would cause priority inversion or long-job blocking.
- Add backpressure and retry budgets so incidents do not multiply arrival load.
- Use measurement and simulation when steady-state or exponential assumptions are too weak.

## Supplemented Context

The representative book named in local metadata is Leonard Kleinrock, *Queueing Systems, Volume I: Theory*, but the available assigned source is a MIT web supplement rather than the book text. To make the skill executable for auto-orchestrator design, the skill supplements the source with standard queueing concepts also reflected in the local pack notes:

- Little's Law as a steady-flow sanity check.
- Utilization `rho`, arrival rate `lambda`, service rate `mu`, and worker count `c`.
- Queue discipline choices such as FIFO, priority queues, aging, bounded queues, admission control, and backpressure.
- Engineering observability metrics: arrival rate, service time, queue length, wait time, sojourn time, utilization, idle time, retries, timeouts, and abandonment.

No long source quotations were copied into the skill.
