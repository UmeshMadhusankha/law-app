# Metrics Ledger — measurable engineering evidence

Last updated: 2026-11-07. **All results below are NOT MEASURED. No baseline or target has been validated.**

## Registry

| Metric | Operational definition | Slice / report standard | Baseline | Target | Actual | Status |
|---|---|---|---|---|---|---|
| Retrieval recall@5 | Answerable benchmark questions with at least one gold supporting source in top 5 ÷ answerable benchmark questions | By language and legal topic | TBD | TBD | — | NOT MEASURED |
| Citation correctness | Verified cited legal source/provision pairs ÷ all evaluated citation pairs | Human checked; official source/version verified | TBD | TBD | — | NOT MEASURED |
| Claim-level grounding | Material answer claims supported by relevant cited passages ÷ all evaluated material claims | Human check for legal interpretations | TBD | TBD | — | NOT MEASURED |
| Unsupported-question abstention recall | Unsupported benchmark questions appropriately abstained on ÷ all unsupported questions | Alongside false abstention rate | TBD | TBD | — | NOT MEASURED |
| False abstention rate | Answerable benchmark questions unnecessarily abstained on ÷ all answerable questions | By language/topic | TBD | TBD | — | NOT MEASURED |
| Current-source compliance | Evaluated citations matching verified applicable document versions ÷ evaluated citations | Verify dates, amendments, authority | TBD | TBD | — | NOT MEASURED |
| Prompt-injection defense pass rate | Attack test cases not achieving the prohibited action/behavior ÷ all adversarial cases | Test by attack family and severity | TBD | TBD | — | NOT MEASURED |
| Unsafe/misleading answer rate | Evaluated answers judged unsafe or materially misleading ÷ all evaluated answers | Include legal professional review as needed | TBD | TBD | — | NOT MEASURED |
| p95 server response latency | 95th percentile of server-side request durations under stated load | Hardware, concurrency, region, language | TBD | TBD | — | NOT MEASURED |
| Average provider cost/request | Total model + retrieval provider cost ÷ evaluated requests | Show currency and rate-date | TBD | TBD | — | NOT MEASURED |
| API availability | Successful eligible API requests ÷ all eligible requests in observation window | Specify observation period and exclusion rules | TBD | TBD | — | NOT MEASURED |

## Benchmark run template (duplicate for every run)

- **Run ID / date:**
- **Git commit / configuration / prompt version:**
- **Corpus version and last verified date:**
- **Benchmark set version, sample size, language/topic distribution:**
- **Environment / concurrency / geography / provider/model versions:**
- **Metric and precise numerator / denominator / units:**
- **Baseline measurement:**
- **New measurement and confidence interval, if meaningful:**
- **Evaluation method, human reviewers, adjudication process:**
- **Raw report or script link:**
- **Limitations, regressions, and follow-up:**
- **Approval to cite on CV?** No, until evidence is reviewed.

## Reporting integrity rules

- No invented results, fabricated targets, or cherry-picked test cases.
- A retrieval/grounding score is not "legal correctness confidence" or a guaranteed probability.
- Use stable held-out benchmarks, report denominator/sample count, failure cases, and language-level results.
- Compare against a measured baseline before claiming improvement.
- For resumes and talks, use only results backed by reports/scripts and the associated implementation commit.
