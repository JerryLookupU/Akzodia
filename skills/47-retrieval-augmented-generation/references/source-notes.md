# Source Notes

## Portable Runtime Policy

This file is packaged inside this skill directory. It is a portable provenance and source-summary note, not an external dependency list.

- Normal skill execution must use `SKILL.md` as the executable contract.
- Do not require the user or agent to open external books, websites, source reports, crawl snapshots, local mirror paths, or parent-directory files.
- If source audit is requested, use this file as the local source-trace summary.
- The method, gates, output formats, boundaries, and recovery rules needed at runtime are internalized in `SKILL.md`.
## Manifest Entry

- id: 47
- title: Retrieval-Augmented Generation
- skillName: 47-retrieval-augmented-generation

## Source Basis

Original source files were used during distillation, but their machine-local paths are intentionally not stored here. The executable content has been internalized into `SKILL.md`.

## Bibliographic Basis

The source is Patrick Lewis, Ethan Perez, Aleksandra Piktus, Fabio Petroni, Vladimir Karpukhin, Naman Goyal, Heinrich Kuettler, Mike Lewis, Wen-tau Yih, Tim Rocktaeschel, Sebastian Riedel, and Douwe Kiela, "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks," arXiv:2005.11401.

## Distilled Theory

The paper frames retrieval-augmented generation as a hybrid memory architecture. A pre-trained seq2seq generator provides parametric memory, while a dense vector index of text passages provides explicit non-parametric memory. The retriever selects top candidate documents for an input, and the generator conditions on the input plus retrieved passages.

The motivation is practical: parametric models can store factual knowledge but cannot easily update that knowledge, expose provenance, or avoid hallucinations on knowledge-intensive tasks. A non-parametric memory can be revised, expanded, inspected, and replaced.

The paper introduces two generation formulations:

1. RAG-Sequence uses the same retrieved document across the generated sequence.
2. RAG-Token can condition different generated tokens on different retrieved documents.

For auto-orchestrators, this maps to two design options. A single-source workflow uses one admitted source set as grounding for the whole answer or plan. A multi-source workflow lets different parts of the output draw on different evidence, but requires stronger citation and consistency checks.

The retrieval mechanism matters. The source uses Dense Passage Retrieval and maximum inner product search over passage embeddings, with top-k retrieval. It compares learned dense retrieval, frozen retrieval, and BM25-style lexical retrieval. The broader design lesson is that retrieval must match the task: semantic retrieval helps many open-domain tasks, while exact lexical matching can be better for entity-heavy fact verification.

RAG improves open-domain question answering and knowledge-intensive generation by combining the flexibility of generated answers with open-book evidence access. The paper reports that RAG generations are more factual, specific, and diverse than a parametric-only BART baseline on generation tasks.

The index hot-swapping result is especially important for orchestrator design. The authors replace an older Wikipedia index with a newer one and show that answers follow the index version without retraining the model. This supports a runtime architecture where external knowledge can be refreshed independently from the model.

The paper also identifies a boundary: the external corpus may be incomplete, wrong, or biased. RAG can reduce hallucination and improve interpretability, but it can also ground outputs in flawed sources. This makes corpus governance, source metadata, evidence validation, and abstention policy core parts of the orchestration design.

## Auto-Orchestrator Translation

- The retriever becomes the orchestrator's evidence acquisition layer.
- The non-parametric memory becomes a versioned, inspectable corpus of policies, docs, traces, cases, code, research, or records.
- The generator becomes the synthesis/planning layer that must condition on admitted evidence.
- Top-k retrieval becomes an orchestration control: larger k improves coverage but raises latency and distraction risk.
- Index hot-swapping becomes a deployment pattern for freshness-sensitive systems.
- Provenance becomes a runtime contract: every grounded decision should carry source ids, versions, and passage-level support.
- Retrieval logs become feedback for improving chunking, query construction, reranking, filters, and abstention.

## Source Completeness

The manifest metadata and source file were sufficient. No external supplementation was needed. Cangjie was unavailable in this runtime, so the skill was distilled with book2skill plus skill-creator-style fallback.

## Book-Derived Essence Capsules

These capsules preserve the source-specific frame that differentiates this skill from generic orchestration advice. They are local audit material: cite them when provenance or source context is requested, but execute the skill from `SKILL.md`.

### BDE-core-framework

- Context: Retrieval-Augmented Generation sources and local RAG entry. This capsule records the central framework that should shape the skill's runtime behavior.
- Key fragment: Query -> retrieve -> rerank -> ground -> generate -> cite -> evaluate. Retrieval changes the model’s evidence boundary.
- Operational use: Use this frame as the first modeling lens before applying any generic workflow, checklist, or output template.
- Boundary: Do not use RAG to answer questions whose needed evidence is absent, stale, inaccessible, or not attributable.
- Local citation: `references/source-notes.md#BDE-core-framework`

### BDE-deep-idea

- Context: This is the source-specific thought that prevents the skill from collapsing into ordinary planning or summarization.
- Key fragment: RAG is not “add search”; it is a controlled evidence pipeline that must preserve source relevance, attribution, and answerability.
- Operational use: Use this idea to decide what the skill should emphasize, what evidence it should request, and what mistakes it should catch.
- Boundary: Do not expand the idea beyond the named source frame; keep modern application claims tied to the workflow in `SKILL.md`.
- Local citation: `references/source-notes.md#BDE-deep-idea`

### BDE-discovery-method

- Context: This capsule turns the source theory into a diagnostic method for finding structure, failure, or leverage in a concrete user problem.
- Key fragment: Define corpus boundary, chunking, query transformation, recall target, reranking, citation policy, refusal rules, freshness, and evaluation set.
- Operational use: Use these questions as the discovery pass before recommendations, design changes, or implementation steps.
- Boundary: If the required observations are unavailable, state assumptions or ask for the missing evidence instead of inventing certainty.
- Local citation: `references/source-notes.md#BDE-discovery-method`

## Internalization Map

- Runtime method, activation gates, response shape, and failure boundaries live in `SKILL.md`.
- Source provenance, compressed context, and audit-only capsules live in this file.
- Test expectations live in `test-prompts.json` and should assert that the skill works without external material.
- `audit.json` records closure status and must point to `references/source-notes.md` rather than outside paths.

## Local Citation Guidance

When a user asks where a rule came from, cite this local file and the relevant book-derived capsule: `references/source-notes.md#BDE-core-framework`, `references/source-notes.md#BDE-deep-idea`, or `references/source-notes.md#BDE-discovery-method`. Do not ask the user to open original books, websites, crawl folders, local mirrors, source reports, parent directories, or cross-skill files.
