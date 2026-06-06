# Source Notes

## Manifest Source

- `auto_orchestrator_theory_txt_pack_v2/原文目录/05_右脚_续跑保活恢复/30_SRE__Site_Reliability_Engineering/01_sre_google.txt`
- Source URL in file: `https://sre.google/sre-book/table-of-contents/`

The local source file contains the Google SRE book table of contents rather than full chapter text. It identifies the domain scope: embracing risk, service level objectives, eliminating toil, monitoring, automation, release engineering, simplicity, alerting, on-call, troubleshooting, emergency response, incident management, postmortems, testing, overload, cascading failures, reliable launches, communication, and production best practices.

## Supplemental Metadata

- Book: `Site Reliability Engineering: How Google Runs Production Systems`
- Editors: Betsy Beyer, Chris Jones, Jennifer Petoff, and Niall Richard Murphy
- Publisher: O'Reilly Media
- Public source: Google SRE book site at `https://sre.google/sre-book/`
- Supplemented pages consulted from the same official source family:
  - `https://sre.google/sre-book/service-level-objectives/`
  - `https://sre.google/sre-book/eliminating-toil/`
  - `https://sre.google/sre-book/monitoring-distributed-systems/`
  - `https://sre.google/sre-book/managing-incidents/`
  - `https://sre.google/sre-book/postmortem-culture/`
  - `https://sre.google/sre-book/handling-overload/`
  - `https://sre.google/sre-book/reliable-product-launches/`

## Distillation Rationale

The auto-orchestrator translation treats SRE as an operating discipline for agent and workflow platforms:

- SLOs convert user promises into measurable reliability policy.
- Error budgets give teams an explicit way to trade launch velocity against reliability work.
- Toil analysis prevents the orchestrator team from scaling production by adding manual intervention.
- Monitoring should page on user-impacting symptoms and keep cause signals available for triage.
- Incident response and postmortems turn failures into changes in system design, process, tests, and ownership.
- Overload handling and launch readiness make reliability a design-time concern rather than a post-incident patch.

The resulting skill is deliberately not a generic SRE summary. It is an executable checklist for designing reliability contracts, ownership, operational controls, and feedback loops around auto-orchestrators.
