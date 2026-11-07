# Architecture Decision Register

Last updated: 2026-11-07

Record requirements and product boundaries separately from the architecture chosen to fulfill them. "Proposed" does not mean approved.

| ID | Topic | Type | Status | Next action |
|---|---|---|---|---|
| [ADR-0001](ADR-0001-no-autonomous-legal-actions.md) | No autonomous legal actions | Product/architecture boundary | **Accepted** | Verify scope in API design and tests |
| [ADR-0002](ADR-0002-evidence-grounded-rag.md) | Evidence-grounded RAG with backend verification | Architecture candidate | **Proposed** | Define safety invariants and compare baseline designs |
| [ADR-0003](ADR-0003-shared-backend.md) | One backend for Android and Web | Architecture candidate | **Proposed** | Evaluate Flutter Web against alternative web frontends |

## Explicitly undecided choices

- Exact frontend stack(s), authentication strategy, hosting/provider/region, vector and embedding model, hosted LLM, reranking, OCR, legal version-tracking process, language rollout, retention/deletion defaults, and release quality thresholds.
- No technology choice becomes **Accepted** solely because it appeared in the project prompt.

## Process

New significant choice → describe context/options → gather evidence → decide and date → test consequences → revisit if assumptions change. Retain history when superseded. Use `ADR_TEMPLATE.md`.
