# Architecture Decision Record (ADR) index

**Initialized:** 2026-11-07  
**Updated:** 2026-11-08  
**Owner:** Project owner (ADRs 0002–0008 accepted; 0001 open)  
**Scope:** decisions for Sri Lankan legal-awareness application.

## Status key

- **PROPOSED:** written recommendation, not yet approved by owner.
- **ACCEPTED:** owner agreed after reviewing context/trade-offs; record approval date.
- **SUPERSEDED:** replaced by a new ADR linking to it; original retained for history.

## Index

| ID | Decision | Status | Date | Related risk |
|---|---|---|---|---|
| ADR-0001 | MVP topic scope after quality assessment | PROPOSED — DEFERRED | 2026-11-07 | R-02, R-04, R-15 |
| ADR-0002 | Versioned and approved legal source registry | ACCEPTED (2026-11-08) | 2026-11-07 | R-01, R-10, R-14 |
| ADR-0003 | One FastAPI modular backend; Flutter Android/Web clients | ACCEPTED (2026-11-08) | 2026-11-07 | R-07, R-08, R-09 |
| ADR-0004 | Language rollout is gated by language-specific validation | ACCEPTED (2026-11-08) | 2026-11-07 | R-03 |
| ADR-0005 | Minimize conversational data; backend secrets; no user accounts by default | ACCEPTED (2026-11-08) | 2026-11-07 | R-05, R-06 |
| ADR-0006 | Preserve historical and future law with dated, status-aware answers | ACCEPTED (2026-11-08) | 2026-11-08 | R-01, R-10 |
| ADR-0007 | Broader source catalogue with gated answer coverage | ACCEPTED (2026-11-08) | 2026-11-08 | R-01, R-02 |
| ADR-0008 | Adaptive PDF extraction with OCR and quality/approval gates | ACCEPTED (2026-11-08) | 2026-11-08 | R-01, R-02, R-14 |

**Existing product constraints, not a new ADR:** no autonomous legal actions; legal information only; source citations and evidence status; user reports; initial Android + Web target. These are already required by `PROJECT_PROMPT_UPDATED.md`.

## ADR template for future decisions

```markdown
# ADR-XXXX — Title
- Date:
- Status: PROPOSED / ACCEPTED / SUPERSEDED
- Context / drivers:
- Decision:
- Alternatives considered:
- Consequences and trade-offs:
- Security and privacy impact:
- Evidence / experiments / source links:
- Review or revisit condition:
- Supersedes / superseded by:
- Owner approval + date:
```

Update the index when statuses change. Don't alter an accepted ADR retroactively to conceal earlier choices.

## Source-first assessment extension — 2026-11-08

The owner agreed to broad source discovery and 20 subject labels before choosing the MVP. ADR-0007 is accepted; ADR-0001 remains open pending corpus quality and review evidence. This is not acceptance of a complete archive or of blanket AI answers. See `docs/phase-0/CORPUS_DISCOVERY_PLAN.md`.

## Batch 001 OCR architecture milestone — 2026-11-08

The owner expressly accepted ADR-0008 as a documented architecture decision and presentation story. This is supported by an initial local two-PDF OCR feasibility test, **not** a completed ingestion pipeline or legal correctness evaluation. See `ADR-0008-adaptive-extraction-and-ocr-quality-gates.md`.
