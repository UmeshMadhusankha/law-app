# Batch 001 — OCR text QA and legal-status mapping sprint

**Proposed:** 2026-11-08  
**Owner capacity:** ~10 hours/week; near-zero development budget  
**Current maturity:** Batch 001 intake and OCR feasibility demonstrated; OCR word accuracy and legal status are **NOT VERIFIED**.  
**Related ADRs:** ADR-0002, ADR-0006, ADR-0007, ADR-0008. ADR-0001 remains open.

## Goal

Determine whether the recovered text from two problematic official-source PDFs is accurate enough to proceed to structured extraction. This is not an approval of entire documents for legal AI answers.

## Tasks (planning estimates, not measured time)

| Task | Estimated effort | Evidence |
|---|---:|---|
| Confirm original and OCR PDF identities and SHA-256 hashes | 1 h | Preserved originals and identity checks |
| Compare 3 substantive passages in each OCR PDF against original page images | 3 h | `corpus/reviews/batch-001/OCR_PASSAGE_REVIEW.csv` |
| Correct and document observed OCR errors | 2 h | Revision history and derivative hashes |
| Draft provision-level amendment/commencement crosswalk | 2 h | `corpus/reviews/batch-001/LEGAL_STATUS_CROSSWALK.csv` |
| Draft 5 question/source pairs and update metric/portfolio logs | 2 h | Versioned evaluation seed and evidence links |

**Estimated total:** 10 hours. **Expected tooling cost:** $0 using existing local tools.

## Six-passage manual OCR review

1. Open the **original** PDF and OCR-generated PDF side by side; the original page image is the transcription reference.
2. Choose three substantive legal provisions from different pages of the National Child Protection Authority Act (SL-0039), and three from the Human Rights Commission Act (SL-0003).
3. Fill the provided review worksheet with exact PDF page, printed page, provision ID, and both independently read original wording and extracted OCR wording.
4. Check every word; prioritize **negations**, section numbers, dates, names, lists and cross-references.
5. Mark `PASS` only after fully comparing the passage. Use `FAIL` for a confirmed mismatch; `BLOCKED` for illegible pages; otherwise retain `NOT_REVIEWED`.
6. Record error category (NEGATION, SECTION_ID, NUMBER_OR_DATE, OMITTED_TEXT, TYPO, READING_ORDER, OTHER), reviewer, date and corrections. Never infer missing legal words.
7. Do not promote either Act to `APPROVED_FOR_ANSWER` after just six passage checks. Sample checks are a diagnostic, not proof of whole-document accuracy.

## Metrics (NOT MEASURED yet)

- **Sample passage exact-match rate:** `fully compared passages marked PASS / all fully compared passages`. Record sample selection, numerator and denominator.
- **Critical error count:** confirmed differences involving negation, section identifiers, dates/numbers or omission that might affect legal interpretation.
- **Provision verification coverage:** `reviewed target provisions / total target provisions` (denominator TBD pending provision inventory).
- **Text availability:** the prior OCR run found text on 20/20 child-protection PDF pages and 21/21 HRCSL pages. This is **not a transcription accuracy metric**.

## Temporal law-status crosswalk

Preserve separate dimensions for OCR quality and legal applicability. Map the 2023 Constitution consolidation to the certified 2026 22nd Amendment; and the 2022 Personal Data Protection Act to its 2025 amendment and 2026 commencement Gazette.

Record precise provision IDs, official source URLs, effective-date evidence and relevant as-of date. Mark unresolved fields `UNKNOWN_PENDING_VERIFICATION`. A publication date alone does not prove commencement.

## Exit criteria

- Six passage review rows either fully documented or explicitly blocked.
- A legal-status crosswalk draft with unresolved items flagged rather than guessed.
- Errors and any corrected text revisions linked to their original PDF and SHA-256.
- Metric ledger and portfolio logs updated **only** with actual results.
- No unverified OCR text promoted to approved legal-answer evidence.

## Mandatory milestone record

- **Decision:** ADR-0008 remains accepted unless a new ADR supersedes it.
- **Metric/evidence:** Results with source hash, selection method, reviewer and commit.
- **CV:** Only activities actually carried out and verified.
- **Pitch:** Explain why searchable PDF text is not automatically trustworthy legal text.
- **Next verification:** Wider OCR audit and document/version checks before section-aware retrieval.
