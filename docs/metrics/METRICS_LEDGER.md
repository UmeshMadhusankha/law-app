# Engineering Metrics Ledger

**Initialized:** 2026-11-07  
**Status:** definitions only — **NO application evaluation has been performed**.  
**Important:** Avoid invented baselines or retrospective claims. All current results = **NOT MEASURED**, targets = **TBD**.

| ID | Metric | Exact calculation / unit | Baseline | Target | Result | Dataset / run evidence |
|---|---|---|---|---|---|---|
| M-01 | Retrieval Recall@5 | # answerable gold questions with >=1 correct, currently approved gold passage in top 5 ÷ # answerable gold questions ×100% | NOT MEASURED | TBD | NOT MEASURED | No gold benchmark yet |
| M-02 | Citation identity correctness | # exact citations mapped to correct approved doc/version/section/excerpt ÷ # evaluated citations ×100% | NOT MEASURED | TBD | NOT MEASURED | No system yet |
| M-03 | Source applicability compliance (redefined 2026-11-08) | # reviewed primary legal claims using provision verified applicable on the claim’s relevant as-of date ÷ # reviewed primary legal claims requiring a temporal applicability determination ×100% | NOT MEASURED | TBD | NOT MEASURED | No corpus yet |
| M-04 | Claim-level grounding precision | # reviewed atomic legal claims fully supported by cited evidence ÷ # reviewed atomic legal claims ×100% | NOT MEASURED | TBD | NOT MEASURED | Human reviewer required |
| M-05 | Legal answer correctness | # domain-reviewed correct answers ÷ # domain-reviewed answerable cases ×100% (report rubric and ambiguous cases separately) | NOT MEASURED | TBD | NOT MEASURED | No expert review yet |
| M-06 | Safe abstention recall | # correct abstentions for gold unsupported cases ÷ # gold cases requiring abstention ×100% | NOT MEASURED | TBD | NOT MEASURED | No benchmark yet |
| M-07 | False abstention rate | # answerable gold questions incorrectly abstained ÷ # answerable gold questions ×100% | NOT MEASURED | TBD | NOT MEASURED | No benchmark yet |
| M-08 | Unsafe response rate | # outputs judged unsafe/misleading at defined severity ÷ # reviewed responses ×100% | NOT MEASURED | TBD | NOT MEASURED | No review yet |
| M-09 | Prompt-injection defense pass | # adversarial tests avoiding specified violation ÷ # completed adversarial tests ×100% | NOT MEASURED | TBD | NOT MEASURED | No test suite yet |
| M-10 | p50/p95 API response latency | 50th/95th percentile of request completion times in ms | NOT MEASURED | TBD | NOT MEASURED | No endpoint yet |
| M-11 | Cost per request | (tracked inference + attributable hosting spend) ÷ billable requests, currency/request | NOT MEASURED | TBD | NOT MEASURED | No provider selected |
| M-12 | API failure rate | # failed requests under published policy ÷ # attempted requests ×100% | NOT MEASURED | TBD | NOT MEASURED | No endpoint yet |
| M-13 | Sinhala / Tamil quality by language | M-01–M-08 measured separately for each released language | NOT MEASURED | TBD | NOT MEASURED | No language gold set |

## Mandatory per-run evidence template

```markdown
### Run ID: RUN-YYYYMMDD-###
- Date/time (UTC):
- Metric IDs and definitions (version):
- Benchmark dataset version + content hash:
- Environment (hardware/runtime/deployment):
- Git commit and pipeline version:
- Source corpus snapshot + document versions:
- LLM/embedding models, parameters, prompts:
- Sample size and numerator/denominator:
- Baseline comparator:
- Result + unit:
- Reviewer rubric/role and disagreements:
- Reproduction commands / artifact paths:
- Errors/limitations:
```

## Research work vs engineering outcome

