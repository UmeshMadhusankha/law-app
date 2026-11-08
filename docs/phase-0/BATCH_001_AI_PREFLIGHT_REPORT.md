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

## Project-owner confirmation — 2026-11-08

The project owner reported checking **three selected discrepancies in the National Child Protection Authority Act**, agreeing with the observed `No act` → `Noact` and `paragraph (b)` → `paragraph (6)` differences and with the presence of errors in Penal Code section numbers in section 39. For the third item the owner's message did **not** independently specify the exact affected statutory identifiers; those candidate tokens remain in the AI-assisted preflight and require exact transcription before correction.

The corresponding three rows in `corpus/reviews/batch-001/OCR_PASSAGE_REVIEW.csv` are marked `FAIL` at the **inspected-span level only**. The other three HRCSL rows remain `NOT_REVIEWED`. No complete provisions or whole PDFs have been fully proofread. These are owner-reported confirmations, not a blinded reference-transcription benchmark.

### Scope, stopping rule, and consequence

The owner chose to stop additional manual sampling for now because of a ~10-hour/week development budget. This is a **resource-prioritization decision**, not evidence that the unchecked passages are correct. Keep both OCR derivatives **UNREVIEWED / NOT APPROVED_FOR_ANSWER**. The next sprint should focus on repeatable automatic extraction checks, with targeted manual review of provisions proposed for actual user-facing answers. Do not silently replace original PDFs or impute missing review results.
