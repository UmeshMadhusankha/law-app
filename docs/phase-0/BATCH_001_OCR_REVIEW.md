# Batch 001 — OCR remediation trial (2026-11-08)

**Scope:** Repair the *extraction layer*, not the laws themselves.
**Decision:** ADR-0008 accepted. **No source promoted to APPROVED_FOR_ANSWER.**

## Inputs and verified outcomes

| ID | Original PDF | Pages | Original hash | Derived OCR PDF | Derived hash | OCR text page presence (>40 chars) |
|---|---|---:|---|---|---|---|
| SL-0039 | National Child Protection Act, No. 50 of 1998.pdf | 20 | `d8c10decf9e808d4eb05a83ade2d662348a43f3b1184737d08ed48874fa15f6c` | `National_Child_Protection_Act_OCR_UNREVIEWED.pdf` | `985a47b57adde2f39192db68c1f82d54e1cbdafe8aae6ea0561db920a0f7ea63` | 20/20 |
| SL-0003 | HRCSL-Act-English.pdf | 21 | `f71645a336b9f4b265325f36e77088a77151064fc9041fc6bb8d0f43f1f6f74b` | `HRCSL_Act_OCR_UNREVIEWED.pdf` | `168c4165fbe1ddc4aab4bc746934637db956dee5457686a09af0f75c2035b8ef` | 21/21 |

- **SL-0039:** Original had **0** extractable characters across 20 pages. Derived PDF has 31,998 characters counted using page.get_text() on PyMuPDF, including whitespace.
- **SL-0003:** Original contained visibly corrupted text; derived PDF has 36,806 extracted characters (including whitespace). Original also contained text, so comparing text-presence ratios cannot establish improvement in accuracy.
- **Visual sampling:** First, middle and last pages of each PDF were rendered for a quick side-by-side layout check. No major layout differences were visually observed in those six page pairs. The word-level OCR accuracy was **not** independently validated.
- **Software/environment:** Tesseract 5.5.0, English data, Python 3.13.5. Child Act: 180 DPI PNG render + Tesseract-generated page PDFs + merge. HRCSL Act: PyMuPDF grayscale renders + re-OCR with single-threaded Tesseract processes, parallel jobs, and page PDF merge. This shows a locally reproducible approach, not production automation.
- **Source authority and legal effective status:** unchanged and **NOT VERIFIED** as part of this experiment.

## Why the Windows command failed

Tesseract cannot accept a PDF as its input image. The screenshot shows `Pdf reading is not supported` and an attempted 0-byte output. The working original must not be overwritten or discarded. Use a PDF-aware OCR tool (such as NAPS2) or render PDF pages into images before calling Tesseract. Quote Windows filenames containing spaces.

## Manual review required before indexing

1. Compare at least three substantive legal provisions in each OCR PDF against the corresponding original page images, including a 'shall not' or other negation where present.
2. Review headings, section identifiers, dates, and cross-references; document exact page/section corrections.
3. Where wording is unclear, preserve the original image and mark **NEEDS_CORRECTION**; never let the AI guess missing characters.
4. Generate searchable chunks only after text QA and legal/source status approval. Record the approving reviewer, timestamp and version.
5. When corrected derivatives are generated, hash them and link back to the original document ID, never replace the original silently.

## Distinguishing what was achieved

- **DONE:** local two-document OCR conversion, searchable text presence verified, source and derived hashes recorded, six page pairs visually sampled, ADR accepted.
- **NOT DONE:** gold transcription, accuracy measurement, provision-specific verification, quality-gated ingestion integration, legal answer approval.
