# OCR remediation milestone — read me first

This update adds **ADR-0008**, revised ADR index, a Batch 001 OCR metrics entry, CV evidence, pitch update, run manifest and a Windows troubleshooting guide. It is a **documentation overlay** for the previously delivered Batch 001 GitHub-ready package.

To apply: unzip this documentation patch into your GitHub working repository, preserving `docs/` and `corpus/` paths; review the diff; commit. The OCR output PDFs are provided separately and should be retained as **UNREVIEWED** derivatives of the original PDFs, not as replacements for the originals or approved RAG chunks.

```bash
git add docs corpus/batches/batch-001/OCR_RUN_2026-11-08.csv OCR_FIX_START_HERE.md
git commit -m "docs: record adaptive OCR quality gate and Batch 001 remediation"
```

Recorded: 2026-11-08. Tesseract 5.5.0, English OCR. Child scan: 20/20 pages searchable post OCR; HRCSL: 21/21 pages searchable post re-OCR. These are **text-presence diagnostics**, not measured accuracy.
