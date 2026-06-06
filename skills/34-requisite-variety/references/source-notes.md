# Source Notes: Requisite Variety

## Manifest Metadata

- Entry id: `34`
- Title: `Ashby 控制论 / Requisite Variety`
- Skill name: `34-requisite-variety`
- Source files:
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/34_Ashby_控制论__Requisite_Variety/01_pespmc1_vub_ac_be.txt`
  - `auto_orchestrator_theory_txt_pack_v2/原文目录/06_执行中枢_控制反馈/34_Ashby_控制论__Requisite_Variety/03_ashby_info.txt`

## Source Basis

The source is W. Ross Ashby's *An Introduction to Cybernetics* (1956), electronically republished by Principia Cybernetica. The manifest includes a short metadata page and a long OCR text of the book.

The skill is distilled mainly from Part III, chapters 10-12:
- Chapter 10 frames regulation as protecting essential variables from disturbances.
- Chapter 11 states the law of requisite variety and connects regulation to information channels.
- Chapter 12 turns the law into regulator design: given outcome variables, acceptable states, environment, and disturbances, form a regulator that keeps outcomes within bounds.

## Distilled Concepts

- `D`: disturbances. In orchestrator design these are task classes, input defects, hidden state, tool failures, policy conflicts, latency/cost pressure, and other external variation.
- `R`: regulator responses. These are route choices, specialist agents, tool choices, prompts, guardrails, retries, approval gates, refusals, and scope reductions.
- `T`: the transformation or environment through which disturbance plus response produces an outcome. This includes model limits, tool contracts, permissions, APIs, runtime state, and user constraints.
- `E`: essential outcome variables. For orchestrators these include correctness, safety, completion, cost, latency, data integrity, and trust.
- `h`: the acceptable region for `E`.

Ashby's core design claim for this skill: the variety reaching the outcome can be forced down only by corresponding regulator variety, unless the environment or passive constraints already block enough disturbance variety. For orchestration, this means failures are often caused by a mismatch between what the runtime can encounter and what the controller can observe and vary.

## Executable Interpretation For Auto-Orchestrators

Use the law as a design audit:

1. Define what must remain controlled (`E`) and the acceptable band (`h`).
2. Enumerate distinguishable disturbances (`D`) that threaten those outcomes.
3. Identify the regulator's actual response repertoire (`R`) and its sensing/motor channels.
4. Compare rows of disturbance cases with columns of responses.
5. If distinct disturbances require distinct responses, ensure the orchestrator can both distinguish and execute them.
6. Prefer reducing required variety before adding control machinery: schemas, constraints, standard task boundaries, input validation, and passive blocking.
7. Add branches, subagents, tools, or approvals only when tied to a named disturbance and a controlled outcome.

## Useful Source Anchors

- `01_pespmc1_vub_ac_be.txt`: identifies Ashby as a founder of cybernetics and systems theory, and lists the law of requisite variety among his fundamental ideas.
- `03_ashby_info.txt`, chapter 7: variety is a property of a set of distinguishable possibilities; constraint reduces possible variation.
- `03_ashby_info.txt`, section 10/6: a regulator blocks the flow of variety from disturbance to essential variables.
- `03_ashby_info.txt`, sections 11/6-11/7: only variety in the regulator can force down variety in outcomes; variety can destroy variety.
- `03_ashby_info.txt`, section 11/11: regulator capacity is bounded by communication capacity through the relevant channel.
- `03_ashby_info.txt`, sections 11/17-11/21: compound disturbances, noise, initial state, compound targets, and internal complexity can all be represented by vector forms of `D`, `E`, and related variables.
- `03_ashby_info.txt`, sections 12/1-12/2: regulator design begins with `E`, `h`, `T`, and `D`; sensory and motor restrictions make full regulation impossible.

## Metadata Completeness

Metadata was complete for distillation: the manifest entry provided id, title, skill name, skill directory, and source files. No supplemental web or external book lookup was required.
