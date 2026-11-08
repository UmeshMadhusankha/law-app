# Batch 001 — OCR text QA and source-status mapping sprint

**Proposed:** 2026-11-08  
**Owner capacity:** ~10 hours/week; near-zero development budget  
**Current maturity:** Intake and OCR *feasibility* demonstrated; OCR accuracy and current-law status not validated.  
**Related ADRs:** ADR-0002, ADR-0006, ADR-0007, ADR-0008. ADR-0001 remains OPEN.

## Sprint goal

Determine whether recovered text from two problematic official-source PDFs is accurate enough to be considered for structured extraction, without claiming entire-document legal verification. Create a provision-level review trail and start mapping relationships between original statutes, amendments and commencement notices.

## Tasks and estimated time (not time tracked)

| Task | Budget | Output |
|---|---:|---|
| Verify originals and OCR derivatives, preserve exact source IDs and hashes | 1h | Files and identities checked; no originals overwritten |
| Independently compare **three substantive passages per PDF** to visible original page images | 3h | Complete `OCR_PASSAGE_REVIEW.csv`, exact quoted discrepancies noted |
| Re-run extraction/correct passages with errors; record revisions and hash changed derivatives | 2h | New candidate text or documented blockers |
| Map constitutional and PDPA amendment/commencement relationships | 2h | `LEGAL_STATUS_CROSSWALK.csv`, unresolved statuses clearly flagged |
| Draft five candidate question/source pairs and update metrics & evidence logs | 2h | Draft questions + updated metrics; no legal correctness claim |

## OCR passage review procedure

1. Use the original PDF as independent visual ground truth. Do **not** use the OCR text as its own reference.
2. For each document, select at least three **substantive sections/provisions** from different pages. The six worksheet rows are placeholders; choose actual section IDs and page numbers from the original.
3. Record the document's own printed page number *and* PDF page number, since they can differ.
4. Compare every word of the chosen passage, including negatives, numbers, dates, names and cross-references. Record actual errors, without inferring legal correctness.
5. Mark a passage `PASS` only if fully compared and no transcription differences were found. Mark `FAIL` for a mismatch, `BLOCKED` when text cannot be read, or leave `NOT_REVIEWED`.
6. Classify any detected errors: `NEGATION`, `SECTION_ID`, `NUMBER_OR_DATE`, `OMITTED_TEXT`, `TYPO`, `READING_ORDER`, `OTHER`.
7. Do not mark either document `APPROVED_FOR_ANSWER` on the strength of six spot checks. To make legal answers, we still need adequate provision-level coverage, version/commencement verification, evaluated retrieval, and qualified legal review.

## Proposed QA metrics (all currently NOT MEASURED)

- Sampled passage exact-match rate = passages marked PASS / passages actually fully reviewed. Report numerator, denominator and selection method. No target established yet.
- Critical OCR error count = confirmed changes involving negation, section ID, numbers/dates, or omission that could change legal meaning.
- Review coverage = provisions with human OCR comparison / candidate provisions in the chosen answer scope. Total count requires a section inventory; TBD.
- Text availability is a separate metric: 20/20 and 21/21 OCR text-layer pages were previously observed; this is **not accuracy**.

## Legal applicability review procedure

- Preserve as a separate dimension from text quality.
- Constitution consolidation and 2026 amendment: record exact affected provision IDs and effective evidence; don't assume the consolidation is automatically current.
- Data Protection Act 2022, Amendment Act 2025, and Gazette 2498/16: map each targeted provision, the effect of the amendment, and the Gazette's scope rather than applying one status to the whole Act.
- Use `UNKNOWN_PENDING_VERIFICATION` when effective date/authority/version is unresolved.
- Legal-status assertions for user-facing answers require authoritative source evidence and, where needed, qualified legal review.

## Exit criteria for this sprint

- Six passages independently compared, with page references and outcomes **or** blockers recorded.
- At least one observed extraction issue is characterized or an explicit no-issue result is documented from the reviewed sample.
- Crosswalk draft created; ambiguous legal statuses recorded as pending instead of guessed.
- Metrics updated with measured numerators/denominators; no invented OCR accuracy or legal correctness values.
- No unreviewed OCR text promoted to approved retrieval evidence.

## Milestone reporting template

- **Decision update:** ADR-0008 remains accepted; record any needed revision using a new ADR.
- **Metric/evidence update:** Six passage rows, with observed review statuses, benchmark version, run date and commit.
- **CV/portfolio insight:** Describe the actual QA method and error findings only after completed.
- **Pitch/story update:** Explain why PDF text presence != trustworthy legal text.
- **Next verification:** Extend review coverage, map effective dates, and create initial legal QA questions.

## Sampling discipline — conflict-resolution refinement

The six hand-selected passages are a **diagnostic sample**, not a statistically representative estimate of whole-document OCR accuracy. Before examining the derived OCR text, record why each original provision was chosen (for example, beginning/middle/end of the Act or a passage containing a negation, section number, or cross-reference). Do not select only easy-to-read passages to inflate results. Report any exact-match percentage only as a **sampled-passages** result with the numerator, denominator, reviewer, extraction version, and sampling notes. Never label it “overall document OCR accuracy.”
