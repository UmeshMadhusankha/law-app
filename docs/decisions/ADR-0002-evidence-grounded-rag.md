# ADR-0002 — Evidence-grounded RAG with deterministic verification

- **Date:** 2026-11-07
- **Status:** Proposed — NOT adopted yet
- **Decision type:** AI architecture

## Context

The assistant must cite precise, applicable Sri Lankan legal sources and avoid unsupported authoritative claims. Prompt-only requests to "be confident" are not an adequate safety mechanism.

## Options to evaluate

| Option | Strength | Concern |
|---|---|---|
| Direct hosted LLM | Simple | Unverifiable source provenance and legal currency |
| Basic vector RAG | Fast proof of concept | Weak handling of sections, versions, conflicting evidence |
| Section-aware, hybrid evidence-grounded RAG with backend checks | More auditable citations and abstention | Additional ingestion and evaluation complexity |

## Proposed design

Versioned authoritative legal corpus → section-aware indexing → retrieval → evidence sufficiency checks → bounded answer generation → structured validation and citation matching → evidence status or abstention.

## Evidence required before acceptance

Run an initial gold-set benchmark comparing at least a direct-LLM baseline and a simple retrieval baseline, and inspect citation validity, unsupported-claim rate, refusal behavior, and cost/latency. Define which checks are deterministic and which require human/legal expert judgment.

## Revisit trigger

If high-quality, versioned sources cannot be acquired, if citations remain unreliable, or if operating costs exceed budget.
