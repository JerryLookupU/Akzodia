---
name: 47-retrieval-augmented-generation
description: Use when designing an auto-orchestrator that must ground generation, decisions, tool plans, or answers in retrieved external knowledge; especially when freshness, provenance, hallucination control, evidence inspection, or updatable non-parametric memory matters.
---

# Retrieval-Augmented Generation For Auto-Orchestrators

## When To Use

Use this skill when an orchestrator should combine model reasoning with explicit retrieved knowledge instead of relying only on model parameters:

- The task is knowledge-intensive and users would reasonably expect access to current documents, policies, manuals, logs, cases, code, research, or domain records.
- The orchestrator must cite or inspect evidence behind an answer, route decision, plan, diagnosis, or generated artifact.
- The knowledge base changes faster than the model can be retrained or fine-tuned.
- Hallucination risk is material and the design needs grounding, abstention, or evidence-quality controls.
- The workflow needs to aggregate multiple retrieved passages, not simply extract one span or copy one previous case.
- The system must tune retrieval depth, reranking, chunking, or index refresh as part of orchestration quality.

Typical auto-orchestrator fits include support agents grounded in policies, research agents using source corpora, coding agents grounded in repo docs, incident responders using runbooks and traces, evaluation agents checking claims against evidence, and domain assistants backed by changing regulated knowledge.

## Workflow

1. Define the knowledge-intensive decision point.
   State what the orchestrator must produce and why parametric memory alone is insufficient. Mark whether retrieval is needed for factual answering, plan construction, claim verification, tool selection, policy compliance, freshness, or provenance.

2. Separate parametric and non-parametric memory.
   Treat the model as parametric memory for language, reasoning priors, and synthesis. Treat the index as non-parametric memory for inspectable facts, current records, source-specific constraints, and evidence. Do not blur these roles: retrieved text is the grounding substrate, not decoration.

3. Build the retrieval corpus contract.
   Choose source collections, freshness rules, access controls, redaction rules, and update cadence. Chunk documents around reusable units of meaning, preserve source metadata, and keep enough context for attribution. Record version, timestamp, owner, and policy status for each indexed item.

4. Design retrieval for the orchestration action.
   Convert the user/task state into retrieval queries that match the needed evidence. Use dense retrieval for semantic matches, lexical retrieval for exact entities or policy terms, and hybrid retrieval when both matter. Add reranking when false positives are costly.

5. Set retrieval depth and evidence admission rules.
   Retrieve enough candidates to cover ambiguity, then admit only passages that meet relevance, authority, recency, tenant, and safety constraints. Track `top_k`, score thresholds, source diversity, and fallback behavior. More documents can improve coverage but increase latency, cost, and distraction.

6. Condition generation or planning on admitted evidence.
   Pass the task, constraints, and selected passages into the generator or planner. Require outputs to distinguish grounded claims from inferred synthesis. For multi-source answers, aggregate compatible evidence and surface conflicts instead of forcing a single unsupported answer.

7. Validate grounding before acting.
   Check that important claims, route choices, tool parameters, and compliance decisions are supported by admitted evidence. Reject or repair outputs with missing citations, contradicted evidence, stale sources, irrelevant passages, or unsupported leaps. Use abstention or clarification when retrieval cannot supply useful evidence.

8. Keep the index hot-swappable.
   Make index replacement or refresh an operational path, not a research project. Verify that behavior changes when the corpus version changes. Rebuild embeddings, metadata filters, and caches as part of the release process, and test representative freshness-sensitive queries.

9. Instrument retrieval and generation quality.
   Log query, retrieved ids, admitted evidence, scores, generated output, citations, validation result, latency, cost, and user/evaluator feedback. Use these traces to tune chunking, query rewriting, reranking, `top_k`, corpus coverage, and abstention policy.

10. Close the learning loop without poisoning memory.
   Store successful evidence patterns and failure cases, but do not automatically index generated answers as truth. Index source documents, verified summaries, or reviewed lessons with provenance. Keep stale, biased, low-authority, or tenant-specific content from contaminating general retrieval.

## Failure Modes

- Retrieval theater: retrieved passages are shown or appended, but the orchestrator does not actually condition decisions on them.
- False grounding: the answer cites a source that is topically related but does not support the specific claim or action.
- Stale index: the model appears current because it retrieves documents, but the indexed corpus is old, incomplete, or unversioned.
- Chunking loss: chunks are too small to preserve meaning or too large to isolate relevant evidence.
- Over-retrieval: too many passages dilute attention, raise cost, and let weak evidence crowd out authoritative sources.
- Under-retrieval: too few passages miss conflicting evidence, minority variants, or necessary policy exceptions.
- Retriever mismatch: dense search misses exact legal, code, product, or entity terms; lexical search misses semantic paraphrases.
- Unchecked source bias: the corpus contains incorrect, biased, adversarial, or low-authority material and the orchestrator treats it as truth.
- Memory poisoning: generated outputs, user claims, or unreviewed notes are indexed as authoritative source material.
- Provenance collapse: citations point to documents but not to the passages, versions, or metadata needed for audit.

## Boundaries

Do not use this skill merely because a chatbot has a vector database. Use it when retrieval changes orchestration behavior and grounding quality matters.

Do not use RAG as a substitute for formal verification, deterministic policy enforcement, permissions checks, or human approval when those are required. Retrieval supplies evidence; it does not make an unsafe action safe.

Do not force RAG when the task is stable, fully contained in the prompt, purely computational, or better handled by structured APIs, databases, rules, or direct tool execution.

Do not assume retrieval eliminates hallucination. It reduces risk only when corpus quality, evidence admission, generation constraints, and grounding validation are designed together.

Use case-based reasoning when the main asset is prior solved episodes and adaptation logic. Use RAG when the main asset is explicit external knowledge that the orchestrator must retrieve, inspect, aggregate, cite, or refresh.
