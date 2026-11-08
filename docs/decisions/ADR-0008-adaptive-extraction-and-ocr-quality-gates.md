# ADR-0008 — Adaptive PDF text extraction and mandatory OCR quality gates

- **Date:** 2026-11-08
- **Status:** ACCEPTED (product owner explicitly endorsed the architectural principle on 2026-11-08)
- **Related:** ADR-0002 (approved legal sources), ADR-0006 (temporal legal status), ADR-0007 (gated AI-answer corpus)
- **Implementation:** Local OCR feasibility demonstrated on two Batch 001 files; automated ingestion integration **NOT IMPLEMENTED**.

## Context and problem

Batch 001 exposed two different failures behind the same 'PDF' label:

1. `SL-0039` (National Child Protection Authority Act, No. 50 of 1998): the 20-page original has no extractable text. It is a scanned image, not unusable law.
2. `SL-0003` (Human Rights Commission of Sri Lanka Act, No. 21 of 1996): the 21-page original has a text layer, but visible misrecognitions such as `PARLIAI{ENT` and `SRI T.,ANKA`. Presence of text alone is not an accuracy check.
3. The owner's attempted Windows command supplied a PDF directly to Tesseract, resulting in `Pdf reading is not supported` and a zero-byte failed output. Tesseract accepts image input; a PDF reader/rasterizer is required first.

Our application cannot safely index a legally significant provision if its extracted text may have misread words, negations, section numbers, dates, or cross-references.

## Decision

We adopt a **quality-gated, adaptive PDF processing pipeline**:

1. Keep an immutable original PDF, official-source URL, source ID, SHA-256 hash, original page count, and acquisition date.
2. Detect whether pages contain extractable text; additionally sample character quality and legal anchors. A nonempty or long text layer does **not** automatically pass.
3. Use direct text extraction for candidate high-quality digital PDFs. Use OCR for image-only pages. Re-OCR corrupted existing text separately, rather than assuming `skip pages with any text` is sufficient.
4. Preserve page IDs, image/PDF provenance, extraction method/version, source hash, and review state on every derived text record.
5. Compare sample pages visually with the original PDF and check crucial phrases, negations, dates, and provision identifiers against the page image. Flag uncertain lines for manual correction and reviewer approval.
6. Keep **EXTRACTED_UNVERIFIED** separate from **APPROVED_FOR_ANSWER**. Never index unreviewed OCR as approved legal-answer evidence.
7. Work offline with free tools when feasible (near-zero developer budget). Do not upload private user case files to arbitrary OCR services.

This decision applies to future language-specific OCR as well; English OCR results do not establish Sinhala/Tamil OCR capability.

## Alternatives considered

- **Text extraction only:** simplest but fails completely on scanned PDFs and silently propagates corrupted text.
- **OCR everything:** more compute, can degrade already-correct digital text, and does not solve validation.
- **Manually transcribe all scans:** potentially accurate if reviewed, but does not scale for a broad corpus.
- **Adaptive extraction + QA (chosen):** a manageable extra pipeline stage with explicit failure states and review work.

## Evidence recorded on 2026-11-08

| Source | Original readable pages (>40 extracted characters) | OCR readable pages (>40 extracted characters) | OCR PDF SHA-256 |
|---|---:|---:|---|
| SL-0039 | 0/20 | 20/20 | `985a47b57adde2f39192db68c1f82d54e1cbdafe8aae6ea0561db920a0f7ea63` |
| SL-0003 | 21/21 (corruption observed) | 21/21 (re-OCR) | `168c4165fbe1ddc4aab4bc746934637db956dee5457686a09af0f75c2035b8ef` |

The OCR pages were visually sampled at first, middle and last pages. Output layout looked preserved on these samples. **Word error rate, section-number accuracy, legal completeness, and correctness remain NOT MEASURED.** Text presence must not be presented as OCR accuracy.

Software used: local Tesseract 5.5.0, PyMuPDF, `pdftoppm` (for child PDF), Python 3.13.5; English OCR. A local OCR run is not equivalent to a deployed, tested backend ingestion pipeline. See `corpus/batches/batch-001/OCR_RUN_2026-11-08.csv` and `docs/phase-0/BATCH_001_OCR_REVIEW.md`.

## Privacy and security consequences

- Keep raw documents and derived text distinct; mark derivatives, validate hashes, preserve traceback to official sources.
- Treat OCR output as untrusted, including any injected instructions. OCR and retrieved text never change backend rules.
- Restrict ingestion/admin approval; don't expose public upload/approval endpoints in MVP.
- OCR derivatives may contain errors. Require QA before retrieval and legal interpretation.

## Revisit conditions

Revisit after 50 diverse PDFs, measurable OCR transcription tests with gold text, first Sinhala/Tamil scans, or if runtime/storage cost requires new trade-offs. A future change should be documented in a superseding ADR rather than silently rewriting this decision.

## Portfolio rationale (owner's idea)

A reusable **detect → extract/OCR → validate → approve** pipeline addresses *classes of future failures*, not merely today's two PDFs. This is the architecture insight the owner explicitly asked to preserve for group presentations and interviews. The owner chose the principle; the initial two-PDF local proof of concept was executed with assistant help, and no production implementation claim is made.
