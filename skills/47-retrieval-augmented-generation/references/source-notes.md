# Source Notes

## Manifest Entry

- id: 47
- title: Retrieval-Augmented Generation
- skillName: 47-retrieval-augmented-generation
- skillDir: distilled_skills/auto_orchestrator_theory_skills_v1/skills/47-retrieval-augmented-generation

## Source Files

- `auto_orchestrator_theory_txt_pack_v2/原文目录/08_记忆_知识经验复用/47_检索增强生成__Retrieval_Augmented_Generation/01_arxiv_org.txt`

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
