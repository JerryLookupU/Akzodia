# Source Notes

## Assigned Source

- `auto_orchestrator_theory_txt_pack_v2/原文目录/02_左手_流程执行/14_Petri_网理论__Petri_Nets/supplement_www_pnml_org.txt`
- Captured page: PNML.org, "Petri Net Markup Language - Home Page", last update shown as April 1, 2026.
- Nature of source: standards and interchange-format supplement, not a full textbook chapter.

## What The Source Contributes

- PNML.org is presented as the reference site for Petri Net Markup Language under ISO/IEC 15909 Part 2.
- ISO/IEC 15909 Part 1 defines the semantic model of Petri nets and includes High-Level Petri Nets, Symmetric Nets, and Place/Transition Nets.
- Part 2 defines abstract and concrete syntax for those net types, with UML for abstract syntax and RELAX NG for concrete PNML grammar.
- PNML separates general Petri-net features from type-specific features.
- A Petri Net Type Definition (PNTD) is used for type-specific features, and each net type declares its own namespace URI.
- Convention documents can define features reused by more than one net type.
- User-defined extensions may not be standard-compatible unless recognized by the standard or the receiving tool.
- The site hosts metamodels, grammars, examples, tools, and papers for PNML.

## Supplemented Operational Model

The assigned source did not include enough basic Petri-net execution semantics to make an auto-orchestrator skill executable. The distilled skill therefore supplements the PNML source with standard Petri-net working concepts:

- Places hold tokens and represent conditions, resources, buffers, queues, or control states.
- Transitions are atomic events.
- A marking is the token distribution over places and acts as the current state.
- A transition is enabled when input places contain enough tokens and any guard is satisfied.
- Firing consumes input tokens and produces output tokens according to arc weights.
- Common orchestration checks include reachability, deadlock, liveness, boundedness, conservation, conflict, and concurrency.

Supplemental reference points used for this operational model:

- PNML.org: https://www.pnml.org/
- ISO/IEC 15909 listing for Petri net standards, as referenced from PNML.org.
- Public Petri-net teaching and overview materials that consistently define places, transitions, tokens, markings, enabling, and firing, including:
  - https://petrinet.org/
  - https://academic.oup.com/bib/article/8/4/210/221500

## Distillation Choices

- The skill is oriented toward auto-orchestrator design, not mathematical proof or historical survey.
- PNML details are kept as interchange and portability guidance, because the assigned source mostly concerns PNML standardization.
- The workflow uses Petri-net vocabulary only where it directly helps design, verify, or repair orchestrated execution.
- No long quotations were used; source facts are paraphrased.