Research findings (e.g. official legal-source links, Google Play policy requirements) are **verified research inputs**, not performance metrics. Proposed test-set sizes are **plans**, not completed evaluations. Only populate results after a reproducible experiment.

## New temporal and source-coverage metrics — defined 2026-11-08

| ID | Metric | Exact calculation / unit | Baseline | Target | Result | Evidence |
|---|---|---|---|---|---|---|
| M-14 | Temporal applicability correctness | # reviewed time-dependent QA cases where cited primary provisions were applicable on relevant date ÷ # reviewed time-dependent answerable QA cases ×100% | NOT MEASURED | TBD | NOT MEASURED | No temporal gold set |
| M-15 | History/future mislabeling rate | # evaluated answers presenting non-current law as currently operative ÷ # reviewed answers containing non-current legal material ×100% | NOT MEASURED | TBD | NOT MEASURED | No evaluated responses |
| M-16 | Source approval compliance | # citations resolved to source versions approved for that claim type and date ÷ # evaluated citations ×100% | NOT MEASURED | TBD | NOT MEASURED | No corpus/validator |
| M-17 | Approved topic coverage | # reviewed benchmark topic clusters meeting legal-source review gate ÷ # declared target topic clusters ×100% | NOT MEASURED | TBD | NOT MEASURED | No approved taxonomy |

Report `NOT APPLICABLE` separately for metrics with zero denominators; never report 100% for no samples. Record the evaluation date as well as the **legal as-of date**.

**Definition note (2026-11-08):** M-03 now evaluates claim-date applicability rather than declaring all historical/future citations wrong. Separately labeled historical/future context belongs in M-15; baseline remains NOT MEASURED.


## Corpus discovery baseline — 2026-11-08

| Metric | Definition | Observed value | Scope / evidence |
|---|---|---|---|
| Discovery records logged | Number of manifest rows from official source pages, **including portal listings** | 20 references | `corpus/registry/sources.jsonl`, discovery v0.1; not 20 statutes |
| Downloaded document count | Number of original source PDF files successfully acquired into corpus workspace | 0 | `corpus/raw/` absent; outbound fetch unavailable in execution container |
| Download success rate | Successfully downloaded files / attempted eligible downloads | NOT MEASURED | Only access feasibility checked; no structured acquisition run |
| Source extractability | Sampled source sections reproducing authoritative pages correctly / sampled sections | NOT MEASURED | No raw documents available locally |
| Source currency coverage | Reviewed provisions whose applicability date and governing amendments are resolved / all reviewed provisions | NOT MEASURED | No provision-level review |
| Topic coverage quality | Source completeness, extraction, authority and reviewer validation by topic | NOT MEASURED | `docs/phase-0/MVP_COVERAGE_DECISION_MATRIX.md` |
| AI-answer eligibility | Number of provision clusters approved by reviewers and eval gates | 0 | `approval_state=NOT_APPROVED` for all discovered records |

All metrics describe **discovery artifacts only**, not legal correctness or RAG model performance. Implementation commit/benchmark N/A until the user commits this package.

## First uploaded corpus batch — 2026-11-08 (Batch 001)

**Method:** User-uploaded `law app batch 1.zip`; PyMuPDF page extraction; SHA-256 of PDF bytes; page text presence diagnostic. **Environment:** local sandbox Python/PyMuPDF, no hosted LLM. **Commit:** NOT RECORDED. **Version:** local ingestion script v0.1 at `scripts/ingest_batch.py`. **Evidence:** `corpus/batches/batch-001/BATCH_MANIFEST.csv`, `pages/`, `docs/phase-0/BATCH_001_INGESTION_AUDIT.md`.

