# Qdrant Batch Sync

## Role in the System

The Qdrant Batch Sync workflow is responsible for building and maintaining a semantic search index used for stock identification and lookup. It operates as an offline batch process and is not part of the real-time execution or alerting path.

This workflow enables flexible, typo-tolerant, and alias-aware stock resolution without impacting runtime system performance.

---

## Data Sources & Preparation

The batch process consumes structured reference data from the system’s master instrument dataset. Each record includes identifiers such as:
- Stock symbol
- Instrument name
- Exchange metadata
- Search aliases and alternate representations

Before vectorization, records are normalized and combined into a search-friendly textual representation.

---

## Embedding & Indexing Strategy

Prepared records are converted into dense vector embeddings using a language model optimized for semantic similarity. These embeddings are then inserted into a Qdrant vector store.

Key characteristics of the indexing strategy include:
- Full rebuilds to avoid stale or inconsistent vectors.
- Clear separation between source data and derived embeddings.
- Metadata preservation to support traceability and debugging.

---

## Usage Within the System

The resulting vector index is used by upstream workflows to:
- Resolve user-provided stock references.
- Handle spelling variations and partial matches.
- Improve intent interpretation during command processing.

This allows user-facing workflows to remain simple while relying on a robust search backend.

---

## Failure Handling & Safety

As a batch-oriented workflow:
- Failures do not impact real-time operations.
- Partial runs do not corrupt existing runtime state.
- Re-execution is safe and idempotent.

The system continues to function using the last known valid index if a batch run fails.

---

## Design Rationale

Semantic search was introduced to:
- Reduce friction in user input handling.
- Avoid brittle exact-match logic.
- Support natural interaction patterns without complicating core workflows.

By isolating vector operations into a batch process, the system preserves runtime reliability while benefiting from advanced search capabilities.

---

## Summary

The Qdrant Batch Sync workflow provides a scalable and resilient foundation for semantic stock identification. Its batch-oriented design ensures that advanced search functionality enhances the system without introducing runtime complexity or risk.
