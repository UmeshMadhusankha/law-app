# Batch 001 — Next sprint documentation overlay

**Date:** 2026-11-08  
**Purpose:** Begin source-text quality assurance before retrieval/indexing.  
**Status:** Planning materials only; no new OCR accuracy or legal validation results are claimed.

Files to copy into your existing GitHub working tree:

- `docs/phase-0/BATCH_001_TEXT_QA_SPRINT.md`
- `corpus/reviews/batch-001/OCR_PASSAGE_REVIEW.csv`
- `corpus/reviews/batch-001/LEGAL_STATUS_CROSSWALK.csv`

Review your Git changes before committing:

```bash
git status
git diff --stat
git add docs/phase-0/BATCH_001_TEXT_QA_SPRINT.md corpus/reviews/batch-001/
git commit -m "docs: plan Batch 001 OCR validation and legal-status review"
git push origin main
```

Do not overwrite prior ADRs, OCR reports, or source manifests. Keep original legal PDFs unchanged. These review sheets are not an approval for AI answers.
