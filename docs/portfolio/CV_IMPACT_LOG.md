# CV / Portfolio Evidence Log

**Initialized:** 2026-11-07  
**Rule:** distinguish planned, drafted and validated. Do not claim implementation, deployment, security validation or metric improvements until backed by commits/tests.

## Entry CV-0001 — Phase 0 requirements and design records

- **State:** DRAFTED (subject to owner's review and commit)
- **Problem:** general legal assistant may hallucinate, cite superseded provisions and mishandle sensitive questions.
- **Design work documented:** proposed narrow pilot, provision-level source registry, deterministic citation checking, qualitative evidence status, and human-reviewed benchmark/release gates.
- **Owner's implemented contribution:** **NOT YET DOCUMENTED**. This pack is an AI-assisted proposal; commit, review, ownership and further work should be recorded truthfully.
- **Tests and outcomes:** **NOT MEASURED / NOT IMPLEMENTED**.
- **Trade-off:** reduced initial breadth for traceable, testable legal information.
- **Evidence links:** `docs/phase-0/PRD.md`, `docs/phase-0/RESEARCH_FINDINGS.md`, `docs/decisions/ADR-0001-narrow-mvp-scope.md`, `docs/decisions/ADR-0002-source-authority-and-currency.md`.
- **Future commit/PR:** TBD.

## Planned evidence opportunities (NOT accomplishments)

| Opportunity | What to actually do | Evidence to collect | Status |
|---|---|---|---|
| Versioned legal corpus | Implement source/version/provision approvals and change detection | Source registry schema, source hash manifest, reviewer checklist, tests | PLANNED |
| Retrieval evaluation | Run baseline vs hybrid retrieval on reviewed gold questions | Recall@5, failure taxonomy, code/config/commit | PLANNED |
| Citation validator | Reject unknown, stale and mismatched references | Unit tests and negative-case report | PLANNED |
| Security & privacy | Add secret isolation, rate limits, safe logging and injection tests | Threat model, security test report, CI artifacts | PLANNED |
| Cross-platform app | Implement one API with Flutter Android and Web | Device/browser results, accessibility checks, demo | PLANNED |
| Multilingual QA | Compare English/Sinhala/Tamil on reviewed terminology scenarios | Per-language scores and human-reviewed examples | PLANNED |

## CV bullet template — DO NOT USE AS COMPLETED YET

> Designed and evaluated a version-controlled, evidence-grounded legal-awareness RAG pipeline for Sri Lankan law, achieving **[measured metric + sample]** on **[reviewed benchmark version]** and implementing **[verified safety controls]**; evidence: **[commit/report URL]**.

Only use once work, ownership and metrics are real. Prefer modest factual bullet if no quantified outcome exists.

## Problem–Action–Result interview story scaffold

- **Situation:** Official legal sources can disagree across publication dates; users need correct current law, not merely official-looking PDFs.
- **Task:** Design a retrieval/generation system that recognizes legal version and effective date.
- **Action (proposed):** Versioned corpus, provision-level approval, explicit abstention for uncertain currentness, citation validation, review trail.
- **Result:** **TBD — no deployed system or experiment yet.**
- **Learning:** Authenticity != current legal applicability; deterministic checks reduce certain errors but do not guarantee legal correctness.

## Update after each meaningful milestone

Record date, engineer's own contribution, accepted ADR, tests/dataset, actual result, commit link and honest limitation. No fabricated percentages or retrospective authorship.

## Entry CV-0002 — Phase 0 temporal-law design discussion (2026-11-08)

- **State:** REQUIREMENTS AGREED / DESIGN DOCUMENTED; not implemented or measured.
- **Owner contribution:** proposed retaining historical and forthcoming legal provisions and separating them from currently applicable legal material; challenged narrow domain coverage and articulated future referral concept.
- **Engineering response:** accepted ADR-0006 and proposed two-stage corpus discovery/answer approval in ADR-0007; kept ADR-0001 open.
- **Constraints recorded:** English-only internal prototype, ~10 hours/week, approximately zero budget, prospective but unconfirmed legal reviewer.
- **Tests/metrics:** NOT MEASURED.
- **Potential interview story:** Why source authenticity alone fails to establish legal applicability, and how legal-effective time differs from ingestion time.
- **Evidence:** `docs/decisions/ADR-0006-temporal-law-status.md`, `docs/phase-0/PHASE0_DECISION_UPDATE_2026-11-08.md`. Commit/PR TBD.


## Entry CV-0003 — Source-first scope planning (2026-11-08)

- **Stage:** Product discovery and documentation, not an implemented RAG corpus.
- **Owner contribution:** proposed first researching available official laws and organizing them into approximately 20 subject areas before deciding the MVP domain; insisted on quality as the first selection criterion.
- **Evidence prepared:** topic taxonomy, 20 source/portal metadata records, source-review gates, draft topic-coverage matrix, ADR-0007 acceptance and ADR-0001 deferral.
- **Implementation / evaluations:** 0 downloaded PDFs, 0 indexed documents, 0 approved legal provisions; AI evaluation NOT MEASURED.
- **Future demonstrable outcome:** after ingestion, show checksum manifest, extraction QA report, amendments graph, per-topic review coverage and audited decision record. **No claimed improvement yet.**
- **Interview story:** "I avoided fixing the MVP scope based on guesswork. We designed a source-first decision framework and separate legal source availability from permission to produce AI answers."

## Entry CV-0004 — First reproducible PDF ingestion trial (2026-11-08)

- **Stage:** Completed ingestion *trial*, not production corpus or legal answer engine.
- **Problem:** Official Sri Lankan legal PDFs differ substantially in text availability, formatting, amendment relationships and effective dates.
- **Contribution:** Supplied the first 10-document batch and worked through a SHA-256 inventory, 538-page text extraction with original page provenance, issue triage, and temporal-link registry. Local extractor reproducibility recorded; no deployment or retrieval benchmark.
- **Measured observation:** 10 PDFs enumerated; 507/538 pages contain >100 draft text characters; 1 image-only 20-page PDF identified; 2 OCR sample pages tested; 0 sources legal-answer approved. These are **engineering intake diagnostics**, not legal correctness or a user outcome.
- **Evidence:** `corpus/batches/batch-001/BATCH_MANIFEST.csv`, `docs/phase-0/BATCH_001_INGESTION_AUDIT.md`, `scripts/ingest_batch.py`. Commit link TBD.
- **Future CV bullet (hold until production/eval):** "Built a version-aware legal-source ingestion pipeline supporting XX validated legal documents and improved retrieval recall@k from baseline X to Y" — **NOT YET ACHIEVED; placeholders are not measurements.**
- **Interview story:** "We found that one Act was image-only and another had corrupted OCR. Rather than push the raw extracts into RAG, we recorded provenance and stopped at a quality gate until transcription could be verified."

## ADR-0008 — Adaptive OCR and validation boundary (2026-11-08)

- **Problem:** A 20-page statutory scan yielded no text; a 21-page official Act contained garbled text despite having a text layer. The user's Windows Tesseract invocation also failed because PDF is not a supported input type.
- **Owner's engineering contribution:** Identified and explicitly approved the generalized design pattern: diagnose extraction first; route to direct extraction or OCR as required; **validate** before promoting material to the legal RAG corpus. Requested that this decision, alternatives, and reason be documented for presentations.
- **Assistant-supported local experiment (completed):** Produced separate English OCR derivatives of both PDFs. Child scan: 0/20 -> 20/20 pages with >40 extractable characters. HRCSL: 21/21 pages with text before and after, but the original text was visibly corrupted. New derivatives have hashes and were sampled visually.
- **Not yet done:** Implement adaptive dispatch in the actual backend, automated OCR QA, manually corrected gold transcriptions, or approved legal-source ingestion. **OCR correctness: NOT MEASURED.**
- **CV bullet, cautious current wording:** "Documented an adaptive, provenance-preserving OCR strategy for a Sri Lankan legal RAG corpus and validated a two-document offline feasibility test, recovering searchable text from a 20-page image-only Act." Clarify in interview that the owner made the design choice and the proof of concept was carried out with assistant help.
- **Future bullet (do not use yet):** "Implemented and evaluated an automated, source-aware PDF extraction pipeline across N verified statutes, achieving X% gold transcription accuracy." Placeholder only.
- **Evidence:** `docs/decisions/ADR-0008-adaptive-extraction-and-ocr-quality-gates.md`; `corpus/batches/batch-001/OCR_RUN_2026-11-08.csv`; OCR output PDFs; git commit TBD.
- **Interview STAR outline:** Situation—mixed scans and broken text. Task—avoid feeding corrupted statutory provisions to RAG. Action—choose adaptive OCR plus quality gates, preserve original source and derived text. Result—a small offline feasibility test and traceable samples; quality and production evidence still pending.

## Entry CV-0004 — Owner-confirmed OCR failure modes (2026-11-08)

- **Status:** Three short-span findings confirmed by the project owner; **no whole-document verification or released pipeline**.
- **Problem:** OCR can silently change legal cross-references and section identifiers in government-source PDFs.
- **Owner contribution:** Checked and corroborated three highlighted discrepancies in the National Child Protection Authority Act; explicitly prioritized limited review time rather than declaring other samples correct.
- **Assistant contribution:** Identified candidate anomalies, prepared comparison evidence and updated repository worksheets/documentation.
- **Observed evidence:** One word-space error, one paragraph-label substitution, and errors involving statutory identifiers in section 39; exact individual tokens of the third issue await owner transcription. See `corpus/reviews/batch-001/OCR_PASSAGE_REVIEW.csv` and the AI preflight report.
- **Unmeasured:** OCR accuracy, full-provision fidelity, overall corpus quality, legal correctness, and retrieval performance.
- **Interview-ready story (current scope):** “We discovered that a searchable legal PDF can still contain wrong provision references. I verified three OCR anomalies against source images and retained a quality gate before legal RAG indexing. Broader review and automatic validation remain to be built.”
