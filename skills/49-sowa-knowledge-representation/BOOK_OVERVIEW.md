# Book Overview

## Bibliographic Frame

- Book: `Knowledge Representation: Logical, Philosophical, and Computational Foundations`
- Author: John F. Sowa
- Publisher/source note from local landing page: Brooks Cole, copyright 2000, actual publication date 16 August 1999
- Local source scope: companion page, preface, table of contents, index, errata, and generated Markdown wrappers

## Source Scope

The local repository does not contain full prose for all printed chapters. It contains:

- `BOOK.md` as the generated book entry and reading order.
- `source-map.json` with five local source wrappers.
- `chapters/*.md` generated from landing page, errata, index, preface, and table of contents.
- `site-sowa/krbook/*.htm` originals for the same pages.

This overview therefore distills the book's explicit architecture, preface claims, topic map, examples, and index evidence. It avoids pretending to have read unavailable chapter prose.

## Adler Stage 0

### 1. Structural Reading

Sowa organizes KR as a bridge among logic, ontology, and computation:

1. Logic: history, representing knowledge in logic, varieties of logic, names/types/measures, unity across notations.
2. Ontology: categories, philosophical background, top-level categories, physical entities, abstractions, sets/collections/types/categories, space and time.
3. Knowledge representations: knowledge engineering, frames, rules/data, object-oriented systems, natural language semantics, levels of representation.
4. Processes: times, events, situations, procedures, concurrency, computation, constraints, change.
5. Purposes, contexts, and agents: purpose, context syntax/semantics, first-order and modal reasoning in contexts, encapsulated objects, agents.
6. Knowledge soup: vagueness, uncertainty, randomness, ignorance, limits of logic, fuzzy logic, nonmonotonic logic, theories/models/world, semiotics.
7. Knowledge acquisition and sharing: ontology sharing, conceptual schema, multiple paradigms, mapping representations, language patterns, acquisition tools.
8. Appendices: predicate calculus, conceptual graphs, KIF, ontology base, hotel reservation, library database, controlled English to logic.

### 2. Interpretive Reading

The book's operational thesis is that knowledge representation is not one notation. It is the engineering of a computable surrogate for real-world knowledge, constrained by:

- Formal inference: what follows, what contradicts, what defaults, what changes under new facts.
- Ontological commitment: what kinds of entities, roles, relations, processes, contexts, and purposes the system recognizes.
- Computational realization: what can be stored, queried, transformed, executed, shared, and audited.

This makes representation choice a design decision rather than a taste preference.

### 3. Critical Reading

Strengths:

- The triad of logic, ontology, and computation prevents both vocabulary-only ontologies and formalism-only logic.
- The table of contents forces dynamic and contextual issues into KR rather than leaving them outside the model.
- The index shows broad comparison across paradigms: rules, frames, SQL, Prolog, object systems, conceptual graphs, KIF, Petri nets, controlled language, fuzzy and nonmonotonic logic.
- The preface emphasizes informal specification analysis and ontology selection, which maps well to modern agent and knowledge-base design.

Limits:

- The available local source set is a map, not the full printed book.
- Some technologies in the index are historical, so the skill should preserve design principles rather than recommend legacy tools by default.
- The book's symbolic and ontological center must be complemented by modern retrieval, ML ranking, observability, and governance when building current agent systems.

### 4. Applied Reading

For Codex use, the book distills into one executable capability:

Choose and audit a knowledge representation by starting from reasoning and explanation needs, modeling domain ontology and context, deciding how uncertainty/defaults/change are handled, and building indexes that connect terms, concepts, rules, sources, examples, mappings, and explanations.

## Distilled Skill Direction

The final skill focuses on:

- Knowledge representation selection.
- Semantic and logical modeling.
- Ontology and context scoping.
- Process/change representation.
- Knowledge soup: vagueness, uncertainty, defaults, inconsistency.
- Interoperability across paradigms.
- Index-based knowledge engineering.
- Auditable explanations and revision conditions.

## Evidence Anchors

- `site-sowa/krbook/krpref.htm`: KR as logic + ontology + computation; knowledge engineers as making implicit knowledge explicit.
- `site-sowa/krbook/krtoc.htm`: seven-chapter architecture and appendices.
- `site-sowa/krbook/index.htm`: landing page links to logic, conceptual graphs, KIF, ontology, lexicon, processes, agents, roles, glossary.
- `site-sowa/krbook/krindex.htm`: subject index evidence for contexts, defaults, conceptual graphs, conceptual schemas, nonmonotonic logic, ontology sharing, Petri nets, semantic networks, SQL, Prolog, controlled English, theory revision, etc.
- `site-sowa/krbook/errata.htm`: confirms chapter/section structure and several technical topics.