| Metric | Definition / numerator and denominator | Baseline | Actual batch result | Interpretation |
|---|---|---|---|---|
| Uploaded originals recorded | Number of distinct readable PDF files mapped to the registry | 0 | **10 documents** | 10/10 opened; source/legal provenance still needs review |
| Pages enumerated | Total PDF pages over all uploaded originals | 0 | **538 pages** | Page count, not coverage |
| Text-presence diagnostic | Pages with >100 stripped characters in chosen draft extraction / all pages | NOT MEASURED | **507/538 (94.24%)** | Diagnostic only; no accuracy guarantee; threshold chosen for triage |
| Image-only PDF count | PDFs with no embedded extracted text across all pages / PDFs | NOT MEASURED | **1/10** | SL-0039; 20 pages; full OCR outstanding |
| OCR trial pages | Number of child-protection PDF pages sampled using Tesseract English | 0 | **2 pages**, PDF pp. 1, 3 | Sampled only; full OCR completeness NOT MEASURED |
| Documents with OCR-damaged embedded text | PDFs manually identified in preliminary text sample | NOT MEASURED | **1 flagged** (SL-0003) | Screening observation, not a complete OCR quality audit |
| Search chunks created | Count of section-aware retrieval chunks | 0 | **0** | By design pending legal section parser and QA |
| Provision-level source validity / currency | Reviewed provision/date/status pairs / provision pairs selected for assessment | NOT MEASURED | **NOT MEASURED** | No legal professional validation yet |
| Legal question correctness and citation validity | Review-validated legal answer set and citation scores | NOT MEASURED | **NOT MEASURED** | No answer generator or benchmark run |
| AI-approved sources | Documents whose necessary provision-level quality and legal review passed | 0 | **0** | All approval states NOT_APPROVED |

The denominator 538 includes legitimate blank/cover pages, so the diagnostic must **not** be called OCR accuracy. Retrieval-quality and legal-answer targets remain TBD until a reviewed benchmark exists.

## Batch 001 OCR proof of concept — 2026-11-08

These are **document processing diagnostics**. They do not measure transcription quality, legal correctness, retrieval performance, or OCR word error rate. Sources are identified in `corpus/batches/batch-001/OCR_RUN_2026-11-08.csv`.

| Metric | Definition / unit | Sample | Baseline (original) | Post-OCR observation | Target | Reproduction evidence |
|---|---|---|---|---|---|---|
| OCR-01, text presence SL-0039 | Pages with >40 extracted characters / original pages | 20 pages, one document | 0/20 (0%) | 20/20 (100%) | TBD | PyMuPDF page text; derived PDF SHA-256 in OCR_RUN CSV |
| OCR-02, text presence SL-0003 | Pages with >40 extracted characters / original pages | 21 pages, one document | 21/21 (100%), despite visible corruption | 21/21 (100%) | TBD | PyMuPDF page text; derived PDF SHA-256 in OCR_RUN CSV |
| OCR-03, OCR transcription accuracy | Correctly transcribed gold words / checked gold words ×100% | Gold word sample NOT CREATED | NOT MEASURED | NOT MEASURED | TBD | Requires manually validated page transcripts |
| OCR-04, legal section anchor accuracy | Correctly transcribed section identifiers / reviewed section identifiers ×100% | Gold anchors NOT CREATED | NOT MEASURED | NOT MEASURED | TBD | Requires section-level manual review |
| OCR-05, visual format sample | Pages rendered for manual layout comparison | 3 pages × 2 PDFs = 6 page pairs | Original pages visually available | 6 corresponding OCR page layouts sampled; no major visible layout change observed | TBD | Contact-sheet review; not formal fidelity score |

- **Date:** 2026-11-08. **Environment:** local container, Python 3.13.5, Tesseract 5.5.0, English OCR, PyMuPDF. **Implementation Git commit:** NOT YET COMMITTED.
- **Input corpus:** uploaded Batch 001, source hashes preserved in `BATCH_MANIFEST.csv`. **OCR derived output:** see `OCR_RUN_2026-11-08.csv`.
- **Measurement limitation:** no semantic review or gold standard; no claim that OCR is accurate enough for legal AI.
