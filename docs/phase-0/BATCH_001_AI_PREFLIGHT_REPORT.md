# Batch 001 — AI-assisted OCR quality preflight (2026-11-08)

**Status: preliminary engineering evidence, NOT legal-text approval.**  
**Related ADR:** ADR-0008. **Source files:** Batch 001 originals and derived OCR PDF hashes in `OCR_AI_PREFLIGHT_2026-11-08.csv`.  
**Method:** Six purposively selected provisions were compared using images of the original PDF pages and the corresponding OCR text layers. This is **not** an independent human review, a random sample, or a whole-document accuracy measurement. All six owner-review entries in `OCR_PASSAGE_REVIEW.csv` remain `NOT_REVIEWED`.

## Findings

| Document | Original PDF page / printed page | Provision | Visual source vs OCR | Risk triage |
|---|---|---|---|---|
| Child Protection Act | 6 / 5 | s.10 | `No act` became `Noact` | Low: merged words |
| Child Protection Act | 15 / 14 | s.29(2) | `paragraph (b)` became `paragraph (6)` | High: wrong internal reference |
| Child Protection Act | 19 / 18 | s.39, clause (a) of definition | `288B`, `360B`, `365B` became `288`, `3608`, `3658` | High: potentially invalid statutory identifiers |
| HRCSL Act | 3 / 1 | s.2(1), opening phrase | No mismatch detected in selected short span | Not a whole-passage PASS |
| HRCSL Act | 6 / 4 | s.10(a) | `(a)` became `(b)` and `with` became `wish` | High: clause identity |
| HRCSL Act | 19 / 17 | s.33(c) | `Judicial` became `Judictal` | Medium: institution name |

**Observed:** Five of six purposively chosen spans show an apparent OCR discrepancy; one short span had none detected. **Do not report 5/6 as an OCR error rate, accuracy score, or statistically representative result.**

## Engineering response

1. **Do not promote** either derived OCR PDF to `APPROVED_FOR_ANSWER`.
2. Keep immutable original PDFs and source/derivative SHA-256 hashes. Corrections belong in versioned derivatives, not overwritten source files.
3. Prioritize section and subsection identifiers, negations, dates, citations, and official institution names.
4. The project owner should complete `OCR_PASSAGE_REVIEW.csv` independently using original page images. These AI observations can be compared *after* their review to reduce confirmation bias.
5. Build a larger human-checked gold transcription set before estimating OCR word error rate, section-anchor accuracy, or readiness for retrieval.
6. Continue temporal legal-status verification independently of OCR validation.

## Reproduction and evidence

The CSV records exact PDF pages, printed pages, source and derivative hashes, short excerpts, and discrepancy categories. The separate downloadable evidence package in the project chat includes six rendered original pages. Images and PDFs have **not** been committed to this PR; avoid treating this text-only PR as a complete legal evidence archive. This preflight did not modify a PDF, rerun OCR, assess legal currency, or create approved RAG corpus records.

## Engineering milestone update

- **Decision:** Observations support the existing ADR-0008 quality gate; no new ADR.
- **Metrics:** Six purposively chosen spans inspected; five contain apparent anomalies. Word/character transcription accuracy and whole-document legal correctness **NOT MEASURED**.
- **Portfolio:** Initial failure taxonomy from real documents, not a completed production ingestion pipeline.
- **Pitch:** OCR can generate plausible but wrong statutory identifiers; verification is needed before indexing.
- **Next verification:** Independent manual confirmation, corrected derivative with new hash, then wider stratified sample.
